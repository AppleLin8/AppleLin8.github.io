---

title: find by size
layout: post
categories: shell
date:   2020-12-16 7:30:08 +0800
tags: shell
excerpt: find file by size
---
--------------------
This article is from a personal blog <https://applelin8.github.io/2020/12/16/find-by-size>，Reprint please affirm

------------------


# content <span id="home">

* [highlight](#1)



----------------------------

# highlight <span id="1">

```bash
find [-H] [-L] [-P] [-Olevel] [-D help|tree|search|stat|rates|opt|exec|time] [path...] [expression]
```

查找当前目录下文件大小大于1M的文件

```bash
find ./ -type f -size +1M
```

查找当前目录下文件大小大于10M的文件,并显示它们的详细信息.

```bash
find . -size +10M -ls
```

搜索当前目录中，所有过去10分钟中更新过的普通文件。如果不加-type f参数，则搜索普通文件+特殊文件+目录。

```bash
 find . -type f -mmin -10
```

搜索当前目录中大于10M的文件,并显示详细信息.

```bash
find . -size +10M |xargs -I % ls -ahl %
```

