---
layout: post
title: Http状态码301和302的区别
date: 2015-8-24 22:08:14
author: VERYYOUNG
comments: true
categories: [Http]
---

301和302都是重定向，他们之间有什么区别呢？

<!-- more -->

先看看wiki [http状态码](https://zh.wikipedia.org/zh/HTTP%E7%8A%B6%E6%80%81%E7%A0%81)的解释。

>301 Moved Permanently
被请求的资源已永久移动到新位置，并且将来任何对此资源的引用都应该使用本响应返回的若干个URI之一。如果可能，拥有链接编辑功能的客户端应当自动把请求的地址修改为从服务器反馈回来的地址。除非额外指定，否则这个响应也是可缓存的。







>302 Found
请求的资源现在临时从不同的URI响应请求。由于这样的重定向是临时的，客户端应当继续向原有地址发送以后的请求。只有在Cache-Control或Expires中进行了指定的情况下，这个响应才是可缓存的。





字面区别是301是永久重定向，302是临时重定向。


----------

### 301适合永久重定向

比较常用的场景是做域名跳转。

比如访问[http://veryyoung.github.io](http://veryyoung.github.io)会重定向到[http://veryyoung.me](http://veryyoung.me)

![](http://ww1.sinaimg.cn/large/9732f922gw1eve2cfjlrgj20b906fq3c.jpg)

如上图，请求后的状态码为301，并在返回头的Location中会指明重定向的目标地址。

同时301请求可以缓存（See Status Code，后边写着from cache）

如果你把网页的后缀从.php改为.html，301也是非常适合的。

把网站从http重定向到https，301也非常适合。


----------


### 302用来做临时跳转
比如未登陆的用户访问用户中心重定向到登陆页面。

访问404页面会自动重定向到首页


##nginx 301、302配置

rewrite后面接上permanent就代表301跳

	//把来自veryyoung.me的请求301跳到 www.veryyoung.me
	if ($host != 'veryyoung.me') {
        rewrite ^/(.*)$ http://www.veryyoung.me/$1 permanent;
	}

接上redirect代表302跳

	//把来自veryyoung.me的请求302跳到 www.veryyoung.me
	if ($host != 'veryyoung.me') {
        rewrite ^/(.*)$ http://www.veryyoung.me/$1 redirect;
	}


##301、302 Java实现
	
	//301
	response.setStatus(HttpServletResponse.SC_MOVED_PERMANENTLY);
	response.setHeader("Location", "http://somewhere/");


	//302
	response.setStatus(HttpServletResponse.SC_MOVED_PERMANENTLY);
  	response.sendRedirect("http://somewhere/");









