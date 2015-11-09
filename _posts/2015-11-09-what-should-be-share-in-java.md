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
	

 
 

-----

@TODO

Lombok、dubbo、play、jfinal、joda、druid、Spring Boot、Grails、bintray



	

