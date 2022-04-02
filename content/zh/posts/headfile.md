---
title: "常用函数头文件"
date: 2022-03-24T11:29:03+08:00
description:
# weight: 1
# aliases: ["/first"]
draft: false
author: "嘟囔"
# author: ["Me", "You"] # multiple authors
tags: ["头文件"]
categories: ["Linux"]
---

总是忘记一些函数的头文件，还得百度查。写个文记录下方便自己`ctrl+f`查找。

```c
#include<sys/stat.h>
//修改文件权限
int chmod(const char * path,mode_t mode);
//对已打开的文件进行修改权限
int fchmod(int fd, mode_t mode);
```

```c++
#include <regex>
//c++正则 C++03之前不支持
std::regex
```