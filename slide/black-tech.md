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

<br/>

* Vagrant {:&.fadeIn}
* Docker
* 对比

[slide]

##[Vagrant](https://www.vagrantup.com/)

<br/>

>Create and configure lightweight, reproducible, and portable development environments.

[slide]

创建和配置轻量级的，可重复的，可移植的开发环境。

<br/>

通俗点说就是，我们可以通过 Vagrant 封装一个 Linux 的开发环境，分发给团队成员。成员可以在自己喜欢的桌面系统（Mac/Windows/Linux）上开发程序，代码却能统一在封装好的环境里运行，非常霸气。

<br/>

Vagrant 是一款用来构建虚拟开发环境的工具，非常适合 php/python/ruby/java 这类语言开发 web 应用，“代码在我机子上运行没有问题”这种说辞将成为历史。

[slide]

Vagrant 使用起来非常简单：

<br/>

<pre><code class="markdown">

	vagrant init # 初始化
	vagrant up   # 启动
	
</code></pre>
	 
	 
<br/>
	 
###That's all!

[slide]

![](http://veryyoung.u.qiniudn.com/20151017201834.png)


[slide]

##[Docker](https://www.docker.com/)

<br/>

>An open platform for distributed applications for developers and sysadmins


[slide]

我们来看看程序员在搭建开发环境时遇到的一些问题

<br/>

* 重复操作：同一个软件在不同的环境得分别安装和配置一次。 {:&.rollIn}
* 隔离性差：例如同一个 Mysql 如果权限管理不好很有可能误删别人的数据、不同的开发人员如果在同一台主机环境下共享开发，虽然是用户隔离，但端口如果不规范可能会冲突（我们现在貌似全是 root，更容易出问题）；
* 可移植性差：例如和生产环境不一致、开发人员之间也无法共享、更严重的情况是当有新人入职时，通常需要又折腾一遍开发环境，无法快速搭建。


[slide]

对开发和运维人员来说，最希望的就是一次创建或配置，可以在任意地方正常运行。

<br/>

开发者可以使用一个标准的镜像来构建一套开发容器，开发完成之后，运维人员可以直接使用这个容器来部署代码。 

<br/>

Docker 可以快速创建容器，快速迭代应用程序，并让整个过程全程可见，使团队中的其他成员更容易理解应用程序是如何创建和工作的。 

[slide]

Docker 的基础是 Linux 容器（LXC）等技术。

<br/>

在 LXC 的基础上 Docker 进行了进一步的封装，让用户不需要去关心容器的管理，使得操作更为简便。用户操作 Docker 的容器就像操作一个快速轻量级的虚拟机一样简单。

<br/>


Docker Container 是可重用的，依赖于版本化机制，你很容易重用别人的 Container（叫Image），作为基础版本进行扩展，甚至像 Git 那样进行合并多个 Image。

[slide]

简单来说，Docker 技术允许你在容器中运行你的应用（这有点类似于虚拟机，但是事实上还是有很大的区别），从而确保该应用所需要的所有库和包能够在任何情况下都有效运行，而不管你将他们跑在什么样的机器上。

[slide]

给个 Docker 的例子

<br/>

用 Docker 构建一个 Java 的编译环境，包括 Ubuntu、Jdk、Maven、SVN 。

<br/>

Jdk、Maven 需要手动下载，下载之后分别为

<br/>

jdk-8u51-linux-x64.gz、apache-maven-3.3.3-bin.tar.gz

<br/>

[slide]

创建一个 Dockerfile 文件，包含以下内容

<pre><code class="markdown">

	FROM ubuntu
	RUN apt-get update
	RUN apt-get -y install subversion
	ADD jdk-8u51-linux-x64.gz /usr/local
	ADD apache-maven-3.3.3-bin.tar.gz /usr/local
	ENV JAVA_HOME /usr/local/jdk1.8.0_51
	ENV M2_HOME /usr/local/apache-maven-3.3.3
	ENV PATH $PATH:$JAVA_HOME/bin:$M2_HOME/bin
	
</code></pre>


[slide]


简单的说一下上面的意思，就是基于 Ubuntu 创建一个镜像，然后更新软件源，接着安装 SVN，然后把下载的 Jdk、Maven 添加到镜像，并放置到 /usr/local目录，这里我添加的是一个压缩包，在构建镜像的适合，系统会自动解压，并且镜像里面也不会有压缩的文件，最后再设置环境变量。

[slide]

构建：

<pre><code class="markdown">
	
	docker build -t dev 

</code></pre>

运行

<pre><code class="markdown">
	
	sudo docker run -p 8080:8080 dev

</code></pre>

然后可以在浏览器访问 localhost:8080 了。


[slide]

##和 Vagrant 对比

<br/>

Vagrant 是一款管理虚拟机的工具，而 Docker 是一款通过将应用打包到轻量级容器，而实现构建和部署的工具。两者适用范围不同。一个容器就是一个包含了应用执行所依赖的数据(包括lib，配置文件等等)。它可以保证应用在一个可重复的环境中随时执行。

<br/>

如果你仅仅是想管理虚拟机，那么你应该使用 Vagrant。如果你想快速开发和部署应用，那么应该使用 Docker。

<br/>

Vagrant 和 Docker 并不是相互竞争，而是互补的关系,你甚至可以把 Docker 跑在 Vagrant 上。

[slide]

上次去听了公司内部的一个 Docker 分享，他们的做法是把 Docker 通过各种 Hack 的方法改成了一个虚拟机。

<br/>

感觉就是一个有 Docker 优点（秒级启动、版本控制）的 Vagrant ！
 
