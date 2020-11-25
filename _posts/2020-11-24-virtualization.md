---
title: virtualization
layout: post
categories: IT
date:   2020-11-24 20:59:49 +0800
tags: IT
excerpt: virtualization concept 
---
--------------------
文章出自个人博客<https://applelin8.github.io/2020/11/24/virtualization>，转载请申明

------------------
# content <span id="home">
* [virtualization](#1)
	* [synopsis](#1.1)
	* [glossary](#1.2)



----------------------------




# virtualization <span id="1">

## synopsis <span id="1.1">

虚拟化技术的含义很广泛。
**将任何一种形式的资源抽象成另一种形式的技术都是虚拟化。**
在常用的操作系统中就存在某种意义上的“虚拟化技术”，例如虚拟内存空间和进程。

系统虚拟化是一门跨领域的学科，涉及操作系统、编译和体系结构等学科知识，并延展到资源管理、性能和系统安全等问题。

虚拟化技术分类。

典型系统级虚拟化的技术以及VMM的组成和分类。

基于软件的完全虚拟化技术。

硬件辅助的完全虚拟化技术。

类虚拟化技术的实现原理。

虚拟机的性能评测和调试技术。

系统虚拟化的应用实例。

对虚拟机和系统虚拟化技术的发展作一个展望。

![hello world](https://AppleLin8.github.io/assets/img/blog/it/system_abstruct_layer.png)

## glossary <span id="1.2">

- Host

  在虚拟化中，物理资源通常有一个定语称为宿主(Host)。

  Host Machine

  Host OS

- Guest

  虚拟出来的资源通常有一个定语称为客户（Guest）。
  
  Guest Machine
  
  Guest OS
  
- 硬件抽象层上的虚拟化

  通常来说，宿主机和客户机的ISA（Instruction Set Architecture，指令集架构）是相同的,客户机的大部分指令可以在宿主处理器上直接运行。只有那些需要虚拟化的指令才会由虚拟化软件进行处理，

- 操作系统层上的虚拟化

  操作系统层上的虚拟化是指操作系统的内核可以提供多个互相隔离的用户态实例。这些用户态实例（经常被称为容器）对于它的用户来说就像是一台真实的计算机，有自己独立的文件系统、网络、系统设置和库函数等。从某种意义上说，这种技术可以被认为是UNIX系统chroot命令的一种延伸。因为这是操作系统内核主动提供的虚拟化，因此操作系统层上的虚拟化通常非常高效，它的虚拟化资源和性能开销非常小，也不需要有硬件的特殊支持。但它的灵活性相对较小，每个容器中的操作系统通常必须是同一种操作系统。另外，操作系统层上的虚拟化虽然为用户态实例间提供了比较强的隔离性，但其粒度是比较粗的。因为操作系统层上虚拟化的高效性，它被大量应用在虚拟主机服务环境中。比较有名的操作系统级虚拟化解决方案有Paralles的Virtuozo，Solaris的Zone和Linux的VServer等。

