---
title: "Linux根据用户名得到uid"
date: 2022-03-26T10:35:18+08:00
description: uid获取函数
# weight: 1
# aliases: ["/first"]
draft: false
author: "嘟囔"
# author: ["Me", "You"] # multiple authors
tags: ["uid"]
categories: ["Linux"]
---

### 头文件

```c
#include <pwd.h>
#include <sys/types.h>
```

### 函数
```c
struct passwd * getpwuid (uid_t uid);
```
该函数用来获取指定用户id的用户详细信息，其结果保存函数返回的结构struct passwd中。
```c
struct passwd * getpwnam (const char *name) 
```
该函数的作用于getpwuid类似，不过该函数时根据用户的登录名获取用户的详细信息。

结构`struct passwd`有以下变量：
```c
char *pw_name
//用户登录名
char *pw_passwd.
//加密的密码
uid_t pw_uid
//用户id
gid_t pw_gid
//用户组ID
char *pw_gecos
//用户实际姓名.
char *pw_dir
//用户home目录，或者初始工作目录
char *pw_shell
//用户默认shell
```

### 示例
```c
#include <pwd.h>
#include <sys/types.h>
#include <stdio.h>
int main(void)
{
    struct passwd *user;
    user=getpwnam("root");
    printf("root uid:%d\n", user->pw_uid);
    return 0;
}
```