---
title: "Linux命令备忘"
date: 2021-04-11T20:12:03+08:00
lastmod: 2021-04-11T20:12:03+08:00
draft: false
keywords: ["linux cmd"]
tags: ["linux cmd"]
categories: ["Linux"]
author: "嘟囔"
authorEmoji: 👺
cover:
    image: "/images/post/DSC_0803.JPG"
    # can also paste direct link from external site
    # ex. https://i.ibb.co/K0HVPBd/paper-mod-profilemode.png
    alt: "<alt text>"
    caption: "俺家狗子"
    relative: false # To use relative path for cover image, used in hugo Page-bundles

---

### tar

将 /etc/ 内的所有档案备份下来，并且保存其权限！

    [root@linux ~]# tar -czvpf /tmp/etc.tar.gz /etc
    
这个-p的属性是很重要的，尤其是当您要保留原本档案的属性时！
![🐶](/images/posts/DSC_0811.JPG)


### find

找到全局可写文件（word-writable file）
```sh
find / -xdev -type f \( -perm -0002 -a ! -perm -1000 \) -print
# -type f 表示找文件
# -type d 表示找目录
# -type l 表示找链接文件
```