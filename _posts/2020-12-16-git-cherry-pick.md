---

title: git cherry-pick
layout: post
categories: git
date:   2020-12-16 8:30:38 +0800
tags: git
excerpt: git cherry-pick
---
--------------------
This article is from a personal blog <https://applelin8.github.io/2020/12/16/git-cherry-pick>，Reprint please affirm

------------------


# content <span id="home">

* [highlight](#1)
* [example](#2)



----------------------------

# highlight <span id="1">

创建一个新分支,

```bash
#基于当前分支创建新分支
git checkout -b <new-branch-name>
#基于历史commit id创建分支
git checkout -b <new-branch-name> <SHA1>
```

checkout之前的一个commit并开一个branch指向它了.

在Git中创建分支，是必须有一个父节点的.默认是HEAd节点.
git 场景 ：从一个分支cherry-pick多个commit

# example <span id="2">

## 场景：

在branch1开发，进行多个提交，这时切换到branch2，想把之前branch1分支提交的commit都【复制】过来，怎么办？

## 创建分支branch2 <span id="2.1">
查看所有分支

```bash
$ git branch -a
* branch1
  remotes/origin/HEAD -> origin/branch1
  remotes/origin/branch1
  remotes/origin/branch2
```
创建分支

```bash
## 切换分支 <span id="2.2">
git checkout remotes/origin/branch2

#创建新分支
git checkout -b branch2
```

查看分支

```bash
$ git branch -a
* branch2
  branch1
  remotes/origin/HEAD -> origin/branch1
  remotes/origin/branch1
  remotes/origin/branch2
```


## 首先切换到分支 branch1, 然后查看提交历史记录 <span id="2.3">

```bash
# 切换分支
$ git checkout branch1
$ git branch 
* branch1
  branch2

```


git log

```bash
$find . -size +100M |grep -v git|xargs -I % ls -sh %
2.9G ./out/apple.iso
816M ./apple.tar

$ git  log --oneline  ./apple.tar
02a7492 add apple
$ git  log --oneline  ./out/apple.iso
8c3c7e0 apple iso
$ git log --oneline > log_sha.txt
```

## 切换到分支branch2 <span id="2.4">

```bash
git checkout branch2

```

## 复制指定提交 <span id="2.5">

cherry-pick用法

```bash
#复制单个commit
git cherry-pick <commitHash>
#复制多个commit
git cherry-pick <commitA_Hash> <commitB_Hash>
#复制多个连续commit 注意，不包含第一个commit0_Hash ， 即  git cherry-pick (commit0_Hash..commit100_Hash]
git cherry-pick <commit0_Hash>..<commit100_Hash>
#包含第一个commit0_Hash方法
git cherry-pick <commit0_Hash>^..<commit100_Hash>
```

用git cherry-pick复制

```bash
git cherry-pick 5396bf8^..8c3c7e0
rm -rf ./out/apple.iso
git add -u
git status
git commit --amend
git log --oneline

```

## demo <span id="2.6">

```bash
#!/bin/bash
#set -vx
from=$1
to=$2
SCRIPT_PATH=$(readlink -f $(dirname $0))
file=${SCRIPT_PATH}/hash_git_log.txt
GIT_PATH=${SCRIPT_PATH}/demo

check_ret()
{
    ret=$?
    if [ $ret -ne 0 ]
    then
        echo [error] ret = $ret
        exit -1
    fi
}

is_stop_hash()
{
    hash=$1

    if [ "$hash" == "8c3c7e0" ]
    then
        echo [error] exit: 8c3c7e0
        exit
    fi
}

get_line_no()
{
    hash=$1
    ret=`awk '/'$hash'/{print NR}' $file`
    echo $ret
}

get_hash()
{
    line=$1
    hash=`echo $line|awk '{print $1}'`
    echo $hash
}

show_hash_line_no()
{
    hash=$1
    number=`get_line_no $hash`
    echo [info] $number : $hash
}

parse_line()
{
    line=$1
    hash=`echo $line|awk '{print $1}'`

    #discard "add linux 4.20 kernel"
    if [[ $line =~ "add linux 4.20 kernel" ]]
    then
        echo [warn] $line
        return
    fi

    show_hash_line_no $hash
    is_stop_hash $hash

    if [[ $line =~ "Merge" ]]
    then
        echo git cherry-pick -m 1 $hash
        git cherry-pick -m 1 $hash
        if [ $? -ne 0 ]
        then
            git reset --hard
            git clean -df
        fi
    else
        echo git cherry-pick $hash
        git cherry-pick $hash
        check_ret
    fi
}

read_file()
{
    number_from=`get_line_no $from`
    number_to=`get_line_no $to`
    sed -n ''$number_from','$number_to''p $file|while read line
    do
        echo ------------------------
        parse_line "$line"
    done
}

main()
{
    cd $GIT_PATH
    read_file
}

main

```

