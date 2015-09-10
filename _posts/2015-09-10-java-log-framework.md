---
layout: post
title: Java常用日志框架总结
date: 2015-9-10 16:01:08
author: VERYYOUNG
comments: true
categories: [Java]
---

日志记录在程序开发中是很重要的一个环节，日志在开发、调试、问题定位、问题分析中都起着很重要的作用。

Java生态圈提供了很多日志工具供开发者选择。

<!-- more -->

----------

先明确下另个概念：

1. 日志系统：日志系统是日志的具体实现。Java日志系统比较丰富，常用的有Log4j、java.util.Logging、Logback。
2. 日志框架：为了解决多个日志系统的兼容问题，日志框架应运而生。主流的日志框架有commons-logging和SLF4J。

##Log4j
最早的 Java 日志框架之一，由 Apache 基金会发起，提供灵活而强大的日志记录机制。但是其复杂的配置过程和内部概念往往令使用者望而却步

##java.util.Logging
JDK提供的日志系统，较混乱，不常用。

##Logback
Logback是由log4j创始人设计的又一个开源日记组件。是Log4j的替代产品，需要配合日志框架SLF4j使用。


##commons-logging
目前广泛使用的Java日志门面库。通过动态查找的机制，在程序运行时自动找出真正使用的日志库。但由于它使用了ClassLoader寻找和载入底层的日志库，导致了像OSGI这样的框架无法正常工作，由于其不同的插件使用自己的ClassLoader。OSGI的这种机制保证了插件互相独立，然而却使common-logging无法工作。

##SLF4J
简单日记门面(Facade)SLF4J是为各种loging APIs提供一个简单统一的接口，从而使得最终用户能够在部署的时候配置自己希望的loging APIs实现。 Logging API实现既可以选择直接实现SLF4J接的loging APIs如： NLOG4J、SimpleLogger。也可以通过SLF4J提供的API实现来开发相应的适配器如Log4jLoggerAdapter、JDK14LoggerAdapter。   


##Log4j与LogBack 比较
LogBack作为一个通用可靠、快速灵活的日志框架，将作为Log4j的替代和SLF4J组成新的日志系统的完整实现。LOGBack声称具有极佳的性能。 另外，LOGBack的所有文档是全面免费提供的，不象Log4J那样只提供部分免费文档而需要用户去购买付费文档。 

##SLF4J与common-logging 比较
SLF4J在编译时静态绑定真正的Log库,因此可以再OSGI中使用。

Log4j 提供 TRACE, DEBUG, INFO, WARN, ERROR 及 FATAL 六种纪录等级，但是 SLF4J 认为 ERROR 与 FATAL 并没有实质上的差别，所以拿掉了 FATAL 等级，只剩下其他五种。

大部分人在程序里面会去写logger.error(exception),其实这个时候Log4j回去把这个exception tostring。
真正的写法应该是logger(message.exception);而slf4j就不会使得程序员犯这个错误。

log4j间接的在鼓励程序员使用string相加的写法，而slf4j就不会有这个问题，你可以使用

	logger.error("{} is+serviceid",serviceid);

使用slf4j可以方便的使用其提供的各种集体的实现的jar。（类似commons-logger）

从commons--logger和log4j merge非常方便，slf4j也提供了一个swing的tools来帮助大家完成这个merge。

提供字串内容替换的功能，会比较有效率，说明如下：

	// 传统的字符串产生方式，如果没有要记录Debug等级的信息，就会浪费时间在产生不必要的信息上
	logger.debug("There are now " + count + " user accounts: " + userAccountList);

	// 为了避免上述问题，我们可以先检查是不是开启了Debug信息记录功能，只是程序的编码会比较复杂
	if (logger.isDebugEnabled()) {
	    logger.debug("There are now " + count + " user accounts: " + userAccountList);
	}

	// 如果Debug等级没有开启，则不会产生不必要的字符串，同时也能保持程序编码的简洁
	logger.debug("There are now {} user accounts: {}", count, userAccountList); 



##推荐使用LogBack+Logback


 参考

1. [Java Logging with SLF4J and Logback](https://github.com/congdepeng/depeng-documents/blob/master/Java%20Logging%20with%20SLF4J%20and%20Logback.md)
2. [为什么要使用SLF4J而不是Log4J](http://www.importnew.com/7450.html)
3. [java日志组件介绍（common-logging，log4j，slf4j，logback）](http://www.pinhuba.com/log/101114.htm)














