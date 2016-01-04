---
layout: post
title: Gradle：新一代构建工具
date: 2016-1-4 22:02:50
author: VERYYOUNG
comments: true
categories: [Java]
---

构建是软件生命周期中重要的一环，在现代软件开发过程中，起着越来越重要的作用。

Ant 和 Maven 越来越不够用了， Gradle 是一个比较完美的替代品。


<!-- more -->

----------

##Ant

现在我们用的构建工具主要是 Maven，其实在 Maven 之前还有一种东东，叫 Ant。

Ant 非常的灵活，你可以在 build.xml 里面编写任何你想要的东西。

缺点就是基于 xml 的语法非常啰嗦，难以管理，难以编写。

我刚开始写程序的时候用的是 Ant，反正那语法我一点映像都没有了，我都是从网上找个 build.xml 的例子，然后对着例子建好目录结构。

这个其实就有点“[约定优于配置](https://zh.wikipedia.org/wiki/%E7%BA%A6%E5%AE%9A%E4%BC%98%E4%BA%8E%E9%85%8D%E7%BD%AE)” 的意思了。

##约定优于配置

约定优于配置（convention over configuration），也称作按约定编程，是一种软件设计范式，旨在减少软件开发人员需做决定的数量，获得简单的好处，而又不失灵活性。

如果您所用工具的约定与你的期待相符，便可省去配置；反之，你可以配置来达到你所期待的方式。

写 Java 难免要管理一系列的 xml 文件，很麻烦，很难调试。

[Ruby On Rails](https://zh.wikipedia.org/wiki/Ruby_on_Rails) 这个 Ruby 的框架将约定优于配置这个理念发挥到了极致。 

你只要按照约定在对应的地方添代码就行，其他的 Rails 都帮你做好了，再加上 Ruby 这种优雅简洁的语法，开发效率要比 Java Web 快 N 多倍。

用 Java 做 Web 开发要学一堆的开源框架，Ruby 一个 Ruby On Rails 全部搞定！

##Maven

把话题扯回到构建工具。

Maven 的整合这一概念，为项目提供合理的默认行为。

无需定制，源代码被默认放在${basedir}/src/main/java文件夹中，资源被默认放在 ${basedir}/src/main/resources文件夹中。测试默认放在 ${basedir}/src/test文件夹中，默认一个项目产生的JAR文件。Maven的默认您要编译的字节码到 ${basedir}/target/classes，然后在${basedir}/target文件夹中创建一个分发的JAR文件。

而相同的功能，Ant 得写一大串的 xml 文件。

Maven 很快席卷 Java 圈，几乎成了 Java Web 的标准构建工具了。

##更加复杂的 task


然而每个项目都有自己的特定需求，标准做法必然是无法满足的。

比如目录更改，本地 Jar 包依赖，自定义操作等，Maven 本身没法完成，只能去写 Maven 插件。

扩展 Maven 对任何新手都是一件头疼的事，我们要学会编写插件，要搞清楚生命周期，这时，突然会唤起一丝丝对于 ANT 的怀念，虽然它做简单事不容易，但做复杂事却也没这么困难。

Gradle 能完美的解决 Ant 和 Maven 带来的这些痛点。

##Gradle

Gradle 是其是结合了 Maven 和 Ant 双方优点的一种基于 Groovy DSL 的新式项目构建工具。而且由于是基于 Groovy 语言，所以语法上要比基于 XML 的 Maven 和 Ant 简洁许多，并且功能更加强大。 

它能提供的是：

1.  一个像 Ant 一样，通用的灵活的构建工具。
2.  一种可切换的，像 Maven 一样的基于约定的构建框架，却又从不锁住你。
3.  对多项目构建的强大支持。
4.  强大的依赖管理（基于Apache Ivy）。
5.  全力支持已有的 Maven 或者 Ivy 仓库基础建设。
6.  在不需要远程仓库或者 pom.xml 或者 ivy 配置文件的前提下，支持传递性依赖管理。
7.  兼容 Ant 任务。
8.  基于 Groovy 脚本构建。


直接上一个 Gradle 的例子


	buildscript {
		repositories {
			mavenCentral()
		}
		dependencies {
			classpath("org.springframework.boot:spring-boot-gradle-plugin:1.2.6.RELEASE")
		}
	}
	dependencies {
		compile("org.springframework.boot:spring-boot-starter-web") {
			exclude module: "spring-boot-starter-tomcat"
		}
		compile("org.springframework.boot:spring-boot-starter-security")
		compile("org.springframework.boot:spring-boot-starter-data-jpa")
		testCompile("mysql:mysql-connector-java:5.1.25")
	}
	
就这么点代码，生成一个 Spring-Boot 项目，而基于 maven 的 pom.xml 得写 N 多行了，Ant 就更多了！

Gradle 可以自定义任务

	task hello << {
		println "hello world"
	}

这样就定义了一个任务，然后

	gradle hello

就执行了。

Gradle 基于 Groovy 语言，你可以用 Groovy 去实现一系列复杂的操作，来代替掉 println "hello world" 。

##使用现状

Android 项目管理方面 Gradle 占有统治性地位，Android 新建项目已默认用 Gradle 管理了。

Java 项目大部分还是在用 Maven 管理，只有少部分比较 Geek 的团队已经切到 Gradle 了，比如 LinkedIn、Google...








