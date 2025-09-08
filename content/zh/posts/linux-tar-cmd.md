---
title: "Linux tar备忘"
date: 2021-04-11T20:12:03+08:00
lastmod: 2021-04-11T20:12:03+08:00
draft: false
keywords: ["linux cmd"]
tags: ["linux cmd"]
categories: ["linux cmd"]
author: "嘟囔"
authorEmoji: 👺
# cover:
#     image: "/images/posts/DSC_0803.JPG"
#     # can also paste direct link from external site
#     # ex. https://i.ibb.co/K0HVPBd/paper-mod-profilemode.png
#     alt: "<alt text>"
#     caption: "俺家狗子"
#     relative: false # To use relative path for cover image, used in hugo Page-bundles

---

将 /etc/ 内的所有档案备份下来，并且保存其权限！

    [root@linux ~]# tar -czvpf /tmp/etc.tar.gz /etc
    
这个-p的属性是很重要的，尤其是当您要保留原本档案的属性时！
