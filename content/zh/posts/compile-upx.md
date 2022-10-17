---
title: "编译upx"
date: 2021-06-30T16:30:40+08:00
lastmod: 2022-06-30T17:39:20+08:00
draft: false
keywords: ["upx"]
description: "编译upx记录"
tags: ["upx"]
categories: ["upx"]
author: "嘟囔"


---

1. 源码下载
    
        git clone https://github.com/upx/upx.git
        cd upx
        git submodule init && git submodule update

下载UCL库。UCL是使用ANSI C编写的NRV（Not Really Vanished）算法。 具体介绍http://www.oberhumer.com/opensource/ucl/

        wget http://www.oberhumer.com/opensource/ucl/download/ucl-1.03.tar.gz
        tar -xvf ucl-1.03.tar.gz
        cd ucl-1.03
        ./configure --prefix=/work/bao/ucl/bin CC=clang

注意：指定C编译器为clang。是因为gcc的一个bug，导致 ACC一致性测试失败，所以使用clang。
gcc出现的错误情况FTBFS with GCC 6: compiler failed the ACC conformance test有详细描述。https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=811707

1. 编译UPX

        cd upx
        make all UPX_UCLDIR=/work/bao/ucl-1.03 UPX_LZMADIR=./src/lzma-sdk

编译完了在upx/src/下可以看到`upx.out`程序已生成。