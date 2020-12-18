---
title: pc of two net
layout: post
categories: net
date:   2020-12-7 12:06:28 +0800
tags: net
excerpt: two net ping
---
--------------------
文章出自个人博客，转载请申明

------------------
# content <span id="home">
* [question](#1)
* [windows](#2)
* [linux](#3)

----------------------------

# question <span id="1">

机器有两个网卡，一个是有线，另一个是无线。

pc1 ping  pc2 有线不通。

```bash
ping 192.168.1.3
```



![net](https://AppleLin8.github.io/assets/img/blog/it/2net_wifi_and_wire.png)

# windows <span id="2">
```bash
route PRINT -4
===========================================================================
接口列表
4...66 66 66 66 66 66 ......Realtek PCIe GBE Family Controller
5...88 88 88 88 88 88 ......Qualcomm Atheros QCA9377 Wireless Network Adapter
===========================================================================

IPv4 路由表
===========================================================================
活动路由:
网络目标        网络掩码          网关       接口         跃点数
0.0.0.0       0.0.0.0  10.61.40.254   10.61.40.174    10
0.0.0.0       0.0.0.0  192.168.1.1    192.168.1.152   25
===========================================================================
永久路由:
  无
```
因为pc1的route设置无线的default route的跃点比有线的高，
且没有192.168.1.3的路由，所以pc1 ping pc2的有线网卡不通。

增加路由：

```bash
#添加路由
route add 192.168.1.3 MASK 255.255.255.255  192.168.1.254 metric 30 if 4
#修改gateway和metric
route change 192.168.1.3 MASK 255.255.255.255  192.168.1.254 metric 5 if 4
```

设置规则(metric 越小，优先级越高)：

```bash
(192.168.1.3的metric) < (default 0.0.0.0  192.168.1.1) < (default 0.0.0.0 10.10.1.1)
```



# linux <span id="3">

have nice day
```bash
# show route
ip r
route -n

# add route
route -p add 192.168.1.2 255.255.255.0 192.168.1.3

# ip route
ip route add default via 192.168.1.1 table 1
ip route add 192.168.0.0/24 via 192.168.1.2 table 1
#注:各路由表中应当指明默认路由,尽量不回查路由表.路由添加完毕,即可在路由规则中应用..

ip route add 192.168.1.0/24 dev eth0 via 192.168.1.66 realm 4

```


