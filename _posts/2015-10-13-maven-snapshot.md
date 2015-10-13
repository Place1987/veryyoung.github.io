---
layout: post
title: Maven SNAPSHOT
date: 2015-10-13 20:12:27
author: VERYYOUNG
comments: true
categories: [Java]
---

在使用 Maven 的时候，经常遇到有些项目不稳定，在持续的开发中，有时候做了修改，提交到远程仓库，结果一起工作的小伙伴没接收到更新。

难道只能每次改完都把 ~/.m2 里面的 jar 包 copy 给他？

有木有优雅点的方式？

<!-- more -->

----------

这时候该 SNAPSHOT 派上用场啦！


顾名思义， SNAPSHOT 是快照，那什么是快照呢？

Maven 版本分两种：稳定(release)版和快照(SNAPSHOT)版。


Maven 会根据模块的版本号(pom 文件中的 version)中是否带有 “-SNAPSHOT" 来判断是否为 SNAPSHOT 版本。

如果是,在 mvn deploy 时会自动发布到 nexus 上去。

而使用	SNAPSHOT 的模块，在不更改版本号的情况下，直接编译打包时，maven 会自动从 nexus 服务器上下载最新的 jar 包。

如果是正式发布版本，那么在 mvn deploy 时会自动发布到正式版本库中，而使用正式版本的模块，在不更改版本号的情况下，编译打包时如果本地已经存在该版本的模块则不会主动去 nexus 上下载。

所以，我们在开发阶段，可以将公用库的版本设置为 SNAPSHOT，而被依赖组件则引用快照版本进行开发，在公用库的快照版本更新后，我们也不需要修改pom文件提示版本号来下载新的版本，直接 mvn 执行相关编译、打包命令即可重新下载最新的快照库了。