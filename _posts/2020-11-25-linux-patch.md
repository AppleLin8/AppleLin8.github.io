---
title: linux patch
layout: post
categories: linux
date:   2020-11-25 16:44:52 +0800
tags: linux
excerpt: Make and apply patch on linux
---
--------------------
文章出自个人博客<https://applelin8.github.io/2020/11/25/linux-patch>，转载请申明

------------------
# Contents <span id="home">
* [What is patch?](#1)
    * [简介](#1.1) 
    * [patch文件格式](#1.2)
* [how to make patch](#2)
    * [diff命令](#2.1) 
    * [单文件补丁](#2.2)
    * [文件夹补丁](#2.3)
* [how to apply patch](#3)
    * [patch命令](#3.1) 
    * [应用](#3.2)

----------------------------

Introduce how to make and apply patch on linux?

# What is patch? <span id="1">


## 简介 <span id="1.1">


在linux下，修改了代码，为了方便分享（new feature）或者自己备份使用，一般需要制作一个补丁（patch）。

patch是一个文件两个版本之间的差异。

diff file.version1 file.version2 > file.patch

patch的作用是方便，组合灵活，体积小。

- 场景1

比如两个开发者A和B都有一project, 

现在A在project中增加了新featureA,

如果B要用featureA，就不要整个把A的project的拿过来，如果project很大，这个会很花费拷贝时间和存储空间。

只要制作 featureA.patch, 然后B把featureA.patch的差异打到自己的project，就可以跟A的project的一样使用freatureA了。

freatureA.patch比project的体积小多了，方便分享和备份。

- 场景2

如果同一project, 多个开发人员A、B、C,

它们分别开发了 feature_A 、feature_B 、feature_C，

现在开发人员D，它也有project，他的需求可以是多样的，

D会只使用feature_A，

也许D会使用feature_B和feature_C而不要feature_A。

方便使用者根据需要组合使用patch。

## patch文件格式 <span id="1.2">

补丁文件内容到底是什么样子的？

例子

```bash
[patch_demo] $ cat to-file.patch 
--- from-file	2020-11-25 17:47:49.335233371 +0800
+++ to-file	2020-11-25 17:48:39.955230582 +0800
@@ -1,5 +1,6 @@
+aaa
 000
 111
-222
+bbb
 333
 444
[patch_demo] $ 
```

**补丁头**

> 补丁头分别由---和+++开头的两行，用来表示要打补丁的文件名。
>
> ---开头表示旧文件，
>
> +++开头表示新文件

一个补丁文件中的多个补丁

> 一个补丁文件中可能包含以---和+++开头的很多节，每一节用来打一个补丁。所以一个patch文件中可以包含多个补丁。

块

> 块是补丁中要修改的地方。它通常由一部分不需要修改的内容开始和结束。他们只是表示用来修改的位置。他们通常以@@开始，结束于另一个块的开始或者一个新的补丁头。

块的缩进

> 块会缩进一列，并且这一列用来表示是要增加还是要删除的。

块的第一列

> +号表示这一行是要加上的。-号表示这一行是要删除的。没有加号（+）也没有减号(-)表示这里只是引用的并不需要修改。


# how to make patch? <span id="2">

## diff 命令 <span id="2.1">

制作补丁(patch)用到命令行比较工具 **diff** 。

diff 可以比较两个对象，并输出两者的区别。

diff 的用法：

```bash
diff [options] soure dest
```

**-r** 递归，比较目录下面（包含子目录）所有文件

**-N** 确保patch正确处理已经创建或删除文件的情况

**-u** 输出每个修改前后3行，也可以用-u5指定输出5行

**-E, -b, -w, -B, --strip-trailing-cr** 忽略各种空白，参考帮助，按需选用。

## 单文件补丁 <span id="2.2">

产生单文件补丁

```bash
diff -uN from-file to-file >to-file.patch
```

> 因为是单个文件，所以不需要 -r 选项。

例子：

```bash
[patch_demo] $ ls
from-file  to-file
[patch_demo] $ cat from-file 
000
111
222
333
444
[patch_demo] $ cat to-file 
aaa
000
111
bbb
333
444
[patch_demo] $ diff -uN from-file to-file > to-file.patch
```

得到如下补丁


```bash
[patch_demo] $ cat to-file.patch 
--- from-file	2020-11-25 17:47:49.335233371 +0800
+++ to-file	2020-11-25 17:48:39.955230582 +0800
@@ -1,5 +1,6 @@
+aaa
 000
 111
-222
+bbb
 333
 444
[patch_demo] $ 
```



## 文件夹补丁 <span id="2.3">

```bash
diff -uNr from-dir to-dir > to-dir.patch
```

例子

```bash
[dir] $ tree
.
├── from-dir
│   ├── a.txt
│   └── from.txt
└── to-dir
    ├── b.txt
    └── to.txt

2 directories, 4 files
[dir] $ cat from-dir/a.txt 
111
222
333111
[dir] $ cat from-dir/from.txt 
from
[dir] $ cat to-dir/b.txt 
aaa
b
c
[dir] $ cat to-dir/to.txt 
to
[dir] $ diff -uNr from-dir to-dir > to-dir.patch
```

得到如下补丁

```bash
[dir] $ cat to-dir.patch 
diff -uNr from-dir/a.txt to-dir/a.txt
--- from-dir/a.txt	2020-11-25 17:55:39.717207451 +0800
+++ to-dir/a.txt	1970-01-01 08:00:00.000000000 +0800
@@ -1,3 +0,0 @@
-111
-222
-333111
diff -uNr from-dir/b.txt to-dir/b.txt
--- from-dir/b.txt	1970-01-01 08:00:00.000000000 +0800
+++ to-dir/b.txt	2020-11-25 17:56:27.089204841 +0800
@@ -0,0 +1,3 @@
+aaa
+b
+c
diff -uNr from-dir/from.txt to-dir/from.txt
--- from-dir/from.txt	2020-11-25 17:56:07.124205941 +0800
+++ to-dir/from.txt	1970-01-01 08:00:00.000000000 +0800
@@ -1 +0,0 @@
-from
diff -uNr from-dir/to.txt to-dir/to.txt
--- from-dir/to.txt	1970-01-01 08:00:00.000000000 +0800
+++ to-dir/to.txt	2020-11-25 17:56:38.532204210 +0800
@@ -0,0 +1 @@
+to
[dir] $ 
```


# how to apply patch? <span id="3">



## patch命令 <span id="3.1">

patch的作用是将diff输出的结果(补丁)应用到对就文件(夹)上。最常见的用法是：

```bash
patch -pNUM <patchfile>
```

-p NUM

> 忽略几层文件夹，随后详解。

-E

> 这个选项作用是如果发现空文件，就删除。

-R

> 取消打过的补丁。它是打补丁动作的逆操作。

为了解释-p参数，需要看一下如下patch文件片段：

```bash
--- old/modules/demo       2020-11-25 17:56:07.124205941 +0800
+++ new/modules/demo       2020-11-25 17:56:38.532204210 +0800
```

如果使用参数-p0,就表示从当前目录找一个叫做old的文件夹，再在它下面找**modules/demo**文件来执行patch操作。

而如果使用参数-p1，就表示忽略第一层目录(即不管old),从当前目录寻找**modules**的文件夹，再在它下面找demo。

## 应用 <span id="3.2">

- 处理单个文件补丁的方法

```bash
# 产生补丁
diff -uN from-file to-file > to-file.patch

# 打补丁
patch -p0 < to-file.patch

# 取消补丁
patch -RE -p0 < to-file.patch
```

- 处理整个文件夹补丁的情况

```bash
# 产生补丁
diff -uNr  from-dir  to-dir  >to-dir.patch
 
# 打补丁
cd to-dir
patch -p1 < to-dir.patch
 
# 取消补丁
patch -R -p1 <to-dir.patch
```

