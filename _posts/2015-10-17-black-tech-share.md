---
layout: post
title: ”黑科技“技术分享
date: 2015-10-17 20:31:13
author: VERYYOUNG
comments: true
categories: [Share]
---

我是90后，准确的来说是92年出生，可能是在场人员中最小的一个。

90后的一个很显著的特点就是兴趣点很丰富，有时候会很奇特，容易喜欢上一些稀奇古怪的东西，比如：

这种

![](http://veryyoung.u.qiniudn.com/exo-ot12.png)

这种

![](http://veryyoung.u.qiniudn.com/bb75651910117a031792ac08b9a0c4ff1433225803.jpg)

还有这种

![](http://veryyoung.u.qiniudn.com/113980707767589384o.jpg)


我当然不是来分享这些的，哈哈。

我来分享的是我做为90后程序员所接触到的一些东西，一些看起来很奇特的东西。

进入正题。


-----

我今天给大家分享的主题是“黑科技”，什么是黑科技呢？

来看看 WIKI 的解释：

>黑科技是在《全金属狂潮》中登场的术语，原意指倾听者所拥有，但是非人类自力研发；凌驾于人类现有的科技之上的知识，引申为以人类现有的世界观无法理解的猎奇物。 也可泛指某些技术宅自制的杀伤性科技,例如激光枪，电磁炮，原子弹等。

>黑科技:远超越现今人类科技或知识所能及的范畴，其科学技术或者产品缺乏科学根据且违反自然原理。


我说的黑科技当然不是这些，我下面分享的所谓的“黑科技”大部分指的是一些比较优雅、快捷的开发工具、框架，还有可能是一些好玩的，或者能提高工作效率的小工具。


大部分都是比较新颖的东西，而且有很多背景色都是黑色的，哈哈。


----


下面会介绍到很多东东，每种东西我只是很简单的介绍一下，不会深讲。

第一是因为时间的限制，第二是很多我也只是接触了一点皮毛，让我深入的讲我也讲不了，哈哈！

提到的东西很多，我会尽量把他们连起来。



正式开始了。

-----

##1.	命令行。

命令行是大家每天都在用的东西，自然称不上什么黑科技。
	
但感觉大家现在比较依赖 GUI，基本是能用 GUI 全用了。
	
然而，命令行是程序员最好的朋友！
	
命令行能让程序员知道自己想要什么，明白自己在做什么，也会为自己的行为负责。
	
命令行会明确的告诉你它正在工作的每个细节，而不是
	
![](http://veryyoung.u.qiniudn.com/windows-busy.jpg)
	
还有一个比较大的优点就是，命令行能自由的组合使用，而 GUI 工具就比较难了，这个就不用解释了。
	
对了，还有一个特别重要的原因是除了开发环境，其他环境都是 Linux了，你能依赖的只有命令行。
	
	
当然命令行也有很多缺点，比如重复化、不方便、学习成本高、低效、有些活甚至完全没法完成，比如图形、图表、视频等。
	
##2.	OSX

OSX 是程序员最喜欢的操作系统。

OSX 最大的优点就是保留了命令行，同时提供了最好的 GUI 支持。

主要缺点有两个。

第一是软件缺失：很多小众软件没有提供 OSX 版，玩游戏也特别不方便。

第二个缺点，也是最大的缺点就是， OSX 只能跑在苹果电脑上。

而总所周知，苹果电脑最大的缺点就是：贵！贵！贵！


##3.	[Vagrant](https://www.vagrantup.com/)

>Create and configure lightweight, reproducible, and portable development environments.

上面这段话来自 Vagrant 官网，我翻译一下：创建和配置轻量级的，可重复的，可移植的开发环境。

通俗点说就是，我们可以通过 Vagrant 封装一个 Linux 的开发环境，分发给团队成员。成员可以在自己喜欢的桌面系统（Mac/Windows/Linux）上开发程序，代码却能统一在封装好的环境里运行，非常霸气。

Vagrant 是一款用来构建虚拟开发环境的工具，非常适合 php/python/ruby/java 这类语言开发 web 应用，“代码在我机子上运行没有问题”这种说辞将成为历史。



Vagrant 使用起来非常简单：

	vagrant init # 初始化
	vagrant up   # 启动
	 
That's all!

![](http://veryyoung.u.qiniudn.com/20151017201834.png)


##4.	[Docker](https://www.docker.com/)

>An open platform for distributed applications for developers and sysadmins

给开发人员和系统管理员提供的分布式应用开放平台。

我们来看看程序员在搭建开发环境时遇到的一些问题：

1.	重复操作：同一个软件在不同的环境得分别安装和配置一次。
2.	隔离性差：例如同一个 Mysql 如果权限管理不好很有可能误删别人的数据、不同的开发人员如果在同一台主机环境下共享开发，虽然是用户隔离，但端口如果不规范可能会冲突（我们现在貌似全是 root，更容易出问题）；
3.	可移植性差：例如和生产环境不一致、开发人员之间也无法共享、更严重的情况是当有新人入职时，通常需要又折腾一遍开发环境，无法快速搭建。

对开发和运维人员来说，最希望的就是一次创建或配置，可以在任意地方正常运行。

开发者可以使用一个标准的镜像来构建一套开发容器，开发完成之后，运维人员可以直接使用这个容器来部署代码。 Docker 可以快速创建容器，快速迭代应用程序，并让整个过程全程可见，使团队中的其他成员更容易理解应用程序是如何创建和工作的。 

Docker 容器很轻很快！容器的启动时间是秒级的，大量地节约开发、测试、部署的时间。

Docker 的基础是 Linux 容器（LXC）等技术。

在 LXC 的基础上 Docker 进行了进一步的封装，让用户不需要去关心容器的管理，使得操作更为简便。用户操作 Docker 的容器就像操作一个快速轻量级的虚拟机一样简单。

Docker Container 是可重用的，依赖于版本化机制，你很容易重用别人的 Container（叫Image），作为基础版本进行扩展，甚至像 Git 那样进行合并多个 Image；


简单来说，Docker 技术允许你在容器中运行你的应用（这有点类似于虚拟机，但是事实上还是有很大的区别），从而确保该应用所需要的所有库和包能够在任何情况下都有效运行，而不管你将他们跑在什么样的机器上。


给个 Docker 的例子

用 Docker 构建一个 Java 的编译环境，包括 Ubuntu、Jdk、Maven、SVN 。

Jdk、Maven 需要手动下载，下载之后分别为

jdk-8u51-linux-x64.gz、apache-maven-3.3.3-bin.tar.gz

创建一个 Dockerfile 文件，包含以下内容

	FROM ubuntu
	RUN apt-get update
	RUN apt-get -y install subversion
	ADD jdk-8u51-linux-x64.gz /usr/local
	ADD apache-maven-3.3.3-bin.tar.gz /usr/local
	ENV JAVA_HOME /usr/local/jdk1.8.0_51
	ENV M2_HOME /usr/local/apache-maven-3.3.3
	ENV PATH $PATH:$JAVA_HOME/bin:$M2_HOME/bin

简单的说一下上面的意思，就是基于 Ubuntu 创建一个镜像，然后更新软件源，接着安装 SVN，然后把下载的 Jdk、Maven 添加到镜像，并放置到 /usr/local目录，这里我添加的是一个压缩包，在构建镜像的适合，系统会自动解压，并且镜像里面也不会有压缩的文件，最后再设置环境变量。

构建：
	
	docker build -t dev 

运行
	
	sudo docker run -p 8080:8080 dev

然后可以在浏览器访问 localhost:8080 了。


###和 Vagrant 对比

Vagrant 是一款管理虚拟机的工具，而 Docker 是一款通过将应用打包到轻量级容器，而实现构建和部署的工具。两者适用范围不同。一个容器就是一个包含了应用执行所依赖的数据(包括lib，配置文件等等)。它可以保证应用在一个可重复的环境中随时执行。

如果你仅仅是想管理虚拟机，那么你应该使用 Vagrant。如果你想快速开发和部署应用，那么应该使用 Docker。


Vagrant 和 Docker 并不是相互竞争，而是互补的关系。

上次去听了公司内部的一个 Docker 分享，他们的做法是把 Docker 通过各种 Hack 的方法改成了一个虚拟机，个人感觉还不如直接用 Vagrant！！


-----


下面会介绍几款软件来增强 Windows... 



##5.	[cmder](http://cmder.net/)

Windows 自带的命令行是非常弱的， ls、ssh、ps、grep、VIM  之类特别常用的命令都没有。

cmder 提供了很多常用的 Linux 命令，同时也提供了很多增强功能。

比如新开 tab、分屏。

linux 下 bash 的快捷键大多都可以使用, 比如 清屏 ctrl + l, ctrl + u, 甚至是历史搜索 ctrl + r 。

颜值也比 Window cmd 高很多很多哦！

![](http://veryyoung.u.qiniudn.com/cmder-main.jpg)

![](http://veryyoung.u.qiniudn.com/20151026195931.png)


##6.	[Wox](https://www.getwox.com/)

Launcher 的主要作用之一就是快速定位并启动应用程序，还可以当做计算器，定位文件，打开网页，Google 搜索等， 是使用 Mac 的必备软件。

Mac 平台有很多成熟的 Launcher，比如 Alfred、Quicksilver，甚至是 QQ 自带的 Swiftly（俗称 double command）。

下面是一个典型的 Launcher

![](http://ww2.sinaimg.cn/large/644eac00gw1e8hp0flg1dj20bw09ajry.jpg)

Windows 下也有 Launcher 啦！

它就是 Wox。

Wox 是国人开发的一款开源 Windows Launcher，代码维护在 [https://github.com/qianlifeng/Wox](https://github.com/qianlifeng/Wox)

长这样：

![](http://veryyoung.u.qiniudn.com/wox_preview.5098c3ba.jpg)

用法和 Mac 下的 Launcher 差不多，同时也支持插件，比如这样：

![](http://ww3.sinaimg.cn/large/5d7c1fa4gw1eehedzwcwqj20et09xq3n.jpg)

或者这样：

![](http://veryyoung.u.qiniudn.com/movie-d9daa479-6c37-4de1-b0dc-4e264266b3e9.gif)


##7.	[Everything ](http://www.voidtools.com/)

Windows 自带的搜索卡得令人发指。

Everything 是一款很牛的文件搜索软件， 速度飞快，支持正则表达式。

来个测试！

比如我想找个 hadoop 的例子

这下子快到令人发指了！

![](http://veryyoung.u.qiniudn.com/everything-hadoop.gif)