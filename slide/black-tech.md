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

```

	vagrant init # 初始化
	vagrant up   # 启动
	
```
	 
	 
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

```

	FROM ubuntu
	RUN apt-get update
	RUN apt-get -y install subversion
	ADD jdk-8u51-linux-x64.gz /usr/local
	ADD apache-maven-3.3.3-bin.tar.gz /usr/local
	ENV JAVA_HOME /usr/local/jdk1.8.0_51
	ENV M2_HOME /usr/local/apache-maven-3.3.3
	ENV PATH $PATH:$JAVA_HOME/bin:$M2_HOME/bin
	
```


[slide]


简单的说一下上面的意思，就是基于 Ubuntu 创建一个镜像，然后更新软件源，接着安装 SVN，然后把下载的 Jdk、Maven 添加到镜像，并放置到 /usr/local目录，这里我添加的是一个压缩包，在构建镜像的适合，系统会自动解压，并且镜像里面也不会有压缩的文件，最后再设置环境变量。

[slide]

构建：

```
	
	docker build -t dev 

```

运行

```
	
	sudo docker run -p 8080:8080 dev

```

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
 
 
[slide]

## 代码管理&构建

<br/>

* Git {:&.fadeIn}
* Gradle
* Travis 

[slide]

##[Git](https://git-scm.com/)

<br/>

Git 是 Lunus 大爷的第二个伟大作品。

<br/>

第一个伟大作品是什么？

<br/>

大名鼎鼎的 Linux！ {:&.zoomIn}

<br/>

[slide]

Lunus 是一个非常有个性的人，可以从两个 F**K 事件中体现出来。

<br/>

第一个事件：网传 Lunus 的简历上只有一行字：I created Lunus and fuck you

<br/>

第二个事件：Lunus 对英伟达对 Linux 平台没有提供足够的支持表示不满，在某大学演讲的时候公开的对 NVIDIA 竖起了中指，并说：“这是一个我们从未合作过的垃圾公司”


[slide style="background-image:url('http://veryyoung.u.qiniudn.com/2e03fad339338ced760ab3f2ec1d5858.png')"]


[slide]

Linus 虽然创建了 Linux，但 Linux 的壮大是全球开源贡献者的成果。

<br/>

Lunus 大爷是坚定的 CVS 反对者，他也同样地反对 SVN。

<br/>

在2002年以前，世界各地的志愿者把源代码文件通过diff的方式发给Linus，然后由Linus本人通过手工方式合并代码。

<br/>

随着项目的慢慢壮大，手工的方式越来越难以管理了，Linus 引进了一款叫做 BitKeeper 的代码管理工具。

[slide]

Lunux 的开发者都是大神，有人尝试着破解 BitKeeper，被发现了。

<br/>

BitKeeper 向 Linux 收回授权。

<br/>

Lunus 大爷怒了，三天就完成了一款代码管理工具的开发，这就是大名鼎鼎的 Git，一个月后，Linux 的代码已经托管在 Git 上了。

[slide]

Git 是分布式的版本控制工具，分布式意味着每个开发人员可以从中心版本库/服务器上 clone 一份到 local。

<br/>

在 local 可以随意折腾，各种新建分支，切换分支，暂存，stash，merge，等到必要的时候再 push 到 origin。

<br/>


[slide]

经常有这样的事情发生，当你正在进行项目中某一部分的工作，里面的东西处于一个比较杂乱的状态，而你想转到其他分支上进行一些工作。问题是，你不想提交进行了一半的工作，否则以后你无法回到这个工作点。

<br/>


比较 low 的一种方案是  commit 到 local，然后 再 checkout 到 other branch。

<br/>

这种方案不太建议，每个 commit 最好要是有意义的，可用的。

<br/>

[slide]

Git  的解决方案就是：git stash命令。

<br/>

Git stash 暂存你当时的状态，然后你可以切换到其它地方做任何你想做的事情。

<br/>

等你忙完别的再切回来继续处理。

<br/>

而 svn 只能 commit 到 origin（这时候代码是乱的，可能编译都通过不了，会气死其他同事的），或者 copy 本地修改，手工维护。


[slide]

Git review 代码会更加的方便， 你可以 fork 一份别人的代码，你并木有 push 权限，你只能先 push 到自己的分支，然后对别人的项目发起一个 pull request，由项目管理员来决定是否 merge。

<br/>

给开源项目贡献代码就是这样干的！


[slide]

###总结下 Git 相对于 SVN 的优点：

<br/>

1.	离线操作;
2.	公共服务器压力和数据量小;
3.	分支操作方便（SVN 的分支是 copy 一份， 而 Git 的分支切换只是简单的移动 HEAD 指针）;
4.	暂存;
5.  快;
6.	更智能的追踪变化，Git 采用基于文件内容的源码跟踪，而 SVN 只是基于文件名。rename 之后 svn 将无法追踪，也无法
merge。


[slide]

###当然 Git 也有缺点：

<br/>

1.	学习周期长;
2.	不能按目录进行权限划分（据说可以通过第三方工具来实现）;

[slide]

###使用现状：

<br/>

Git 的最流行的使用者 GitHub 全面压制 SVN 的最大使用者 Google Code，Google Code 已被遗弃，提供一键转换到 GitHub 的功能。

<br/>

绝大大部分开源项目都活跃在 GitHub 上。

<br/>

各大 PaaS 服务商也在慢慢放弃 SVN 。

<br/>

据个人了解，国内的大公司，BAT 一般老项目继续使用 SVN，新项目都转向了 Git。

<br/>

比较年轻的中大型团队，如 Qunar、美团、豆瓣，全部采用 Git。

<br/>

创业团队绝大部分用 Git。


[slide]
##[Gradle](http://gradle.org/)

现在我们用的构建工具主要是 Maven，其实在 Maven 之前还有一种东东，叫 Ant。

Ant 非常的灵活，你可以在 build.xml 里面编写任何你想要的东西。

缺点就是基于 xml 的语法非常啰嗦，难以管理，难以编写。

我刚开始写程序的时候用的是 Ant，反正那语法我一点映像都没有了，我都是从网上找个 build.xml 的例子，然后对着例子建好目录结构。

这个其实就有点 “约定优于配置” 的意思了。

[slide]
约定优于配置（convention over configuration），也称作按约定编程，是一种软件设计范式，旨在减少软件开发人员需做决定的数量，获得简单的好处，而又不失灵活性。

如果您所用工具的约定与你的期待相符，便可省去配置；反之，你可以配置来达到你所期待的方式。

[slide]

写 Java 难免要管理一系列的 xml 文件，很麻烦，很难调试。

[Ruby On Rails](https://zh.wikipedia.org/wiki/Ruby_on_Rails) 这个 Ruby 的框架将约定优于配置这个理念发挥到了极致。 

你只要按照约定在对应的地方添代码就行，其他的 Rails 都帮你做好了，再加上 Ruby 这种优雅简洁的语法，开发效率要比 Java Web 快 N 多倍。

用 Java 做 Web 开发要学一堆的开源框架，Ruby 一个 Ruby On Rails 全部搞定！

[slide]

Maven的整合这一概念，为项目提供合理的默认行为。

无需定制，源代码被默认放在${basedir}/src/main/java文件夹中，资源被默认放在 ${basedir}/src/main/resources文件夹中。测试默认放在 ${basedir}/src/test文件夹中，默认一个项目产生的JAR文件。Maven的默认您要编译的字节码到 ${basedir}/target/classes，然后在${basedir}/target文件夹中创建一个分发的JAR文件。

而相同的功能，Ant 得写一大串的 xml 文件。

</br>

Maven 很快席卷 Java 圈，几乎成了 Java Web 的标准构建工具了。

[slide]

然而每个项目都有自己的特定需求，标准做法必然是无法满足的。

</br>

比如目录更改，本地 Jar 包依赖，自定义操作等，Maven 本身没法完成，只能去写 Maven 插件。

</br>

扩展 Maven 对任何新手都是一件头疼的事，我们要学会编写插件，要搞清楚生命周期，这时，突然会唤起一丝丝对于 ANT 的怀念，虽然它做简单事不容易，但做复杂事却也没这么困难。

[slide]

Gradle 能完美的解决 Ant 和 Maven 带来的这些痛点。

</br>

Gradle 是其是结合了 Maven 和 Ant 双方优点的一种基于 Groovy DSL 的新式项目构建工具。而且由于是基于 Groovy 语言，所以语法上要比基于 XML 的 Maven 和 Ant 简洁许多，并且功能更加强大。 

[slide]

###它能提供的是：

</br>

1.	一个像 Ant 一样，通用的灵活的构建工具。
2.	一种可切换的，像 Maven 一样的基于约定的构建框架，却又从不锁住你。
3.	对多项目构建的强大支持。
4.	强大的依赖管理（基于Apache Ivy）。
5.	全力支持已有的 Maven 或者 Ivy 仓库基础建设。
6.	在不需要远程仓库或者 pom.xml 或者 ivy 配置文件的前提下，支持传递性依赖管理。
7.	兼容 Ant 任务。
8.	基于 Groovy 脚本构建。

[slide]

直接上一个 Gradle 的例子

<br/>

```
	buildscript {
		repositories {
			mavenCentral()
		}
		dependencies {
			classpath("org.springframework.boot:spring-boot-gradle-plugin:1.2.6.RELEASE")
		}
	}
	dependencies {
		compile("org.springframework.boot:spring-boot-starter-web") {
			exclude module: "spring-boot-starter-tomcat"
		}
		compile("org.springframework.boot:spring-boot-starter-security")
		compile("org.springframework.boot:spring-boot-starter-data-jpa")
		testCompile("mysql:mysql-connector-java:5.1.25")
	}
	
```

[slide]

就这么点代码，生成一个 Spring-Boot 项目，而基于 maven 的 pom.xml 得写 N 多行了，Ant 就更多了！

[slide]

Gradle 可以自定义任务

</br>

```
	task hello << {
		println "hello world"
	}

```

这样就定义了一个任务

[slide]

</br>

```
	gradle hello
	
```

</br>

就执行了。

</br>

Gradle 基于 Groovy 语言，你可以用 Groovy 去实现一系列复杂的操作，来代替掉 println "hello world" 。


[slide]

###使用现状：

</br>

Android 项目管理方面 Gradle 占有统治性地位，Android 新建项目已默认用 Gradle 管理了。

</br>

Java 项目大部分还是在用 Maven 管理，只有少部分比较 Geek 的团队已经切到 Gradle 了，比如 LinkedIn、Google...

[slide]
		
##谈到 Gradle 不得不说到 Groovy。		
		
Groovy 是 Java 平台上设计的面向对象编程语言。这门动态语言拥有类似 Python、Ruby 和 Smalltalk 中的一些特性，可以作为 Java 平台的脚本语言使用。		
		
Groovy 的语法与 Java 非常相似，以至于多数的 Java 代码也是正确的 Groovy 代码。Groovy 代码动态的被编译器转换成 Java 字节码。		
		
由于其运行在 JVM 上的特性，Groovy 可以使用其他Java语言编写的库。	

[slide] {:&.zoomIn}
		
Java 语法真的超级啰嗦，写过 Ruby、Python、PHP 这种动态脚本语言的人应该深有体会。

<br />

```	
for (int i = 0; i < 3; i++) {		
	System.out.println("Hello world");		
}	
		
```  


[slide]  {:&.zoomIn}

Groovy 可以这样写



```	
for (i in 0..2) {
	println 'Hello world' 
}
	
```	

	
或者

```	

3.times {
	println 'Hello world'
}

```	

[slide] 

可以不定义类型，Groovy 会智能的去判断类型。

```	
def coll = ["Groovy", "Java", "Ruby"]
assert  coll instanceof Collection
assert coll instanceof ArrayList

```	
[slide]

还有这种高端玩法：

```	
def numbers = [1,2,3,4]
assert numbers + 5 == [1,2,3,4,5]
assert numbers - [2,3] == [1,4]
	
def map=['name':'john','age':14,'sex':'boy']
map.each({ 
	println it.getKey() + "-->" + it.getValue()
	})

```	

[slide]

还有一些非常省代码的特性，比如

不需要 public 修饰符，不需要类型说明，不需要 getter/setter 方法，不需要 return....
	
Groovy 入门门槛非常低，能写 Java 的人随便看几分钟语法就可以动手写了，如果实在搞不定，直接上 Java 代码！

Groovy 的优点很明显，开发效率高；因为是动态语言，缺点也很明显，性能会差不少，大概会慢五倍左右。

但五倍的性能差距，在脚本语言越来越流行的今天，完全不是问题了，至少做 Web 开发没问题。

[slide]

使用现状：好像已经比较流行了，CRM 那边在用这个写脚本，旭日也打算推广 Groovy。

[slide]

##[Travis CI](https://travis-ci.org/)

Travis CI 是一个在线的，分布式的持续集成服务，用来构建及测试在 GitHub 托管的代码。


[slide]

Travis 是非常简单，只需要在代码根目录放置一个 .travis.ylm。

Travis 大多数时候无需显式定义流程，举例，如果有build.gradle 文件, Travis会理解它并使用 Gradle 编译它，测试等等。

它会侦查你的代码并采取相应动作，如果从 Ant 切换到 Maven 再到 Gradle，无需对 Travis 或其配置做任何改变。


使用 Travis，会让你忘记CI的存在. 无论什么时候将代码提交到仓库， Travis会发现并采取相应代码改变(包括 .travis.ylm). 如果有问题，你会收到 Email 通知。

[slide]

如果想做复杂的操作，也可以！

来看个 .travis.ylm 的例子（来自开源项目 [ES](https://github.com/zhangkaitao/es)）

[slide]

```	

	language: java
	
	env:
	- DB=mysql
	
	jdk:
	- openjdk7
	
	mysql:
	database: es
	username: root
	password :
	encoding: utf8
	
	install:
	- mvn install -Dmaven.test.skip=true
	
	before_script:
	- cd web
	- mvn clean
	- mvn db:create
	- mvn db:schema
	- mvn db:data
	- cd ..
	
	script:
	- cd common
	- mvn test
	- cd ..
	- cd web
	- mvn test -Pit
	
	
	
	notifications:
	email:
		- zhangkaitao0503@gmail.com

```	

[slide]

可以在网页上看到构建历史

![](http://veryyoung.u.qiniudn.com/20151206211547.png)

[slide]

以及构建详情

![](http://veryyoung.u.qiniudn.com/20151105203213.png)

详情包括对应的 commit 记录，以及详细的 构建 log (包括执行的每一条命令，以及命令执行之后的反应)。

[slide]

Travis 是基于 Vagrant 来管理环境的，用虚拟化技术的云化方案做成了云 CI。

[slide]

使用现状：目前大部分用于 GitHub 的开源项目的构建，很多知名的开源项目使用它来在每次提交的时候进行构建测试，比如 PHP、Ruby on Rails，Ruby 和 Node.js。

<br />

还没法用在非 GitHub 的项目上，不过 Travis CI 已经试图将这一成功的开源项目在企业层面复制，名字也想好了：Travis Pro。


[slide]

## 编辑器&IDE&IDE插件

<br/>

* 编辑器 {:&.fadeIn}
* IDEA
* IDE 插件 


[slide]

平时写一些简单的脚本、sql，甚至一些 note 的时候，上 IDE 肯定不行， 系统自带的编辑器往往弱爆了。

<br/>

VI(编辑器之神) 和 Emacs(神的编辑器) 入门成本有点高，但慢慢熟悉，再加上一些插件和配置之后，会变成大杀器：完全丢掉鼠标，双眼盯着屏幕，然后使劲的啪啪啪就行。

<br/>

然而学习成本实在太高，想熟练使用得花费巨大的精力，反正我自己是系统的学过好几次 VIM，但最后还是只会用 i、:q! 这些最基本的命令。

[slide]

![](http://veryyoung.u.qiniudn.com/horrorstories.txt.jpg)

[slide]

给大家推荐两个开源圈用的比较多的编辑器：[Sublime](https://www.sublimetext.com/)、[VS Code](https://code.visualstudio.com/)

<br/>

这两编辑器提供了类似 IDE 的很多功能，比如丰富的快捷键、查找、切换、文件切换、代码高亮、代码提升等，通过一些插件的配合可以用起来和 IDE 一样方便，但速度完爆 IDE。

<br/>

都是免费的，而且颜值高！

[slide]

![](http://veryyoung.u.qiniudn.com/sublime-show-1.gif)

[slide]


![](http://veryyoung.u.qiniudn.com/sublime-show-2.gif)

[slide]

![](http://veryyoung.u.qiniudn.com/sublime-show-3.gif)