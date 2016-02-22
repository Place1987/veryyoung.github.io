---
layout: post
title: Java 热部署的方案探索
date: 2016-1-10 22:54:26
author: VERYYOUNG
comments: true
categories: [Java]
---

为什么需要热部署？

Java 程序员最幸福的事情是可以在等程序编译的时候泡 Java！！（开个玩笑）



<!-- more -->

----------

# 热部署的方案


1.	Tomcat Reload 
2.	Eclipse Debug 模式
3.	IDEA Reload
4.	Jetty
5.	Jrebel

## Tomcat Reload


修改 tomcat 的配置文件 server.xml 的 Host 配置，加上 reloadable="true"。

缺点：只能热部署静态文件，修改 Java 或配置会自动重启 server，效率低下，还容易造成内存溢出、 class 找不到等 bug。 


## Eclipse Debug 模式

Eclipse debug 模式修改完 Java 代码会自动重启 server。

缺点同上~


## IDEA Reload

IDEA 在 debug 模式下设置失去焦点更新资源和 classes 

![](http://veryyoung.u.qiniudn.com/20151211144609.png)

缺点：只支持静态文件、Java 现有方法的更改，新增 Java 方法、类，或者改变 SpringMVC 的 RequestMapping、Spring 配置等都不会生效。 


## Jetty
Jetty 会监听生成的 build 目录，遇到文件更新会自动替换掉。

但并不能监听源码的变更。



### 基于Gradle 的解决方案

1.	Gradle Watch 
2.	Gretty
3.	Continuous Build


#### [Gradle Watch](https://github.com/bluepapa32/gradle-watch-plugin)

gradle watch 的作用是监听某种类型的文件的变化，包括添加，删除和修改，然后执行预定义的任务。


使用方法大概如下：

    apply plugin: 'watch'

    watch {
        java {
            files files('src/main/java')
            tasks 'compileJava'
        }
    }
 
 
 缺点：只支持低版本 Gradle，并且已不再维护！
 
 
 
 [Gretty](https://github.com/akhikhl/gretty)
 
 >Gretty is a feature-rich gradle plugin for running web-apps on embedded servlet containers. 
 
 Gretty 覆盖了 jettyRun 和 tomcatRun 等 task，使用起来和普通的 jettyRun 之类的一样，但是提供了热部署的功能。
 
 热部署效率差！感觉是半重启！
 
 
 [Continuous Build](http://gradle.org/feature-spotlight-continuous-build/)
 
 Continuous Build 是 Gradle 2.5 的 feature，持续构建。
 
 使用起来非常简单：
 
    gradle -t
    
缺点：


1.	需要的 Gradle 版本太高  
2.	实验性特性
3.	不支持 Jetty


## [Jrebel](http://zeroturnaround.com/software/jrebel/)

>Reload Code Changes Instantly
 
这是一款 IDE 热部署插件，效果非常强大。

具体可参考[利用Jrebel热部署提升工作效率](/blog/2015/02/05/using-jrebel-hot-deployment-making-work-efficiency.html)。

瑕疵：

1.	修改文件过多偶尔会异常
2.	偶尔会失效
3.	昂贵
