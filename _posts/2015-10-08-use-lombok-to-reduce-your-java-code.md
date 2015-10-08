---
layout: post
title: 使用 Lombok 来缩减 Java 代码
date: 2015-10-8 23:05:08
author: VERYYOUNG
comments: true
categories: [Java]
---

Java 程序员比较烦的一件事情之一就是要写大量的 set、get、toString 等方法。

大部分情况下这些方法都不涉及到业务逻辑，都非常的简单。

虽然 IDE 可以自动生成，但每次更改字段又得重新生成，不够优雅！

<!-- more -->

----------

[Lombok](https://projectlombok.org/) 就能比较优雅的解决掉这个烦恼！！
