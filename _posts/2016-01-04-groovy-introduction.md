---
layout: post
title: Grovvy：一种基于 JVM 的敏捷开发语言
date: 2016-1-4 22:12:22
author: VERYYOUNG
comments: true
categories: [Java]
---

前文说到了 Gradle 依靠 Groovy 语言发挥出了强大的性能。

Groovy是一种基于JVM（Java虚拟机）的敏捷开发语言，它结合了Python、Ruby和Smalltalk的许多强大的特性，Groovy 代码能够与 Java 代码很好地结合，也能用于扩展现有代码。由于其运行在 JVM 上的特性，Groovy 可以使用其他 Java 语言编写的库。


<!-- more -->

----------

Groovy 是 Java 平台上设计的面向对象编程语言。这门动态语言拥有类似 Python、Ruby 和 Smalltalk 中的一些特性，可以作为 Java 平台的脚本语言使用。

Groovy 的语法与 Java 非常相似，以至于多数的 Java 代码也是正确的 Groovy 代码。Groovy 代码动态的被编译器转换成 Java 字节码。

由于其运行在 JVM 上的特性，Groovy 可以使用其他Java语言编写的库。

Java 语法真的超级啰嗦，写过 Ruby、Python、PHP 这种动态脚本语言的人应该深有体会。

来个小例子对比下吧。

	for (int i = 0; i < 3; i++) {
		System.out.println("Hello world");
	}

Groovy 可以这样写

	for (i in 0..2) {
		println 'Hello world'
	}
	
或者

	3.times {
		println 'Hello world'
	}
	
可以不定义类型，Groovy 会智能的去判断类型。

	def coll = ["Groovy", "Java", "Ruby"]
	assert  coll instanceof Collection
	assert coll instanceof ArrayList
	
Java 代码得啰嗦的写

	Collection<String> coll = new ArrayList<String>();
	coll.add("Groovy");
	coll.add("Java");
	coll.add("Ruby");
	
还有这种高端玩法：

	def numbers = [1,2,3,4]
	assert numbers + 5 == [1,2,3,4,5]
	assert numbers - [2,3] == [1,4]
	
	def map=['name':'john','age':14,'sex':'boy']
	map.each({ 
		println it.getKey() + "-->" + it.getValue()
    })
		
还有一些非常省代码的特性，比如

不需要 public 修饰符，不需要类型说明，不需要 getter/setter 方法，不需要 return....
	
Groovy 入门门槛非常低，能写 Java 的人随便看几分钟语法就可以动手写了，如果实在搞不定，直接上 Java 代码！

Groovy 的优点很明显，开发效率高；因为是动态语言，缺点也很明显，性能会差不少，大概会慢五倍左右。

但五倍的性能差距，在脚本语言越来越流行的今天，完全不是问题了，至少做 Web 开发没问题。