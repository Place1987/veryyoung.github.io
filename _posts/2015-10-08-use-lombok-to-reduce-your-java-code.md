---
layout: post
title: 使用 Lombok 来缩减 Java 代码
date: 2015-10-8 23:05:08
author: VERYYOUNG
comments: true
categories: [Java]
---

Java 程序员比较烦的一件事情之一就是要写大量的样板代码。


所谓样板代码，是那些没有营养，却又不得不写的代码，写的时候觉得毫无技术含量，依样画葫芦，比如一个类的全参构造函数、无参构造函数、get/set方法、toString方法等等。

虽然 IDE 可以自动生成，但每次更改字段又得重新生成，不够优雅！

<!-- more -->

----------

[Lombok](https://projectlombok.org/) 就能比较优雅的解决掉这个烦恼！！


1.	@Data
	
	使用 @Data 注解就如同对所有属性使用了 @Getter 注解，对所有非 final 的属性使用了 @Setter 注解, 对 class 使用了  @RequiredArgsConstructor、@ToString, @EqualsAndHashCode
	
	
2.	@Value
	
	与 @Data 类似的注解还有 @Value， 两个注解的主要区别就是如果变量不加 @NonFinal， @Value 会给所有的属性变为 final 的。当然如果是 final 的话，就没有 set 方法了。
	
3.	@Builder

	为对象提供的 builder，可以用类似下面的代码，快速的构建出对象实例。
	
		Person.builder().name("Adam Savage").city("San Francisco").job("Mythbusters").job("Unchained Reaction").build();
		
4.	@SneakyThrows

	在代码中，使用 try、catch 来捕捉一些异常，如果你不想处理，只想抛出去，可以使用 @SneakyThrows 来修饰方法。
	
5.	@NonNull

	将 @NonNull 放在构造函数上会自动检查构造函数的对象是否为空，为空直接抛出 NullPointerException。
	
	生成的代码 如下：
	
		 if (param == null) {
			 throw new NullPointerException("param")
		 }
		 
6.	@Val
	
	你可以使用 val 为局部变量声明的类型。 lombok 会自动决定该变量的类型。
	
	比如：
		
		val example = new ArrayList<String>();
		
	最终会生成
	
		final ArrayList<String> example = new ArrayList<String>();
		

7.	@Cleanup

	可以确保在当前范围内变量用完后自动释放。
	
	比如
		
		@Cleanup InputStream in = new FileInputStream("some/file");
		
	在方法最后会执行
		
		 in.close()

8.	@Sychronized 

	@Sychronized 是一个处理线程安全问题的 annotation，修饰在方法上，会在方法内部加锁。
	
	他的使用方法和关键字 synchronized 比较类似，但是有一些不同点就是，关键字 synchronized 是锁定当前对象（this指针） ， 而 @Synchronized 则会锁定一个 private 的常量。如果当前类中没有这个常量，就会自动生成一个。
	
		
9.	@Getter(lazy=true)

	使用 lazy 版的 @Getter， 会由 Lombok 帮助你管理缓存的同时处理线程安全的问题。
	
10.	@Log
	
	可以使用 @Log 注解生成日志类。
	
	有如下六种用法：
	
		@CommonsLog
		
			private static final org.apache.commons.logging.Log log = org.apache.commons.logging.LogFactory.getLog(LogExample.class);
			 
		@Log
		
			private static final java.util.logging.Logger log = java.util.logging.Logger.getLogger(LogExample.class.getName());	 
			
		@Log4j
		
			private static final org.apache.log4j.Logger log = org.apache.log4j.Logger.getLogger(LogExample.class);	
			
		@Log4j2
		
			private static final org.apache.logging.log4j.Logger log = org.apache.logging.log4j.LogManager.getLogger(LogExample.class);
			
		@Slf4j
		
			private static final org.slf4j.Logger log = org.slf4j.LoggerFactory.getLogger(LogExample.class);
			
		@XSlf4j
		
			 private static final org.slf4j.ext.XLogger log = org.slf4j.ext.XLoggerFactory.getXLogger(LogExample.class);	
			
			
			
			
----

是不是有一种写动态语言的优雅的感觉？					

----

有的同学可能会担心 Lombok 的性能问题。

Lombok 的原理并不是通过字节码类库如 cglib、asm 去增强字节码的，而是使用对抽象语法树 AST 的转换增强字节码(.class文件)的。

不是在执行时决定行为，而是在编译时生成了代码，性能和你手写的一样！！

关于 AST 的官方文档 [http://openjdk.java.net/groups/compiler/doc/compilation-overview/index.html](http://openjdk.java.net/groups/compiler/doc/compilation-overview/index.html)


还有国人整理的注解相关的文档 [Java深度历险（六）——Java注解](http://www.infoq.com/cn/articles/cf-java-annotation)



----

PS：Lombok 对 IDE 提供了很好的支持，调试的时候毫无感知，就像自己手写了那部分样板代码一样！

----

建议所有的 Java 项目都用上这个“黑科技”。