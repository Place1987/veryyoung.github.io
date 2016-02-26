---
layout: post
title: 微信公众号开发流程和注意事项
date: 2016-2-26 15:11:55
author: VERYYOUNG
comments: true
categories: [Others]
---

微信公众号开发其实很简单，稍微有点 web 开发功底就能搞定。下面简单说一下大体的开发流程以及需要注意的点。

<!-- more -->

## 1.注册账号&申请认证
通过这一步之后，我们可以得到一个微信公众号，申请认证后能获得对应的微信 api 权限。

完成1操作之后，登录[微信后台](http://mp.weixin.qq.com), 在后台可以推送文章，管理关注用户，和关注用户聊天。

## 2.开启开发者模式 

微信公众号分为两个模式：编辑模式和开发者模式。

编辑模式是没有开发能力的人使用的，能设定简单的自定义回复规则。

而使用开发者模式，可以通过代码能完成各种复杂的功能。

开启开发模式的时候需要配置4个东西：URL（服务器地址），Token（令牌）、EncodingAESKey、消息加解密方式。

后两个是消息加解密相关的，重点关注下前两个参数。

    URL：能正确响应微信服务器请求的URL，http协议，80端口。
    Token：令牌，须和代码里面指定的一样。


## 3.服务接入

微信服务器会向我们填写的URL 发送一个 GET 请求，并带上参数，如果能正确的根据微信的请求参数返回数据，微信会认为接入成功。

接入成功之后就可以监听微信服务器发送来的事件或者数据并作出正确的响应了。


客户端发起请求，请求发送到微信服务器，微信服务器把请求转发给开发者提供的服务，开发者提供的服务先对请求进行解密，如果认定是微信来的请求，再根据请求的参数作出响应。

![](http://ww3.sinaimg.cn/large/9732f922jw1f1clgytqnsj20f80bsaa9.jpg)


代码编写：参考微信提供的文档 https://mp.weixin.qq.com/wiki/10/bc2b6dd41e25befa713fafcf5094ff1e.html


微信请求的数据格式都是 xml，需要根据规则解析出数据，作出对应的响应，响应数据格式也得是 xml。


一般情况下不会手工去一个个功能接，最好是直接找好网上别人封装好的 sdk，可以在 GitHub 上搜索下 wechat sdk，会有很多选择，
https://github.com/search?utf8=%E2%9C%93&q=wechat+sdk&type=Repositories&ref=searchresults。


选好sdk之后，对着 sdk 的规范进行开发就行了。






## 需要注意的地方

### 1.测试号

直接在用户使用的微信号上进行开发肯定是不太好的，还好微信提供了微信公众号测试号，可以很方便的申请到一个“小号”进行调试，所有高级接口的权限都有的。 申请地址：https://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=sandbox/login

### 2.外网访问

前面提到过，微信服务器会把请求转发开发者编写的服务上去，这个服务必须是能通过外网访问的。在公司里面没有这样的条件。

还好有 [ngrok](https://ngrok.com/) 这个神器，能把内网的 ip 和端口映射到外网去。

点击链接，下载一个对应平台的可执行文件，用法


    ngrok http 8080

    ngrok by @inconshreveable                                                                                                                                                                                                     (Ctrl+C to quit)

    Tunnel Status                 online
    Version                       2.0.19/2.0.20
    Web Interface                 http://127.0.0.1:4040
    Forwarding                    http://d5540cd9.ngrok.io -> localhost:8080
    Forwarding                    https://d5540cd9.ngrok.io -> localhost:8080

    Connections                   ttl     opn     rt1     rt5     p50     p90
                                0       0       0.00    0.00    0.00    0.00

会得到一个外网映射的地址：http://d5540cd9.ngrok.io, 访问这个地址相当于访问了 localhost:8080


### 3.访问外网

微信公众号的有些服务（比如构建菜单）需要服务器主动给微信服务器发送请求的，而公司的服务器默认情况下是不具备这个条件的。如果这个活本地可以完成，最好直接在本地完成，如果非要到线上执行，一定要先申请服务器对外网的访问权限。


### 4.access_token 管理

access_token  是微信公众号非常重要的一个东西，公众号调用很多接口都需要带上这个参数。 access_token 的过期时间是两小时，每天获取的次数有限。需要把这个值缓存起来，如果是多台机器部署，需要注意不能存内存里面，以免多台机器存储的值不同导致多次刷新 access_token，导致获取次数耗尽。