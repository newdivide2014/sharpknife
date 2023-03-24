---
title: "strcasestr函数"
date: 2022-08-26T11:16:08+08:00
description:
# weight: 1
# aliases: ["/first"]
draft: false
author: "嘟囔"
# author: ["Me", "You"] # multiple authors
tags: ["strcasestr"]
categories: ["linux"]
---



```c
#define _GNU_SOURCE
#include <string.h>

char *strcasestr(const char *haystack, const char *needle);

// 如果在编程时没有定义"_GNU_SOURCE"宏，则编译的时候会有警告信息
// warning: initialization makes pointer from integer without a cast
// strcasestr函数并非是标准C库函数，是扩展函数。函数在调用之前未经声明的默认返回int型
```

strcasestr函数的功能、使用方法与strstr基本一致。 
strcasestr函数在"子串"与"父串"进行比较的时候，"不区分大小写"

demo
```c
#define _GNU_SOURCE
#include <stdio.h>
#include <string.h>
int main(int argc, char **argv)
{
    char *str = strcasestr("AbCedhHelloWordjaksGF", "helloword");
    if(str == NULL) 
        printf("str is NULL\n");
    else 
        printf("%s\n", str);     // str:HelloWordjaksGF
    return 0;
}
```