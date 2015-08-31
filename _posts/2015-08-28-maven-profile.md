---
layout: post
title: maven profile分环境打包
date: 2015-8-28 21:10:28
author: VERYYOUNG
comments: true
categories: [Java]
---

用maven管理的程序一般是在本地开发完，上传到版本控制工具，在服务器上更新代码，然后执行

	maven install

但是有些配置文件需要进行改动，如jdbc数据源配置、log日志级别、redis server、jdk版本等。

在线上服务器上去vi是一件特别麻烦的事情。

maven提供了配置文件管理方案：[maven profile](http://maven.apache.org/guides/introduction/introduction-to-profiles.html)。

maven profile可以根据情况去读取不同的配置，来实现配置管理的功能。

加入有 dev、qa、product 三种类别的配置文件，需要在resource目录新建这三个文件夹，分别放入配置文件。

然后在pom.xml中增加配置。

在本地环境中要激活dev，可以

	mvn package –P dev

同理线上执行

	mvn package –P product  

常用的IDE也都有选择profile的方法。








