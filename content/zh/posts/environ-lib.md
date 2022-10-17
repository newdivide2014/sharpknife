---
title: "environ环境变量表 & 库"
date: 2021-06-29T23:22:47+08:00
description: environ环境变量表和库相关的一些
# weight: 1
# aliases: ["/first"]
draft: false
author: "嘟囔"
# author: ["Me", "You"] # multiple authors
tags: ["environ"]
categories: ["Linux"]
---
## 简介

环境变量表就是一个以`NULL`指针结束的***字符指针数组***。  
其中每个元素都是一个字符指针，指向一个以空字符结尾的字符串，  
该字符串就是形如“键 = 值”形式的环境变量。  
该指针数组的地址保存在全局变量`environ`中。

```c
// 通过全局环境变量指针访问所有环境变量
extern char** environ;

char** p;
for(p = environ; p && *p; ++p) 
{
    printf("%s\n", *p);
}
```

`main`汉书的第三个参数就是环境变量表的起始地址。
```c
int main(int argc, char** argv, char* envp[])
{
    extern char** environ;
    printf("%p, %p\n", environ, envp); // 相等
    char* p = NULL;
    for(p = envpl p && *p; ++p) 
    {
        printf("%s\n", *p);
    }
    return 0;
}
```
## 相关函数

```c
#include <stdlib.h>
/* 功能：根据环境变量名称获取其值
*  参数： name 指针 环境变量名称字符串
*  返回值： 成功返回对应的环境变量的值，失败返回NULL
*/
char* getenv(const char* name);

/* 功能：添加或修改一个环境变量，不存在则添加，存在则修改
*  参数： string 是一个形如“键=值”的字符串
*  返回值： 成功返回0，失败返回非0
*/
int putenv(char* string);

/* 参数： overwrite 如果环境变量存在，传0，保持原值不变，传非0，表示替换以前的值
*/
int setenv(const char* name, const char* value, int overwrite);

int unsetenv(const char* name);  // 删除环境变量

int clearenv(void); // 清理环境变量
```

## 库

### 静态库
```sh
ar [选项] <静态库文件> <目标文件列表>
    -r 将目标插入到静态库中，已存在则更新
    -q 将目标文件追加到景泰款尾
    -d 从静态库中删除目标文件
    -t 列表显示静态库中的目标文件
    -x 将静态库展开为目标文件
例子：
# 打包math库 calc是计算模块 show是展示结果模块
ar -r libmath.a calc.o show.o
```

### 动态库
```sh
# 1. 编译成目标文件
gcc -c -fpic calc.c 
gcc -c -fpic show,c
# 2. 打包成动态库
gcc -shared calc.o show.o -o libmath.so

# 编译链接也可以合并为一步完成
gcc -shared -fpic calc.c show.c -o libmath.something
```

`PIC`(Position Independent Code, 位置无关代码)  
`-fPIC`： 大模式，生成的代码比较大，运行速度比较慢，所有平台都支持。
`-fpic`： 小模式，生成的代码比较小，运行速度比较快，仅部分平台支持。

#### 动态库的动态加载
在程序中动态加载共享库需要调用一组特殊的函数，这组函数在一个独立的库中予以实现。

需要包含此头文件，并链接此库
```c
#include <dlfcn.h>
-ldl

// 将共享库载入内存并获得其访问句柄
void* dlopen(cha const* filename, int flag);
// filename 动态可路径
// flag RTLD_LAZY 延迟加载 使用到库李的符号时才真的加载进内存
//      RTLD_NOW  立即加载

// 从已被加载的动态库中获取特定名称的符号地址
void* dlsym(void* handle, char const* symbol);

// 从内存中卸载动态库
int dlclose(void* handle);
//所卸载的动态库未必真的从内存中立即消失，可能其他的程序也在用
//只有所有使用该库的程序都显式或者隐式的卸载了该库，才能真正的释放了这块内存
//无论所卸载的动态库是否真正被释放，传递给dlclose函数的句柄都会在该函数成功返回后立即失效

//获取加载、使用、卸载过程中发生的错误
char* dlerror(void);

//demo
void *handle = dlopen("libmath.so", RTLD_NOW);
if(!handle) 
{
    fprintf(stderr, "dlopen: %s\n", dlerror());
    exit(EXIT_FAILURE);
}

int (*add)(int, int) = (int (*)(int, int))dlsym(handle, "add");
if(!add) 
{
    fprintf(stderr, "get add function address failed!\n");
    exit(EXIT_FAILURE);
}
int sum = add(1, 2);
```

#### 辅助工具
查看符号表： `nm`  
列出目标文件、可执行程序、静\动态库中的符号。

查看依赖： `ldd`  
查看可执行文件或者共享库多依赖的共享库。
