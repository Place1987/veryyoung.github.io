---
layout: post
title: ngrok：将本地服务暴露到外网
date: 2016-1-6 22:50:09
author: VERYYOUNG
comments: true
categories: [Http]
---

ngrok 可以将本地服务暴露到外网，解决了路由穿透， 80 端口封锁之类的问题。


<!-- more -->

----------

##外网能访问需要的条件

###公网IP

运营商并没有给所有人提供了公网 IP， 如果在宿舍或者公司，这想都不敢想。

###路由映射

得有路由器的完全控制权，才能把公网 IP 映射到本机来。

###80 端口

部分运营商对 80 端口是封锁的。


来看看微信公众号开发者接入对 url 的要求

>必须以http://开头，目前支持80端口

而如果你在公司，想调试怎么办？不可能每改动一次都让 OP 上线一次吧，多麻烦！！

ngrok 能完美解决这个痛点啦！！

用起来很简单，到 [ngrok官网](https://ngrok.com/)， 下载 ngrok 服务，然后执行一段简单的命令就行了。

比如 

    ngrok http 8090
    
可以把本机的 8090 端口暴露到外网。

看看运行结果就知道了，一目了然。

    ./ngrok http 8090

    ngrok by @inconshreveable  

    Tunnel Status                 online
    Version                       2.0.19/2.0.19
    Web Interface                 http://127.0.0.1:4040
    Forwarding                    http://b8b5676b.ngrok.io -> localhost:8090
    Forwarding                    https://b8b5676b.ngrok.io -> localhost:8090

    Connections                   ttl     opn     rt1     rt5     p50     p90
                                23      0       0.00    0.00    0.53    24.77

    HTTP Requests
    -------------

    POST /auth.do                  200 OK
    POST /auth.do                  200 OK
    POST /auth.do                  200 OK
    POST /auth.do                  200 OK
    
    
----

ngrok 官方提供的服务在国内很不稳定，国内有很多这样的服务。

ngrok 是开源的，代码在 [https://github.com/inconshreveable/ngrok](https://github.com/inconshreveable/ngrok)， 可以尝试自建一个 ngrok 服务。

----

V2EX 上有人把 QQ 浏览器内嵌的 ngrok 服务提取出来了，速度很快哦，下载地址在 [http://yun.baidu.com/s/1pJu1yw7](http://yun.baidu.com/s/1pJu1yw7)
