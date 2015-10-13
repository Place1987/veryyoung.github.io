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


1.	@Getter / @Setter

	这两个注解可以自动生成繁琐的 set 和 get 方法，生成的代码正如 IDE 自动生成的一样（bool 值的 get 方法会叫 is）。
	
 	默认的 set 和 get 方法都是 public 的，你可以通过 AccessLevel 来控制访问粒度。
	 
	比如
	
		@Setter(AccessLevel.PROTECTED)
		
	会生成一个 protected 的 set 方法。
	
2.	@ToString

	生成一个人类可读的 toString 方法，默认情况下，它会打印类的名称，以及每个字段的 get 方法（数组将会通过  Arrays.deepToString 打印），以逗号分隔。
	
	默认情况下，所有非静态字段将被打印出来。如果你想跳过某些字段，可以用 exclude 去排除。
	
	比如不想打印 id ，可以 
	
		@ToString(exclude="id")
		

3.	@EqualsAndHashCode
	
	生成 equals() 和 hashCode() 方法的。

	默认情况下，它会使用所有非静态，非瞬态字段，如果你想跳过某些字段，可以用 exclude 去排除。
	
4.	@NoArgsConstructor, @RequiredArgsConstructor, @AllArgsConstructor
	
	
