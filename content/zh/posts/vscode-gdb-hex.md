---
title: "VScode GDB调试 16进制查看内存和表达式"
date: 2022-08-26T11:16:08+08:00
description: 调试技巧
# weight: 1
# aliases: ["/first"]
draft: false
author: "嘟囔"
# author: ["Me", "You"] # multiple authors
tags: ["VScode GDB"]
categories: ["GDB"]
---

### VScode监视窗口16进制查看表达式，只需要在表达式后面加`,h`， 
比如： `buf,h`，则按16进制显示buf的值

### 查看内存 
使用`gdb`的`x`命令查看内存，在调试控制台或者监视窗口执行： `-exec x/20xb buf`

### 关于gdb的x指令 
`x/<n><f> <addr>` 
`<n>`是一个数字，表示要查看几个内存单元，内存单元在后面定义。 
`<f>`表示显示的形式，对于整数变量来说取值有： 
    `x` 十六进制格式显示变量 
    `d`	十进制格式显示变量 
    `u`	按十六进制格式显示无符号整型 
    `o`	按八进制格式显示变量 
    `t`	按二进制格式显示变量 
    `a`	按十六进制格式显示变量 
    `c`	按字符格式显示变量 
    `f`	按浮点数格式显示变量 
    `s` 表示按字符串显示 
    `u` 指一个内存单元的大小，取值包括：
        b=1 byte 
        h=2 bytes 
        w=4 bytes 
        g=8 bytes
        默认是4bytes

例如：`-exec x/24xb buf` 
就是按16进制显示buf开头的24个内存单元，每个内存单元的大小是1字。