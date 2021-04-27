---
title: "Linux tar备忘"
date: 2021-04-11T20:12:03+08:00
lastmod: 2021-04-11T20:12:03+08:00
draft: false
keywords: ["linux cmd"]
tags: ["linux cmd"]
categories: ["linux cmd"]
author: "嘟囔"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: true
toc: true
autoCollapseToc: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
# contentCopyright: true
reward: false
mathjax: false
---



![dog](/images/post/DSC_0803.JPG)
<!--more-->
献上狗子~嘻嘻

将 /etc/ 内的所有档案备份下来，并且保存其权限！

    [root@linux ~]# tar -czvpf /tmp/etc.tar.gz /etc
    
这个-p的属性是很重要的，尤其是当您要保留原本档案的属性时！
