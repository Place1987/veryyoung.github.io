---
layout: post
title: Travis CI：新一带持续集成工具
date: 2015-12-28 23:06:11
author: VERYYOUNG
comments: true
categories: [Linux]
---

[Travis CI](https://travis-ci.org/)  是一个在线的，分布式的持续集成服务，用来构建及测试在 GitHub 托管的代码。


<!-- more -->

----------

Travis 是非常简单，不像 Jenkins 可以允许无限多的插件、有无数个工作任务创建和复杂的流程等等，不需要写很复杂的脚本。

Travis 大多数时候无需显式定义流程，举例，如果有 build.gradle 文件, Travis 会理解它并使用 Gradle 编译它，测试等等。

它会侦查你的代码并采取相应动作，如果从 Ant 切换到 Maven 再到 Gradle，无需对 Travis 或其配置做任何改变。

Travis 基于一个简单文件.travis.ylm，它驻留在你的代码根目录，即使这个配置文件变得复杂，大部分情况下 Travis 总是假设我们根据标准来实行，因为标准和简单意味着更好更有效的设计。

使用 Travis，会让你忘记 CI 的存在. 无论什么时候将代码提交到仓库， Travis 会发现并采取相应代码改变(包括 .travis.ylm). 如果有问题，你会收到 Email 通知。


如果想做复杂的操作，也可以！

来看个 .travis.ylm 的例子（来自开源项目 [ES](https://github.com/zhangkaitao/es)）

	language: java
	
	env:
	- DB=mysql
	
	jdk:
	- openjdk7
	
	mysql:
	database: es
	username: root
	password :
	encoding: utf8
	
	install:
	- mvn install -Dmaven.test.skip=true
	
	before_script:
	- cd web
	- mvn clean
	- mvn db:create
	- mvn db:schema
	- mvn db:data
	- cd ..
	
	script:
	- cd common
	- mvn test
	- cd ..
	- cd web
	- mvn test -Pit
	
	
	
	notifications:
	email:
		- zhangkaitao0503@gmail.com
		

一套流程走下来，每一句都很直白，一目了然！


可以在网页上看到构建历史

![](http://veryyoung.u.qiniudn.com/20151206211547.png)

以及构建详情

![](http://veryyoung.u.qiniudn.com/20151105203213.png)

详情包括对应的 commit 记录，以及详细的 构建 log (包括执行的每一条命令，以及命令执行之后的反应)。

Travis 是基于 Vagrant 来管理环境的，用虚拟化技术的云化方案做成了云 CI。


-----


使用现状：目前大部分用于 GitHub 的开源项目的构建，很多知名的开源项目使用它来在每次提交的时候进行构建测试，比如 PHP、Ruby on Rails，Ruby 和 Node.js。

还没法用在非 GitHub 的项目上，不过 Travis CI 已经试图将这一成功的开源项目在企业层面复制，名字也想好了：Travis Pro。








