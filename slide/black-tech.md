title: “黑科技”
speaker: veryyoung
url: https://github.com/veryyoung
transition: move
theme: dark

[slide]

# “黑科技”
### 各种新奇的、好玩的技术或者技术产品，能让开发过程变得更简单和方便，能提高工作效率。



<br/><br/>
<small>演讲者：杨雄伟</small>


[slide]
## 大纲
----
* 小工具&浏览器插件 {:&.zoomIn}
* 虚拟化&容器
* 代码管理&构建
* 编辑器&IDE&IDE插件
* Java Jars
* Others

[slide]
## 什么是黑科技呢？

###来看看 WIKI 的解释：

<br/>
<br/>


>黑科技:远超越现今人类科技或知识所能及的范畴，其科学技术或者产品缺乏科学根据且违反自然原理。{:&.zoomIn}


[slide]

我下面分享的所谓的“黑科技”大部分指的是一些比较优雅、快捷的开发工具、框架，还有可能是一些好玩的，或者能提高工作效率的小工具。 


[slide]

## 下面会介绍到很多东东，每种东西我只是很简单的介绍一下，不会深讲。

<br/>
<br/>

第一是因为时间的限制，第二是很多我也只是接触了一点皮毛，让我深入的讲我也讲不了，哈哈！



[slide]

## 小工具&浏览器插件

* cmder {:&.fadeIn}
* Wox
* Everything
* Chrome Plugins

[slide]
##[cmder](http://cmder.net/)

Windows 自带的命令行是非常弱的， ls、ssh、ps、grep、VIM  之类特别常用的命令都没有。

<br/>		
		
cmder 提供了很多常用的 Linux 命令，同时也提供了很多增强功能,比如新开 tab、分屏。	

<br/>			
	
<br/>	
linux 下 bash 的快捷键大多都可以使用, 比如 清屏 ctrl + l, ctrl + u, 甚至是历史搜索 ctrl + r 。		
		
###颜值也比 Window cmd 高很多很多哦！		

[slide]
		
![](http://veryyoung.u.qiniudn.com/cmder-main.jpg)		

[slide]
	
![](http://veryyoung.u.qiniudn.com/20151026195931.png)


[slide]
##[Wox](https://www.getwox.com/)

Launcher 的主要作用之一就是快速定位并启动应用程序，还可以当，定位文件，打开网页，Google 搜索等， 是使用 Mac 的必备软件。		
		
		
<br/>		
Mac 平台有很多成熟的 Launcher，比如 Alfred、Quicksilver，甚至是 QQ 自带的 Swiftly（俗称 double command）。		
	
[slide]		
###下面是一个典型的 Launcher		
		
<br/>			
![](http://ww2.sinaimg.cn/large/644eac00gw1e8hp0flg1dj20bw09ajry.jpg)

[slide]			
		
Windows 下也有 Launcher 啦！		

<br/>		

它就是 Wox。	
	
<br/>		

Wox 是国人开发的一款开源 Windows Launcher，代码维护在 [https://github.com/qianlifeng/Wox](https://github.com/qianlifeng/Wox)		
	
[slide]					
		
![](http://veryyoung.u.qiniudn.com/wox_preview.5098c3ba.jpg)	

	
[slide]			

###用法和 Mac 下的 Launcher 差不多，同时也支持插件

<br/>
		
![](http://ww3.sinaimg.cn/large/5d7c1fa4gw1eehedzwcwqj20et09xq3n.jpg)		
		
[slide]	
	
![](http://veryyoung.u.qiniudn.com/movie-d9daa479-6c37-4de1-b0dc-4e264266b3e9.gif)


[slide]

##[Everything](http://www.voidtools.com/)


Everything 是一款很牛的文件搜索软件， 速度飞快，支持正则表达式。


[slide style="background-image:url('http://veryyoung.u.qiniudn.com/everything-hadoop.gif')"]


[slide]

##[Chrome Plugins](https://chrome.google.com/webstore/category/extensions?hl=zh-CN)

<br/>

###Chrome 提供了丰富的插件来增强功能。

[slide]

###[Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)

Postman 是调试 web api 的一款利器，它能够发送任何类型的 HTTP requests (GET, HEAD, POST, PUT..)，附带任何数量的参数+ headers。

<br/>

支持不同的认证机制（basic, digest, OAuth），接收到的响应语法高亮（HTML，JSON或XML）。

<br/>

Postman 能够保留了历史的请求，这样我们就可以很容易地重新发送请求，有一个“集合”功能，用于存储所有请求相同的API/域。


[slide]

###[uBlock Origin](https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm)

<br/>

uBlock Origin 是一款高效的网络请求过滤工具，占用极低的内存和 CPU。

<br/>

用 Chrome 的人或多或少会用过 AdBlock，可以挡住那些烦人的广告（主要是网盟广告），but， AdBlock会让电脑一直烫烫烫啊，uBlock Origin完美解决这个问题。


[slide]

###[FeHelper](https://chrome.google.com/webstore/detail/web前端助手fehelper/pkgccpejnmalmdinmhkkfafefagiiiad)

<br/>

提供了很多常用的FE工具，包括字符串编解码、图片base64编码、代码压缩、美化、JSON格式化、正则表达式、时间转换工具、二维码生成器、编码规范检测、页面性能检测、栅格检测、JS运行效率分析等。

<br/>

非常实用，强烈推荐！


[slide]

###[划词翻译](https://chrome.google.com/webstore/detail/划词翻译/ikhdkkncnoglghljlkmcimlnlhkeamad)

<br/>

一个简便但强大的翻译扩展。

<br/>

支持谷歌、百度、有道、必应四大翻译和朗读引擎，可以方便的查看、复制和朗读不同引擎的翻译结果。

<br/>

对阅读英文文档非常有帮助。

[slide]

###[新浪微博图床](https://chrome.google.com/webstore/detail/新浪微博图床/fdfdnfpdplfbbnemmmoklbfjbhecpnhf)

<br/>

简单好用的新浪微博图床,支持选择/拖拽/粘贴上传图片,并生成图片地址,HTML和Markdown三种格式,并且可以浏览历史记录。

[slide]

###[HTTPS Everywhere](https://www.eff.org/HTTPS-EVERYWHERE)

<br/>

https 会对信息加密，保护到用户的隐私，避免钓鱼等。

<br/>

HTTPS Everywhere会将带有 http 链接重定向到 https（如果有）链接。


[slide]

##虚拟化&容器

* Vagrant {:&.fadeIn}
* Docker
* 对比