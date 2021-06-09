---
title: "数据结构--树🌲"
date: 2021-05-26T00:24:44+08:00
description: 🌲的知识点学习
# weight: 1
# aliases: ["/first"]
draft: true
author: "嘟囔"
# author: ["Me", "You"] # multiple authors
enableTOC: true
tags: ["tree"]
categories: ["数据结构"]
---
## 树

### 基本概念
树是由n（n>= 0）个结点组成的有限集合。
度：一个结点包含子树的数目，称为该结点的度。
树叶（叶子）：度为0的结点，称为叶子结点或树叶，也叫终端结点。
兄弟结点：具有同一个双亲的结点，称为兄弟结点
树的度：树中结点度的最大值称为树的度。（唯一性）
树的层数：根结点的层数为1，其他结点的层数为从根结点到该结点所经历的分支数目再加1。（唯一性）
树的高度（深度）：树中结点所处的最大层数称为树的高度。
森林：若干颗互不相交的树组成的集合为森林。

树的表示方法：
1. 树形结构表示法
2. 凹入法表示法
3. 嵌套集合表示法
4. 广义表表示法

---

### 二叉树的基本概念和逻辑结构
特点：  
1. 每个结点的度 $\leq2$；   
2. 是有序树；    
二叉树的每个结点最多存在2个孩子。
形态：有5种(空集，仅有根，根+左，根+右，根+左+右)  

**性质：**  
1. 若二叉树的层次从1开始，则在二叉树的第i层最多有$2^{i-1}$个结点。（$i\geq1$）（数学归纳法证明）
2. 深度为k的二叉树最多有$2^k-1$个结点。（$k\geq1$）
3. 对任意一颗二叉树，如果叶子结点个数为n0，度为2的结点个数为n2，则$n0=n2+1$。
4. 具有n个结点的完全二叉树的深度为$\lfloor\log_2n\rfloor\+1$。（向下取整）  
证明：设完全二叉树的深度为k，则有  
$2^{k-1}-1 < n \leq 2^k-1$  
$2^{k-1}\leq n<2^k$  
取对数$k-1\leq log_2n<k$  
因为k为整数，所以$k=\lfloor\log_2n\rfloor\+1$。证毕。
5. 编号规则。(自顶向下，自左向右依此编号)

两类特殊二叉树：
1. 满二叉树。如果编号是连续的（性质5），则是满二叉树。
2. 完全二叉树  
满二叉树一定是完全二叉树，但是完全二叉树不一定是满二叉树。

### 二叉树的存储结构
1. 顺序存储（数组表示）  
简单但是会造成空间上的浪费。  
适合满二叉树或者是二叉树用顺序存储好。  
2. 链式存储  

### 遍历二叉树
遍历次序（6+1）：  
1. 先序（先访问根再访问左子树，然后右子树）  
2. 中序（左根右）
3. 后序（左右根）

### 线索二叉树

1. 为什么二叉树中加入线索？  

   原来的左、右孩子域有许多空指针没有利用起来，为了不浪费存储空间，利用原有孩子指针为空时存放直接前驱和后继，这样的指针成为“线索”，加线索的过程称为线索化。加了线索的二叉树，称为线索二叉树，对应的二叉树链表称为线索二叉链表。
2. 怎么加
3. 如何区分孩子和前驱后继

线索二叉树的分类：  
1. 前序
2. 中序
3. 后序

线索二叉树链式存储  
每个结点5个域，但其中只有2个指针

### 哈夫曼树及其应用
1. 路径长度：俩个结点的路径上的分支数  
2. 树的路径长度：各结点到根结点的路径长度之和。  
3. 结点的带权路径长度：从根结点到该结点之间的路径长度与该结点的权的乘积。  
4. 树的带权路径长度（wpl）:所有叶子结点的带权路径长度之和。  
5. 哈夫曼树：wpl最小的二叉树称为哈夫曼树（最优二叉树），在哈夫曼树中，权值大的结点离根最近。  
6. 哈夫曼树的构造：    
7. 应用：数据压缩编码
8. 是一种无前缀编码，解码时不会混淆。  

### 二叉树、树和森林的转换

树的表示法
1. 双亲表示法  
2. 孩子表示法
   一个结点所有孩子链接成一个单链表形。
3. 双亲孩子表示
4. 孩子兄弟表示法
   第一根链指向第一个孩子，第二根链指向下一个兄弟。（左指针指孩子，右指针指兄弟）

树转换为二叉树
1. 连线：相邻兄弟之间连线。
2. 抹线：抹掉双亲与除左孩子外其他孩子之间的连线。
3. 旋线：将树作适当的旋转。

森林转换成二叉树
1. 将森林中每一颗树分别转换成二叉树
2. 合并：使第n颗树接入到第n-1颗的右边并成为它的右子树，依次连接，直到最后剩下一颗二叉树为止。

二叉树还原成树或森林
1. 右链断开
2. 二叉树还原成树

树和森林的遍历  
一个结点可能有两颗以上的子树，所以不宜讨论它们的中序遍历，即树和森林只有先序遍历和后序遍历
1. 先序遍历
2. 后序遍历

*树和森林的先序遍历等价于它转换成的二叉树的先序遍历，树和森林的后序遍历等价于它转换成的二叉树的* **中序遍历**。

>p29