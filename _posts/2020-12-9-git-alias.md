---
title: git alias
layout: post
categories: git
date:   2020-12-9 12:06:28 +0800
tags: git
excerpt: git alias
---
--------------------
文章出自个人博客<https://applelin8.github.io/2020/12/9/git-alias>，转载请申明

------------------
git cp = git cherry-pick

it.

it's fine.

# content <span id="home">

* [git alias](#1)

----------------------------

# git-alias <span id="1">



```bash
[alias]
    co = checkout
    cob = checkout -b
    coo = !git fetch && git checkout
    br = branch
    brd = branch -d
    brD = branch -D
    merged = branch --merged
    st = status
    aa = add -A .
    cm = commit -m
    aacm = !git add -A . && git commit -m
    cp = cherry-pick
    amend = commit --amend -m
    dev = !git checkout dev && git pull origin dev 
    staging = !git checkout staging && git pull origin staging
    master = !git checkout master && git pull origin
    po = push origin
    pod = push origin dev 
    pos = push origin staging
    pom = push origin master
    poh = push origin HEAD
    pogm = !git push origin gh-pages && git checkout master && git pull origin master && git rebase gh-pages && git push origin master && git checkout gh-pages
    pomg = !git push origin master && git checkout gh-pages && git pull origin gh-pages && git rebase master && git push origin gh-pages && git checkout master
    plo = pull origin
    plod = pull origin dev 
    plos = pull origin staging
    plom = pull origin master
    ploh = pull origin HEAD
    unstage = reset --soft HEAD^
    ls = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]\\ %Creset%ad" --date=short  --decorate
    ll = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate --numstat
    f = "!git ls-files | grep -i" 
    gr = grep -Ii 
    la = "!git config -l | grep alias | cut -c 7-"
```




