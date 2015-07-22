---
layout: post
title: 64位Ubuntu系统安装32位兼容库
date: 2014-05-21 17:47
author: VERYYOUNG
comments: true
categories: [Linux]
---
最近狠狠心把电脑换成ubuntu了，但是真心有点离不开QQ，于是准备WINE
WINE QQ只支持32 位

在64位ubuntu系统上运行32位程序需要安装32位lib


        可以用以下命令来安装：  

         sudo apt-get install ia32-libs

         64位Ubuntu系统安装32位兼容库 ，如果是刚安装的系统一定要先


         sudo apt-get update

         sudo apt-get upgrade


         再执行 sudo apt-get install ia32-libs 

如果出现:

正在读取软件包列表... 完成
正在分析软件包的依赖关系树       
正在读取状态信息... 完成       
现在没有可用的软件包 ia32-libs，但是它被其它的软件包引用了。
这可能意味着这个缺失的软件包可能已被废弃，
或者只能在其他发布源中找到
可是下列软件包取代了它：
  lib32z1 lib32ncurses5 lib32bz2-1.0

E: 软件包 ia32-libs 没有可供安装的候选者

运行以下命令即可：
sudo apt-get install g++-multilib
