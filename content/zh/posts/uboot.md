---
title: "uboot"
date: 2021-06-28T15:30:47+08:00
description: uboot相关
# weight: 1
# aliases: ["/first"]
draft: true
author: "嘟囔"
# author: ["Me", "You"] # multiple authors
tags: ["uboot"]
categories: ["Embedded"]
---
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=65766&auto=1&height=66"></iframe>

## uboot的作用

 是bootloader的一种，bootloader类似于PC上的BIOS，其作用是为操作系统的启动初始化硬件环境，加载启动操作系统。

## uboot源码的获取

 途径一： [去uboot官网网站下载](http://www.denx.de/wiki/U-Boot/WebHome)  
途径二： 上游厂家 （追溯芯片厂家） //如果移植时墙裂建议使用该代码修改。

## uboot源码编译

```sh
make xxx_config
make
make clean # 清除编译过程中产生的中间文件
make distclean # 清除配置和编译过程中产生的文件
```

## uboot源码阅读

1. 寻找入口点
```sh
rm uboot
make V=1
# 继而分析链接过程   
start.S	
vim u-boot.lds
```

```c
    .text :
	{
		arch/arm/cpu/XXX/xxx/start.o (.text*)
        ...
    }
```
入口点 arch/arm/cpu/XXX/xxx/start.S

2. u-boot启动第一个阶段

start.S    
设置为SVC  
关闭看门狗  
使CACHE 无效  
禁止MMU  
清0BSS段  
完成一系列硬件的初始化  
调用run_main_loop  

```c
//board_f.c
bl  board_init_f{  
    //完成了一系列硬件的初始化
	initcall_run_list(init_sequence_f) 
    ...
}
//board_r.c
ldr pc, =board_init_r{ 
    //完成一系列硬件的初始化 最后执行了run_main_loop	
    initcall_run_list(init_sequence_r) 	
    ...
}
```

3. u-boot启动的第二个阶段
   
获取环境变量bootdelay  
获取环境变量bootcmd  
倒数读秒计时  
无打断， 执行bootcmd中的命令： 加载启动内核  
有打断， 输出命令提示符 接收用户命令 匹配执行命令

```c
main_loop{
	s = bootdelay_process() 
    {
	    s = getenv("bootdelay");
	    bootdelay = s ? (int)simple_strtol(s, NULL, 10) : CONFIG_BOOTDELAY;
	    s = getenv("bootcmd");
	    stored_bootdelay = bootdelay;
	    return s;
	}
	autoboot_command(s) 
    {
	    //倒数读秒计时 判断是否有用户打断
	    if (stored_bootdelay != -1 && s && !abortboot(stored_bootdelay)) 
        {
	        //如果没有用户打断 就执行bootcmd中记录的命令
	        //加载内核 启动内核 uboot后续代码不会被执行到了
	        run_command_list(s, -1, 0);
	    }
    }
				
	cli_loop()
    {
	    cli_simple_loop()
        {
	        for (;;) 
            {
	            //输出命令提示符 接收用户输入的命令 存储到console_buffer
	            len = cli_readline(CONFIG_SYS_PROMPT);
	            strcpy(lastcommand, console_buffer);
                run_command_repeatable(lastcommand, flag);
			}
		}
	}	
}  
```

## 附

1. linux内核启动相关逻辑

`vim arch/arm/kernel/head.S`

```s
# 检查内核是否支持当前处理器
bl      __lookup_processor_type
# 创建页表
bl      __create_page_tables
ldr     r13, =__mmap_switched
# 使能MMU
b       __enable_mmu
				                         
	__enable_mmu:
	....
	....
	b       __turn_mmu_on
				 
	ENTRY(__turn_mmu_on)
    # 正式开启了MMU功能 后续使用的地址就都是虚拟地址
    ...
    mov     r3, r13
    mov     pc, r3  # 跳转到__mmap_switched去执行
            
 	__mmap_switched:
    ...
    b       start_kernel	  # 后续就都是C程序			 
			
			
	start_kernel(){
		rest_init(){
			//创建内核线程 线程主体函数kernel_init
			kernel_thread(kernel_init, NULL, CLONE_FS | CLONE_SIGHAND);
		}
	}
			                    
	kernel_init(){
		prepare_namespace(){
			//挂载bootargs 指定的根文件系统
			mount_root();
		}
		init_post(){
			//execute_command,指向的就是  init=/linurc
			if (execute_command) { 
				//将 "/linuxrc" 作为用户空间的1号进程启动   execl
				run_init_process(execute_command);
			}
			//如果没有找到指定的程序，试图使用 /sbin/init程序作为1号进程启动
			run_init_process("/sbin/init");
			...
			//如果找到 内核恐慌 5s后重启
			panic("No init found.  Try passing init= option to kernel. ");
			...
		}
	}
```

2. 整个流程简述  
开发板上电--->执行uboot--->设置为SVC模式--->关看门狗--->使缓存数据无效--->禁止MMU--->清零BSS段--->一系列硬件初始化（系统时钟 uart  lcd i2c ...）  
--->run_main_loop--->倒数读秒计时--->执行bootcmd中记录的命令（通常就是加载启动内核）--->判断内核是否支持该CPU--->创建页表--->开启MMU(自此以后使用的都是虚拟地址)--->创建内核中0号进程  
--->加载指定的根文件系统--->启动用户空间1号进程--->1号进程会启动用户空间的其它进程--->开启一个shell进程--->用户可以输入命令	