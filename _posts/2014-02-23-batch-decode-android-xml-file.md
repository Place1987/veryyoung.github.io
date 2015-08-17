---
layout: post
title: 批量反编译Android xml文件
date: 2014-02-23 13:33
author: VERYYOUNG
comments: true
categories: [Android]
---

android界面一般采用Xml编写,与图片资源结合

如果想"借鉴"别人的安卓界面,可以下载别人的apk
解压,然后图片资源可以找出来

xml文件也可以看到,不过都是二进制,需要反编译
可以使用如下办法进行反编译

1. 下载<a href="https://code.google.com/p/android4me/downloads/list" title="AXMLPrinter2.jar" target="_blank">AXMLPrinter2.jar</a>
2. 下载<a href="http://files.cnblogs.com/mengshu-lbq/BatchAXPrinter.BIN.zip" title="BatchAXPrinter.jar" target="_blank">BatchAXPrinter.BIN.zip</a> 下载之后解压,更改后缀为.jar
3. 在控制台进入到解压后apk的目录,输入java -jar BatchAXPrinter.jar AXMLPrinter2.jar ../res/layout/
其中 ../res/layout/是你要反编译的XML文件的根目录。即可完成批量反编译xml文件

再加上之前得到的图片资源,安卓界面"借鉴"成功!
