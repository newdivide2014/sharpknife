---
title: "svn Can't convert string from 'UTF-8' to native encoding"
date: 2021-08-27T09:26:40+08:00
description: svn报错解决
# weight: 1
# aliases: ["/first"]
draft: false
author: "嘟囔"
# author: ["Me", "You"] # multiple authors
tags: ["svn error"]
categories: ["svn"]
---

操作`svn checkout`代码的时候报错了。  
`svn: Can't convert string from 'UTF-8' to native encoding`  
无法把utf-8编码转化成本地编码。因为代码里有word文档，可能就是中文的问题了。

查看一下`locale`
```sh
[root@localhost src]: locale
LANG=en_US.UTF-8
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=
```

解决办法就是把环境变量`LC_ALL`设置一下
```sh
export LC_ALL=zh_CN.UTF-8
```

`