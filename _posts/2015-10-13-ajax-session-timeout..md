---
layout: post
title:	处理 Ajax session 超时
date: 2015-10-13 20:45:25
author: VERYYOUNG
comments: true
categories: [Java]
---

很多应用都在需要用户登陆的 controller 添加了拦截器，未登陆或登陆超时会被重定向到登陆页面。

但是长期不操作 session 过期之后，执行 Ajax 请求，返回的数据会直接是登陆页面的 html 文件。

这样用户操作起来会得不到任何的反馈，没有返回数据，也没重定向到登陆页面。

<!-- more -->

----------

我们需要单独处理 Ajax 请求。

Ajax 请求头中带有 X-Requested-With 信息，其值为 XMLHttpRequest，这正是我们可以利用的地方。


可以在拦截器里面判断请求是否来自 Ajax，如果来自 Ajax，设置一个标示：

            //如果是ajax请求响应头会有，x-requested-with
            if (request.getHeader("x-requested-with") != null && request.getHeader("x-requested-with").equalsIgnoreCase("XMLHttpRequest")) {
                response.setHeader("sessionStatus", "timeout");//在响应头设置session状态
                return false;
            }
			


接下来就是 js 的事情了。

Ajax 可以全局设置:

	$.ajaxSetup({  
		type: 'POST',  
		complete: function(xhr,status) {  
			var sessionStatus = xhr.getResponseHeader('sessionstatus');  
			if(sessionStatus == 'timeout') {  
				window.location.href = '/login';              
			}  
		}  
	});
	
	
这样 Ajax 请求的时候，如果 session 过期了也会重定向到 login 页面了！