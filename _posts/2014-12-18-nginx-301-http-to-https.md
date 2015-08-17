---
layout: post
title: Nginx跳转任意http请求到https
date: 2014-12-18 22:59
author: VERYYOUNG
comments: true
categories: [Linux]
---
网站买了证书，绿条，多霸气！

那么自然得拦截http的访问方式了。

拦截http，301到https



各种Google，最后在Nginx官网找到例子，配置很简单，如下:

	server {
	        listen          *:80;
	        return          301 https://www.domain.com$request_uri;
	}

其实就是拦截所有80端口的请求，然后重定向到https的对应uri

完整配置如下:


	server {
	        listen  443 ssl;
	        ssl_certificate /home/ubuntu/www.domain.com.crt;
	        ssl_certificate_key /home/ubuntu/domain.com.key;
	
	
	        location ~ ^/(public/|webscan_360_cn.html|do_not_delete/noc.gif) {
	                root         /home/node/static;
	                expires      30d;
	        }
	
	
	
	        location / {
	                proxy_pass http://127.0.0.1:5000;
	                proxy_set_header Host $http_host;
	                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	        }
	
	}
	
	server {
	        listen          *:80;
	        return          301 https://www.domain.com$request_uri;
	}


