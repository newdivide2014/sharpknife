---
title: "编译Python3.9.7"
date: 2021-09-30T11:27:45+08:00
description: 编译python3.9.7无法打开libssl.so.47报错解决
# weight: 1
# aliases: ["/first"]
draft: false
author: "嘟囔"
# author: ["Me", "You"] # multiple authors
tags: ["python3.9.7",  “libssl.so.47”]
categories: ["python"]
---

源码编译个`python3.9.7`安装一下子，嘎嘎！（去python官网下载去）

```sh
tar -xvf Python-3.9.7.tgz
cd Python-3.9.7
./configure --prefix=/work/git/INSTALL/python3.9.7/ --enable-shared CFLAGS=-fPIC && make && make install 
# 指定安装目录为/work/git/INSTALL/python3.9/
```

然后报错了...

## 报错信息

```sh
*** WARNING: renaming "_hashlib" since importing it failed: libssl.so.47: cannot open shared object file: No such file or directory
```

## 编译openssl

查了一下，没安装`openssl`，那就装一下`openssl`

来这里 [openssl官网](https://www.openssl.org/source/) 下载一个。（我下载的是openssl-1.1.1f.tar.gz）

编译一下openssl

```sh
tar -xvf openssl-1.1.1f.tar.gz
cd openssl-1.1.1f
./config && make && make install # 编译完直接安装到系统路径
openssl version -a # 安装成功后执行可以看到openssl的版本信息了
```

重新编译一下python3.9.7，还是报同样的错误。额。。。还是说找不到`libssl.so.47`

查看了下python的编译配置，在`python3.9.7/Modules/Setup`

`vim Modules/Setup`找到`ssl`的相关配置，在214行原始文件的这些配置都是注释掉的需要改一下  

```sh
212 # Socket module helper for SSL support; you must comment out the other
213 # socket line above, and possibly edit the SSL variable:
214 SSL=/usr/local/ssl	# ssl的头文件位置
215 _ssl _ssl.c \
216         -DUSE_SSL -I$(SSL)/include -I$(SSL)/include/openssl \
217         # -L$(SSL)/lib -lssl -lcrypto  原始的是这样的，但是我安装的openssl的libssl.so.47在/user/local/lib下 
218         -L/user/local/lib -lssl -lcrypto
```

## 编译python3.9.7

然后再次编译`python3.9.7`

```sh
cd Python-3.9.7
./configure --prefix=/work/git/INSTALL/python3.9.7/ --enable-shared CFLAGS=-fPIC && make && make install
```

成功！哈哈

