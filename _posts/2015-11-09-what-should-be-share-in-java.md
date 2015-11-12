---
layout: post
title: Java 中值得分享的 libs
date: 2015-11-9 21:35:22
author: VERYYOUNG
comments: true
categories: [Java]
---

Java 最强大的就是其丰富的解决方案。

下面分享几个比较 Nice 的方案，其中有些能让 Java 开发变得简单和优雅！^_^



<!-- more -->

----------

##1.	[Apache Commons](https://commons.apache.org/)


Apache Commons 我们或多或少用过一点，比如 StringUtils.isEmpty、CollectionUtils、isEmpty().

Apache Commons 封装了一些常用的工具类，减少重复操作，比如字符串操作、IO 操作、集合增强等。

![](http://veryyoung.u.qiniudn.com/apache-commons.png)

举几个例子吧：

	// 读取网页内容
	InputStream in = new URL( "https://www.sogou.com" ).openStream();  
	try {  
		System.out.println(IOUtils.toString(in));  
	} finally {  
		IOUtils.closeQuietly(in);  
	} 
	
	//生成指定长度的字母和数字的随机组合字符串
	RandomStringUtils.randomAlphanumeric(5); 


非常好用，值得系统的学一遍。


##2.	[Guava](https://code.google.com/p/guava-libraries/)

Guava 是 Google 出品的第三方工具库，功能和 Apache Commons 有点类似。

Guava 做了很多数据结构的增强，比如不可变集合、多项映射的 Map 等。

这个也同样建议系统的学习，能让 Java 编程变得优雅不少。

[并发编程网](http://ifeve.com/) 有个不错的中文版教程: [Google Guava官方教程（中文版）](http://ifeve.com/google-guava/)


##3.	[javatuples](http://www.javatuples.org/)

编程过程中经常会遇到多个返回值的问题，通常返回一个 Array、集合（List、Set、Map）或自定义一个 Class。

在很多语言中都提供元组类型 Tuple 的支持，比如 Scala、C++、.Net。

javatuples 是一个很简单的 lib，它没有什么华丽的功能，就是提供了支持返回多个元素的一些类。 

- Unit<A> (1 element)
- Pair<A,B> (2 elements)
- Triplet<A,B,C> (3 elements)
- Quartet<A,B,C,D> (4 elements)
- Quintet<A,B,C,D,E> (5 elements)
- Sextet<A,B,C,D,E,F> (6 elements)
- Septet<A,B,C,D,E,F,G> (7 elements)
- Octet<A,B,C,D,E,F,G,H> (8 elements)
- Ennead<A,B,C,D,E,F,G,H,I> (9 elements)
- Decade<A,B,C,D,E,F,G,H,I,J> (10 elements)


 

##4.	[OkHttp](https://github.com/square/okhttp)

HttpClient 用起来挺麻烦的，语法啰嗦，拿到手肯定得自己再封装一次，而且一堆废弃的 api， not happy....

OkHttp 是 HttpClient 的一个成熟的替代品！

首先语法很优雅：

	OkHttpClient client = new OkHttpClient();
	
	Request request = new Request.Builder()
		.url("https://api.github.com/repos/square/okhttp/issues")
		.header("User-Agent", "OkHttp Headers.java")
		.addHeader("Accept", "application/json; q=0.5")
		.addHeader("Accept", "application/vnd.github.v3+json")
		.build();
	
		Response response = client.newCall(request).execute();
		if (!response.isSuccessful()) {
			throw new IOException("Unexpected code " + response);
		}
	
		System.out.println("Server: " + response.header("Server"));
		System.out.println("ResponseBody: " + response.body().string());
		
语法很简洁，几乎每一行代码都是有用的。

同时支持 

1.	使用 GZIP 压缩减少传输的数据量;
2.	缓存，减少重复请求;
3.	SPDY；
4.	连接池；
5.	失败重试（如果你的服务有多个 IP 地址，如果第一次连接失败，OkHttp 将使备用地址）;

Android 在慢慢的废弃 HttpClient，终于在 6.0 把 HttpClient 完全删掉了。

##5.	[jsoup](http://jsoup.org/)

jsoup 是一款 Java 的 HTML 解析器，可直接解析某个 URL 地址的 HTML 文本内容。

它提供了一套非常省力的 API，可通过 DOM，CSS 以及类似于 jQuery 的操作方法来取出和操作数据。


	Document doc = Jsoup.connect("https://www.sogou.com/").get();
	Elements newsHeadlines = doc.select(".s-input-box input);
	
jsoup 也可以 set httpHeader 等。

可以做比较轻量级的爬虫。


##6.	[fastjson](https://github.com/alibaba/fastjson)

fastjson 是一个 Java 语言编写的高性能功能完善的 json 解析库，号称史上最快的 jackson，来自阿里巴巴。

除了 jdk 外不依赖任何 jar 包，用起来也非常简单，语法类似 Gson。

	User user = new User();
	user.setId(1L);
	user.setUserName("userName");
	
	String jsonString = JSON.toJSONString(user); 
	
	user = JSON.parseObject(jsonString, User.class);
	

##7.	[Mockito](http://mockito.org/)

Mockito 是一个流行的 Mocking 框架。

它使用起来简单，学习成本很低，而且具有非常简洁的 API ，测试代码的可读性很高。

因此它十分受欢迎，用户群越来越多，很多的开源的软件也选择了 Mockito。

         
	List<String> list = mock(ArrayList.class);  
		
	when(list.get(0)).thenReturn("helloworld");  
	
	String result = list.get(0);  
		
	verify(list).get(0);  
		
	Assert.assertEquals("helloworld", result);  
	
	when(list.get(1)).thenThrow(new RuntimeException("test excpetion"));  


##8.	[Logback](http://logback.qos.ch/)

Logback 是由 log4j 创始人设计的又一个开源日志组件, 用来替换掉 log4j。

据说有很多优点，我也不太清楚，我只知道用起来很优雅 ^_^
	
	
	// log4j
	if (logger.isDebugEnabled()) {
		logger.debug("There are now " + count + " user accounts: " + userAccountList);
	}
	
	// slf4j
	logger.debug("There are now {} user accounts: {}", count, userAccountList);
	
Logback 一般与日志门面框架 [SLF4J](http://www.slf4j.org/) 配合使用。
	

##9.	[Joda](http://www.joda.org/joda-time/)

Java 自带的时间工具 java.util.Calendar、java.util.Date 非常别扭，一个很简单的功能都要写很多很行代码。

比如给一个日期加90天并输出结果：

	Calendar calendar = Calendar.getInstance();
	calendar.set(2000, Calendar.JANUARY, 1, 0, 0, 0);
	SimpleDateFormat sdf = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss.SSS");
	calendar.add(Calendar.DAY_OF_MONTH, 90);
	System.out.println(sdf.format(calendar.getTime()));

Joda 是 Java8 之前最优雅的 Java 时间库。

上面的功能使用 Joda 只需两行

	DateTime dateTime = new DateTime(2000, 1, 1, 0, 0, 0, 0);
	System.out.println(dateTime.plusDays(90).toString("MM/dd/yyyy HH:mm:ss.SSS");
	
Joda 还提供了

	LocalDate - 不包含具体时间的日期，年月日
	LocalTime - 不含日期的时间，时分秒
	Instant - 时间戳
	DateTime - 带时区的时间
	DateTimeZone - a better time-zone
	Duration and Period - 时间区间
	Interval - 时间间隔
	一个全面的和灵活的时间格式解析
	
Java8 已结引进了 Joda 的思想增强了 Java 时间库，然而大部分项目都没有升到 Java8。


##10.	[Lombok](https://projectlombok.org/)

Java 程序员比较烦的一件事情之一就是要写大量的样板代码。

所谓样板代码，是那些没有营养，却又不得不写的代码，写的时候觉得毫无技术含量，依样画葫芦，比如一个类的全参构造函数、无参构造函数、get/set方法、toString方法等等。

虽然 IDE 可以自动生成，但每次更改字段又得重新生成，不够优雅！

Lombok 就能比较优雅的解决掉这个烦恼！

详情请参考 [使用 Lombok 来缩减 Java 代码](/blog/2015/10/08/use-lombok-to-reduce-your-java-code.html)

##11 [Druid](https://github.com/alibaba/druid)

>Druid 是Java语言中最好的数据库连接池。Druid能够提供强大的监控和扩展功能。

Druid 来自阿里巴巴集团，在功能、性能、扩展性方面，都超过其他数据库连接池，包括 DBCP、C3P0、BoneCP、Proxool、JBoss DataSource。

Druid 不仅仅是一个数据库连接池，还提供了强大的监控功能，可以在 web 页面上看到连接池和 Sql 的工作情况。

其次，方便扩展。Druid 提供了 Filter-Chain 模式的扩展 API，可以自己编写 Filter 拦截 JDBC 中的任何方法，可以在上面做任何事情，比如说性能监控、SQL审计、用户名密码加密、日志等等。 

Druid 内置提供了用于监控的 StatFilter、日志输出的 Log 系列 Filter、防御 SQL 注入攻击的 WallFilter。 

在 Druid 的 GitHub 地址上有很详细的 Druid 介绍、使用  [Wiki](https://github.com/alibaba/druid/wiki/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98)



##12 [Dubbo](http://dubbo.io/)

Dubbo 是一个阿里巴巴开源出来的一个分布式服务框架，致力于提供高性能和透明化的 RPC 远程服务调用方案，以及 SOA 服务治理方案。

使用起来非常简单：


服务端：	
	
	<bean id=“xxxService” class=“com.xxx.XxxServiceImpl” /> 
	
	<dubbo:service interface=“com.xxx.XxxService” ref=“xxxService” /> 

客户端：

	<dubbo:reference id=“xxxService” interface=“com.xxx.XxxService” /> 
	
Dubbo 采用全 Spring 配置方式，透明化接入应用，对应用没有任何 API 侵入，只需用 Spring 加载 Dubbo 的配置即可。

Dubbo 支持各种常用的协议，如 Thrift、RMI、Hessian、WebService 等。

同时也提供了注册中心、监控中心等。

比我们内部自己写的 SOA 使用起来会简单不少。


##13 [Spring Boot](http://projects.spring.io/spring-boot/)

Spring Boot 是一个微框架，其设计目的是用来简化 Spring 应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。

约定大于配置！！！

Spring 平台饱受非议的一点就是大量的 XML 配置以及复杂的依赖管理，Spring Boot 可以做到 0 xml，同时 pom 文件也可以极大化的减小。

##14 [JFinal](http://www.jfinal.com/)

JFinal 是基于 Java 语言的极速 WEB + ORM 框架，其核心设计目标是开发迅速、代码量少、学习简单、功能强大、轻量级、易扩展、Restful。 

在拥有Java语言所有优势的同时再拥有 ruby、python、php 等动态语言的开发效率！为您节约更多时间，去陪恋人、家人和朋友 :)

![](http://veryyoung.u.qiniudn.com/20151112212459.png)

快速出 demo 神器！

类似这种的框架还有 [Play](https://www.playframework.com/)、[Grails](https://grails.org/)、[Ninja](http://www.ninjaframework.org/)、[Spark](http://sparkjava.com/) 等。





	

