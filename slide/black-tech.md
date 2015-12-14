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

## 没有深入、只有皮毛



[slide]

## 小工具&浏览器插件

<br/>

* cmder {:&.fadeIn}
* Wox
* Everything
* Chrome Plugins

[slide]
##[cmder](http://cmder.net/)

<br/>	

Windows 自带的命令行是非常弱的， ls、ssh、ps、grep、vim  之类特别常用的命令都没有。 {:&.fadeIn}

<br/>		
		
cmder 提供了很多常用的 Linux 命令，同时也提供了很多增强功能,比如新开 tab、分屏。 {:&.fadeIn}

<br/>			
	
Linux Bash 的快捷键大多都可以使用, 比如 清屏 ctrl+l, 历史搜索 ctrl+r 。	 {:&.fadeIn}	
	

[slide]
		
![](http://veryyoung.u.qiniudn.com/cmder-main.jpg)		

[slide]
	
![](http://veryyoung.u.qiniudn.com/20151213133203.png)


[slide]
##[Wox](https://www.getwox.com/)

<br />	

Launcher 的主要作用之一就是快速定位并启动应用程序，还可以当，定位文件，打开网页，Google 搜索等， 是使用 Mac 的必备软件	{:&.fadeIn}
		
<br />	
	
Mac 平台有很多成熟的 Launcher，比如 Alfred、Quicksilver，甚至是 QQ 自带的 Swiftly（俗称 double command） {:&.fadeIn}		
	
[slide]		
###下面是一个典型的 Launcher		
		
<br/>	
		
![](http://ww2.sinaimg.cn/large/644eac00gw1e8hp0flg1dj20bw09ajry.jpg)

[slide]			
		
Windows 下也有 Launcher 啦！		

<br/>		

它就是 Wox。 	{:&.fadeIn}
	
<br/>		

Wox 是国人开发的一款开源 Windows Launcher，代码维护在 [https://github.com/qianlifeng/Wox](https://github.com/qianlifeng/Wox) {:&.fadeIn}		
	
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

<br/>	

Everything 是一款文件搜索软件， 速度飞快，支持正则表达式。


[slide style="background-image:url('http://veryyoung.u.qiniudn.com/everything-hadoop.gif')"]


[slide]

##[Chrome Plugins](https://chrome.google.com/webstore/category/extensions?hl=zh-CN)

<br/>

###Chrome 提供了丰富的插件来增强功能。

[slide]

###[Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)

<br />	

Postman 是调试 Rest API 的一款利器  {:&.zoomIn}


[slide]

###[uBlock Origin](https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm)

<br/>

uBlock Origin 是一款高效的广告过滤工具，占用极低的内存和 CPU。 {:&.zoomIn}


[slide]

###[FeHelper](https://chrome.google.com/webstore/detail/web前端助手fehelper/pkgccpejnmalmdinmhkkfafefagiiiad)

<br/>

提供了很多常用的FE工具，包括字符串编解码、图片base64编码、代码压缩、美化、JSON格式化、正则表达式、时间转换工具、二维码生成器、编码规范检测、页面性能检测、栅格检测、JS运行效率分析等。 {:&.zoomIn}

<br/>

非常实用，强烈推荐！ {:&.zoomIn}


[slide]

###[新浪微博图床](https://chrome.google.com/webstore/detail/新浪微博图床/fdfdnfpdplfbbnemmmoklbfjbhecpnhf)

<br/>

简单好用的新浪微博图床,支持选择/拖拽/粘贴上传图片,并生成图片地址,HTML和Markdown三种格式,并且可以浏览历史记录。 {:&.zoomIn}

[slide]

###[HTTPS Everywhere](https://www.eff.org/HTTPS-EVERYWHERE)

<br/>

https 会对信息加密，保护到用户的隐私，避免钓鱼等。 {:&.zoomIn}

<br/>

HTTPS Everywhere会将带有 http 链接重定向到 https（如果有）链接。 {:&.zoomIn}


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

###创建和配置轻量级的，可重复的，可移植的开发环境。 

<br/>

通俗点说就是，我们可以通过 Vagrant 封装一个 Linux 的开发环境，分发给团队成员。成员可以在自己喜欢的任意桌面系统上开发程序，代码却能统一在封装好的环境里运行。  {:&.zoomIn}


[slide]

Vagrant 使用起来非常简单：

<br/>

```

vagrant init # 初始化

vagrant up   # 启动
	
```
	 

[slide]

![](http://veryyoung.u.qiniudn.com/20151213140722.png)


[slide]

##[Docker](https://www.docker.com/)

<br/>

>An open platform for distributed applications for developers and sysadmins


[slide]

我们来看看程序员在搭建开发环境时遇到的一些问题

<br/>

* 重复操作：同一个软件在不同的环境得分别安装和配置一次 {:&.rollIn}
* 隔离性差：不同的开发人员如果在同一台主机环境下共享开发，虽然是用户隔离，但端口如果不规范可能会冲突
* 可移植性差：例如和生产环境不一致、开发人员之间也无法共享、更严重的情况是当有新人入职时，通常需要又折腾一遍开发环境，无法快速搭建


[slide]

对开发和运维人员来说，最希望的就是一次创建或配置，可以在任意地方正常运行。

<br/>

开发者可以使用一个标准的镜像来构建一套开发容器，开发完成之后，运维人员可以直接使用这个容器来部署代码。 {:&.rollIn}

<br/>

Docker 可以快速创建容器，快速迭代应用程序，并让整个过程全程可见，使团队中的其他成员更容易理解应用程序是如何创建和工作的。  {:&.rollIn}

[slide]

Docker 的基础是 Linux 容器（LXC）等技术。

<br/>

在 LXC 的基础上 Docker 进行了进一步的封装，让用户不需要去关心容器的管理，使得操作更为简便。用户操作 Docker 的容器就像操作一个快速轻量级的虚拟机一样简单。 {:&.rollIn}

<br/>

Docker Container 是可重用的，依赖于版本化机制，你很容易重用别人的 Container（叫Image），作为基础版本进行扩展，甚至像 Git 那样进行合并多个 Image。 {:&.rollIn}

[slide]

Docker 技术允许你在容器中运行你的应用，从而确保该应用所需要的所有库和包能够在任何情况下都有效运行，而不管你将他们跑在什么样的机器上。 

[slide]

给个 Docker 的例子

<br/>

用 Docker 构建一个 Java 的编译环境，包括 Ubuntu、Jdk、Maven、SVN 。 {:&.rollIn}


[slide]

创建一个 Dockerfile 文件，包含以下内容

<br/>

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

构建

<br/>

```
	
docker build -t dev 

```

[slide]

运行

<br/>

```

sudo docker run -p 8080:8080 dev

```

[slide]

##和 Vagrant 对比

<br/>

Vagrant 是一款管理虚拟机的工具，而 Docker 是一款通过将应用打包到轻量级容器，而实现构建和部署的工具。两者适用范围不同。  {:&.rollIn}

<br/>

一个容器就是一个包含了应用执行所依赖的数据(包括lib，配置文件等等)。它可以保证应用在一个可重复的环境中随时执行。  {:&.fadeIn}

<br/>

如果你仅仅是想管理虚拟机，那么你应该使用 Vagrant。如果你想快速开发和部署应用，那么应该使用 Docker。  {:&.rollIn}

<br/>

[slide]

###Vagrant 和 Docker 并不是相互竞争，而是互补的关系, 完全可以把 Docker 跑在 Vagrant 上。

[slide]

上次去听了公司内部的一个 Docker 分享，他们的做法是把 Docker 通过各种 Hack 的方法改成了一个虚拟机。 

<br/>

一个有 Docker 优点（秒级启动、版本控制）的虚拟机！ {:&.zoomIn}
 
 
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


[slide]

Linus 虽然创建了 Linux，但 Linux 的壮大是全球开源贡献者的成果。

<br/>

Lunus 是 cvs 和 svn 的反对者。  {:&.fadeIn}

<br/>

早些时候源代码都是通过 diff 的方式发给 Linus，然后由 Linus 本人通过手工方式合并代码。 {:&.fadeIn}

<br/>

随着项目的慢慢壮大，手工的方式越来越难以管理了，Linus 引进了一款叫做 BitKeeper 的代码管理工具。 {:&.fadeIn}

[slide]

BitKeeper 向 Linux 收回授权。 

<br/>

Lunus 花了三天就完成了一款代码管理工具的开发，这就是大名鼎鼎的 Git，一个月后，Linux 的代码已经托管在 Git 上了。 {:&.fadeIn}

[slide]

Git 是分布式的版本控制工具，分布式意味着每个开发人员可以从中心版本库/服务器上 clone 一份到 local。

<br/>

在 local 可以随意折腾，各种新建分支，切换分支，暂存，stash，merge，等到必要的时候再 push 到 origin。 {:&.fadeIn}


[slide]

当你正在进行项目中某一部分的工作，里面的东西处于一个比较杂乱的状态，而你想转到其他分支上进行一些工作。

<br/>

svn 只能提交到远端，但这样可能会影响到其它成员。 {:&.fadeIn}

<br/>

不提交，在本地可能会丢失，而且最后积累成大的 commit 是不被版本控制工具建议的。 {:&.fadeIn}

[slide]
使用 Git ，可以随意的新建一个分支，commit 到 local

<br/>

或者用 Git stash 暂存你当时的状态，

<br/>

然后你可以切换到其它地方做任何你想做的事情。

<br/>

等你忙完别的再切回来继续处理。


[slide]

Git review 代码会更加的方便， 你可以 fork 一份别人的代码，你并木有 push 权限，你只能先 push 到自己的分支，然后对别人的项目发起一个 pull request，由项目管理员来决定是否 merge。

<br/>

###给开源项目贡献代码就是这样干的！


[slide]

###总结下 Git 相对于 SVN 的优点

<br/>

1.	离线操作; {:&.fadeIn}
2.	公共服务器压力和数据量小;
3.	分支操作方便（SVN 的分支是 copy 一份， 而 Git 的分支切换只是简单的移动 HEAD 指针）;
4.	暂存;
5.	更智能的追踪变化（Git 采用基于文件内容的源码跟踪，而 SVN 只是基于文件名。rename 之后 svn 将无法追踪，也无法
merge）。


[slide]

###当然 Git 也有缺点

<br/>

1.	学习周期长;
2.	不能按目录进行权限划分（据说可以通过第三方工具来实现）;

[slide]

###使用现状：

<br/>

Git 的最流行的使用者 GitHub 全面压制 SVN 的最大使用者 Google Code，Google Code 已被遗弃，提供一键转换到 GitHub 的功能。 {:&.fadeIn}

<br/>

绝大大部分开源项目都活跃在 GitHub 上。 {:&.fadeIn}

<br/>

各大 PaaS 服务商也在慢慢放弃 SVN 。 {:&.fadeIn}

<br/>

据个人了解，国内的大公司，BAT 一般老项目继续使用 SVN，新项目都转向了 Git。 {:&.fadeIn}

<br/>

比较年轻的中大型团队，如 Qunar、美团、豆瓣，全部采用 Git。 {:&.fadeIn}

<br/>

创业团队绝大部分用 Git。 {:&.fadeIn}


[slide]
##[Gradle](http://gradle.org/)

<br />

现在我们用的构建工具主要是 Maven，其实在 Maven 之前还有一种东东，叫 Ant。 {:&.fadeIn}

<br />

Ant 非常的灵活，你可以在 build.xml 里面编写任何你想要的东西。 {:&.fadeIn}

<br />

缺点就是基于 xml 的语法非常啰嗦，难以管理，难以编写。 {:&.fadeIn}

<br />

我刚开始写程序的时候用的是 Ant，反正那语法我一点映像都没有了，我都是从网上找个 build.xml 的例子，然后对着例子建好目录结构。{:&.fadeIn}

<br />

这个其实就有点 “约定优于配置” 的意思了。 {:&.fadeIn}

[slide]

约定优于配置（convention over configuration），也称作按约定编程，是一种软件设计范式，旨在减少软件开发人员需做决定的数量，获得简单的好处，而又不失灵活性。

<br />

如果您所用工具的约定与你的期待相符，便可省去配置；反之，你可以配置来达到你所期待的方式。 {:&.fadeIn}

[slide]

写 Java 难免要管理一系列的 xml 文件，很麻烦，很难调试。

<br />

[Ruby On Rails](https://zh.wikipedia.org/wiki/Ruby_on_Rails) 这个 Ruby 的框架将约定优于配置这个理念发挥到了极致。  {:&.fadeIn}

<br />

你只要按照约定在对应的地方添代码就行，其他的 Rails 都帮你做好了，再加上 Ruby 这种优雅简洁的语法，开发效率要比 Java Web 快 N 多倍。 {:&.fadeIn}



[slide]

Maven的整合这一概念，为项目提供合理的默认行为。

<br />

无需定制，源代码被默认放在${basedir}/src/main/java文件夹中，资源被默认放在 ${basedir}/src/main/resources文件夹中。  {:&.fadeIn}

<br />

测试默认放在 ${basedir}/src/test文件夹中，默认一个项目产生的JAR文件。  {:&.fadeIn}

<br />

Maven的默认您要编译的字节码到 ${basedir}/target/classes，然后在${basedir}/target文件夹中创建一个分发的JAR文件。  {:&.fadeIn}

<br />

而相同的功能，Ant 得写一大串的 xml 文件。  {:&.fadeIn}

</br>

Maven 很快席卷 Java 圈，几乎成了 Java Web 的标准构建工具了。 {:&.fadeIn}


[slide]

然而每个项目都有自己的特定需求，标准做法必然是无法满足的。

</br>

比如目录更改，本地 Jar 包依赖，自定义操作等，Maven 本身没法完成，只能去写 Maven 插件。 {:&.fadeIn}

</br>

扩展 Maven 对任何新手都是一件头疼的事，我们要学会编写插件，要搞清楚生命周期，这时，突然会唤起一丝丝对于 ANT 的怀念，虽然它做简单事不容易，但做复杂事却也没这么困难。 {:&.fadeIn}

[slide]

Gradle 能完美的解决 Ant 和 Maven 带来的这些痛点。

</br>

Gradle 是其是结合了 Maven 和 Ant 双方优点的一种基于 Groovy 的新式项目构建工具。  {:&.fadeIn}

<br />

而且由于是基于 Groovy 语言，所以语法上要比基于 XML 的 Maven 和 Ant 简洁许多，并且功能更加强大。 {:&.fadeIn}

[slide]

###它能提供的是

</br>

1.	一个像 Ant 一样，通用的灵活的构建工具。  {:&.fadeIn}
2.	一种可切换的，像 Maven 一样的基于约定的构建框架，却又从不锁住你。
3.	对多项目构建的强大支持。
4.	强大的依赖管理（基于Apache Ivy）。
5.	全力支持已有的 Maven 或者 Ivy 仓库基础建设。
6.	兼容 Ant 任务。
7.	基于 Groovy 脚本构建。

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

Gradle 可以自定义任务

</br>

```
	task hello << {
		println "hello world"
	}

```

[slide]

</br>

```
	gradle hello
	
```

</br>


</br>

Gradle 基于 Groovy 语言，你可以用 Groovy 去实现一系列复杂的操作，来代替掉 println "hello world" 。 {:&.fadeIn}

[slide]

Gradle 默认不支持 maven profile，但是基于 gradle 自定义任务很好解决。

[slide]

```
environments {
    dev {
        jdbc {
            url = 'jdbc:mysql://localhost:3306/test?zeroDateTimeBehavior=convertToNull'
            user = 'root'
            password = 'test'
        }
    }

    qa {
        jdbc {
            url = 'jdbc:mysql://localhost:3306/test?zeroDateTimeBehavior=convertToNull'
            user = 'root'
            password = 'test'
        }
    }

    product {
        jdbc {
            url = 'jdbc:mysql://localhost:3306/test?zeroDateTimeBehavior=convertToNull'
            user = 'root'
            password = 'test'
        }
    }
}


```

[slide]

```
jdbc.url=@jdbc.url@

jdbc.user=@jdbc.user@

jdbc.password=@jdbc.password@

```

[slide]

```
def loadConfiguration() {
   def profile = project.hasProperty('profile') ? project['profile'] : 'dev'

   println("Using profile: $profile")

   def configFile = file('config.groovy')
   new ConfigSlurper(profile).parse(configFile.toURL()).toProperties()
}

processResources {
   from(sourceSets.main.resources.srcDirs) {
       filter(org.apache.tools.ant.filters.ReplaceTokens, tokens: loadConfiguration())
   }
}

```


[slide]

###使用现状

</br>

Android 项目管理方面 Gradle 占有统治性地位，Android 新建项目已默认用 Gradle 管理了。 {:&.fadeIn}

</br>

Java 项目大部分还是在用 Maven 管理，只有少部分比较 Geek 的团队已经切到 Gradle 了，比如 LinkedIn、Google... {:&.fadeIn}


[slide]

##[Travis CI](https://travis-ci.org/)

</br>

Travis CI 是一个在线的，分布式的持续集成服务，用来构建及测试在 GitHub 托管的代码。


[slide]

Travis 使用非常简单，只需要在代码根目录放置一个 .travis.ylm。

</br>

Travis 大多数时候无需显式定义流程，举例，如果有build.gradle 文件, Travis会理解它并使用 Gradle 编译它，测试等等。 {:&.fadeIn}

</br>

它会侦查你的代码并采取相应动作，如果从 Ant 切换到 Maven 再到 Gradle，无需对 Travis 或其配置做任何改变。 {:&.fadeIn}

</br>

使用 Travis，会让你忘记CI的存在. 无论什么时候将代码提交到仓库， Travis会发现并采取相应代码改变(包括 .travis.ylm). 如果有问题，你会收到 Email 通知。 {:&.fadeIn}

[slide]

如果想做复杂的操作，也可以！

</br>

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

</br>

![](http://veryyoung.u.qiniudn.com/20151206211547.png)

[slide]

以及构建详情

</br>

![](http://veryyoung.u.qiniudn.com/20151105203213.png)

</br>

详情包括对应的 commit 记录，以及详细的 构建 log (包括执行的每一条命令，以及命令执行之后的反应)。

[slide]

Travis 是基于 Vagrant 来管理环境的，用虚拟化技术的云化方案做成了云 CI。

[slide]

使用现状：目前大部分用于 GitHub 的开源项目的构建，很多知名的开源项目使用它来在每次提交的时候进行构建测试，比如 PHP、Ruby on Rails，Ruby 和 Node.js。

<br />

还没法用在非 GitHub 的项目上，不过 Travis CI 已经试图将这一成功的开源项目在企业层面复制，名字也想好了：Travis Pro。 {:&.fadeIn}


[slide]

## 编辑器&IDE&IDE插件

<br/>

* 编辑器 {:&.fadeIn}
* IDEA
* IDE 插件 


[slide]

编辑器可以完成大部分的开发工作

<br/>

VI(编辑器之神) 和 Emacs(神的编辑器) 入门成本有点高，但慢慢熟悉，再加上一些插件和配置之后，会变成大杀器：传说中的键盘党。 {:&.fadeIn}


[slide]

![](http://veryyoung.u.qiniudn.com/horrorstories.txt.jpg)

[slide]

给大家推荐两款编辑器：[Sublime](https://www.sublimetext.com/)、[VS Code](https://code.visualstudio.com/)

<br/>

这两编辑器提供了类似 IDE 的很多功能，比如丰富的快捷键、查找、切换、文件切换、代码高亮、代码提升等，通过一些插件的配合可以用起来和 IDE 一样方便，但速度完爆 IDE。


[slide]

![](http://veryyoung.u.qiniudn.com/sublime-show-1.gif)

[slide]


![](http://veryyoung.u.qiniudn.com/sublime-show-2.gif)

[slide]

![](http://veryyoung.u.qiniudn.com/sublime-show-3.gif)

[slide]

![](http://veryyoung.u.qiniudn.com/20151214205422.png)

[slide]

![](http://veryyoung.u.qiniudn.com/20151214205502.png)

[slide]

##[IDEA](https://www.jetbrains.com/idea/)

<br/>

>The Most Intelligent Java IDE

<br/>

IDEA 是 Jetbrains 家的一款优秀的代表作，除了 IDEA 之外，他家还有 PhpStorm、PyCharm、RubyMine、WebStorm、CLion、ReSharper、Android Studio 等这几款分别在各自领域做到最好的 IDE。 {:&.fadeIn}
[slide]

CSDN 对这款产品有[非常详细的介绍](http://mall.csdn.net/product/623)。

<br/>

个人总结一下就是

<br/>

1.	快、即时； {:&.fadeIn}
2.	丰富的插件；
3.	对新东西支持非常好；
4.	Cool！
5.	智能！智能！智能！


[slide]

##缺点还是有的

<br/>

1.	占内存（IDEA 为了提供即时的、智能的提示，会在后台做很多索引和运算） {:&.fadeIn}
2.	贵！（目前的售价是 499刀/年）；

[slide]

使用情况

<br/>

因为价格昂贵，再加上在 Eclipse 后面出来的，国内大公司用的不是很多，创业公司和个人开发者比较喜欢用这个，不过大部分也用得上盗版。 {:&.fadeIn}

<br/>

国外已经非常普及了，可能这和国外的消费观念有关。 {:&.fadeIn}

<br/>

2013 年 Google I/O 大会的时候，抛弃了合作已久的 Eclipse，选择了和 IDE 新贵 IDEA 合作，推出了 IDEA For Android，也就是 [Android Studio](https://developer.android.com/intl/zh-cn/tools/studio/index.html)   {:&.fadeIn}


<br/>

目前 Android Studio 已席卷 Android 圈，还在坚守 Eclipse 的 Android 开发者不多了。 {:&.fadeIn}

[slide]
## IDE插件

<br />

合理的安装和使用插件能显著提高编程效率


[slide]

## [CheckStyle](http://plugins.jetbrains.com/plugin/1065) 

<br />

通过检查对代码编码格式，命名约定，Javadoc，类设计等方面进行代码规范和风格的检查，从而有效约束开发人员更好地遵循代码编写规范。{:&.fadeIn}


[slide]

## [FindBugs](https://plugins.jetbrains.com/plugin/3847)

<br />

FindBugs 通过检查类文件或 JAR 文件，将字节码与一组缺陷模式进行对比从而发现代码缺陷，完成静态代码分析，可以找出常见的 bug 或者可能潜在 bug 的地方。 {:&.fadeIn}

[slide]


## [Jrebel](https://plugins.jetbrains.com/plugin/4441)

<br />

热部署神器，改完代码直接生效，不用重启啦！ {:&.fadeIn}

[slide]

## [CamelCase](https://plugins.jetbrains.com/plugin/7160)

<br />

可以切换变量命名风格，如 SogouInc、sogouInc、sogou—inc、SOGOU_INC {:&.fadeIn}

[slide]

##[RestClient](https://plugins.jetbrains.com/plugin/5951)

<br />

可用来调试 HTTP 接口，相当于 IDE 版的 POSTMAN {:&.fadeIn}

[slide]

## [CodeGlance](https://plugins.jetbrains.com/plugin/7275)

<br />

生成右侧代码缩略图，用过 Sublime 的肯定知道 ^_^ {:&.fadeIn}


[slide]

## [GsonFormat](https://plugins.jetbrains.com/plugin/7654)

<br />

把 Json 数据转为 Java 对象，很实用的！！！ {:&.fadeIn}

[slide]

## [AceJump](https://plugins.jetbrains.com/plugin/7086)

<br />

Emacs 用户肯定知道是干嘛的！！

<br />

所谓 AceJump，就是你按快捷键进入 AceJump 模式后（默认是 Ctrl+J），再按任一个字符，插件就会在屏幕中这个字符的所有出现位置都打上标签，你只要再按一下标签的字符，就能把光标移到该位置上。换言之，你要移动光标时，眼睛一直看着目标位置就行了，根本不用管光标的当前位置，非常舒服。 {:&.fadeIn}

[slide]

## [LiveEdit](https://plugins.jetbrains.com/plugin/7007)

<br />

Intellij IDEA 默认自动保存的，根本不用 Ctrl+S，LiveEdit 能自动更新浏览器里的网页，所以 F5 也省了 {:&.fadeIn}

如果是是双屏的话，基本上所敲即所得了。 {:&.zoomIn}


[slide]

## [Key Promoter](https://plugins.jetbrains.com/plugin/4455)

<br />

Key Promoter 会统计你用键盘或鼠标操作了某功能几次，对应的快捷键是啥，或者建议你给常用的功能绑定快捷键。{:&.fadeIn}


[slide]

#Java Jars

<br />

一些常用的 Java jar 包或者框架，能让 Java 编程变得优雅许多！

[slide]

##[Apache Commons](https://commons.apache.org/)

<br />

Apache Commons 我们或多或少用过一点，比如 StringUtils.isEmpty、CollectionUtils.isEmpty(). {:&.fadeIn}

<br />

Apache Commons 封装了一些常用的工具类，减少重复操作，比如字符串操作、IO 操作、集合增强等。 {:&.fadeIn}

[slide]

![](http://veryyoung.u.qiniudn.com/apache-commons.png)

[slide]

##举几个例子吧：

```
// 读取网页内容
InputStream in = new URL( "https://www.sogou.com" ).openStream();  
try {  
	System.out.println(IOUtils.toString(in));  
} finally {  
	IOUtils.closeQuietly(in);  
} 

//生成指定长度的字母和数字的随机组合字符串
RandomStringUtils.randomAlphanumeric(5); 

```

[slide]

##[Guava](https://code.google.com/p/guava-libraries/)

<br />

Guava 是 Google 出品的第三方工具库，功能和 Apache Commons 有点类似。 {:&.zoomIn}

<br />

Guava 做了很多数据结构的增强，比如不可变集合、多项映射的 Map 等。 {:&.zoomIn}

<br />

这个也同样建议系统的学习，能让 Java 编程变得优雅不少。 {:&.zoomIn}


[slide]

##[并发编程网](http://ifeve.com/) 有个不错的中文版教程: [Google Guava官方教程（中文版）](http://ifeve.com/google-guava/)


[slide]

##[javatuples](http://www.javatuples.org/)

<br />

编程过程中经常会遇到多个返回值的问题，通常返回一个 Array、集合（List、Set、Map）或自定义一个 Class。 {:&.zoomIn}

<br />

在很多语言中都提供元组类型 Tuple 的支持，比如 Scala、C++、.Net。 {:&.zoomIn}

[slide]

javatuples 是一个很简单的 lib，它没有什么华丽的功能，就是提供了支持返回多个元素的一些类。

<br />

```

Unit<A> (1 element)
Pair<A,B> (2 elements)
Triplet<A,B,C> (3 elements)
Quartet<A,B,C,D> (4 elements)
Quintet<A,B,C,D,E> (5 elements)
Sextet<A,B,C,D,E,F> (6 elements)
Septet<A,B,C,D,E,F,G> (7 elements)
Octet<A,B,C,D,E,F,G,H> (8 elements)
Ennead<A,B,C,D,E,F,G,H,I> (9 elements)
Decade<A,B,C,D,E,F,G,H,I,J> (10 elements)

```

[slide]

##[OkHttp](https://github.com/square/okhttp)

<br />

HttpClient 用起来挺麻烦的，语法啰嗦，拿到手肯定得自己再封装一次，而且一堆废弃的 api， not happy....  {:&.zoomIn}

<br />

OkHttp 是 HttpClient 的一个成熟的替代品！ {:&.zoomIn}

[slide]

```
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

```

[slide]

语法很简洁，几乎每一行代码都是有用的。 

<br />

同时支持 

<br />

1.	GZIP;  {:&.zoomIn}
2.	缓存，减少重复请求;
3.	SPDY；
4.	连接池；
5.	失败重试;

[slide]

##Android 官方推荐使用 OkHttp，同时在6.0删除了对 HttpClient 的内置。


[slide]

##[jsoup](http://jsoup.org/)

<br />

jsoup 是一款 Java 的 HTML 解析器，可直接解析某个 URL 地址的 HTML 文本内容。 {:&.fadeIn}

<br />

它提供了一套非常省力的 API，可通过 DOM，CSS 以及类似于 jQuery 的操作方法来取出和操作数据。 {:&.zoomIn}

[slide]

```

Document doc = Jsoup.connect("https://www.sogou.com/").get();
Elements newsHeadlines = doc.select(".s-input-box input);

```

<br />


jsoup 也可以 set httpHeader 等。{:&.fadeIn}

<br />

可以做比较轻量级的爬虫。{:&.fadeIn}


[slide]

[fastjson](https://github.com/alibaba/fastjson)

<br />

fastjson 是一个 Java 语言编写的高性能功能完善的 json 解析库，号称史上最快的 jackson，来自阿里巴巴。{:&.fadeIn}

<br />

除了 jdk 外不依赖任何 jar 包。 {:&.fadeIn}

[slide]

##用起来也非常简单，语法类似 Gson

<br />

```

User user = new User();
user.setId(1L);
user.setUserName("userName");

String jsonString = JSON.toJSONString(user); 

user = JSON.parseObject(jsonString, User.class);

```

[slide]

##[Mockito](http://mockito.org/)

<br />

Mockito 是一个流行的 Mocking 框架。 {:&.fadeIn}

<br />

它使用起来简单，学习成本很低，而且具有非常简洁的 API ，测试代码的可读性很高。 {:&.fadeIn}

<br />

因此它十分受欢迎，用户群越来越多，很多的开源的软件也选择了 Mockito。 {:&.fadeIn}
         
		 
[slide]

```		 
List<String> list = mock(ArrayList.class);  
	
when(list.get(0)).thenReturn("helloworld");  

String result = list.get(0);  
	
verify(list).get(0);  
	
Assert.assertEquals("helloworld", result);  

when(list.get(1)).thenThrow(new RuntimeException("test excpetion"));  

```

[slide]

##[Logback](http://logback.qos.ch/)

<br />

Logback 是由 log4j 创始人设计的又一个开源日志组件, 用来替换掉 log4j。  {:&.fadeIn}

<br />

据说有很多优点，我也不太清楚，我只知道用起来很优雅 ^_^ {:&.fadeIn}


[slide]

```
// log4j
if (logger.isDebugEnabled()) {
	logger.debug("There are now " + count + " user accounts: " + userAccountList);
}

// slf4j
logger.debug("There are now {} user accounts: {}", count, userAccountList);
	
```

[slide]

Logback 一般与日志门面框架 [SLF4J](http://www.slf4j.org/) 配合使用。


[slide]

[Joda](http://www.joda.org/joda-time/)

<br />

Java 自带的时间工具 java.util.Calendar、java.util.Date 非常别扭，一个很简单的功能都要写很多很行代码，还得异常处理。

[slide]

##比如给一个日期加90天并输出结果

<br />

```
Calendar calendar = Calendar.getInstance();
calendar.set(2000, Calendar.JANUARY, 1, 0, 0, 0);
SimpleDateFormat sdf = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss.SSS");
calendar.add(Calendar.DAY_OF_MONTH, 90);
System.out.println(sdf.format(calendar.getTime()));
	
```

[slide]

Joda 是 Java8 之前最优雅的 Java 时间库。

<br />

上面的功能使用 Joda 只需两行

<br />

```

DateTime dateTime = new DateTime(2000, 1, 1, 0, 0, 0, 0);
System.out.println(dateTime.plusDays(90).toString("MM/dd/yyyy HH:mm:ss.SSS");

``` 

[slide]

##Joda 还提供了

<br />

* LocalDate - 不包含具体时间的日期，年月日 {:&.fadeIn}
* LocalTime - 不含日期的时间，时分秒
* Instant - 时间戳
* DateTime - 带时区的时间
* DateTimeZone - a better time-zone
* Duration and Period - 时间区间
* Interval - 时间间隔
* 一个全面的和灵活的时间格式解析


[slide]

Java8 已经引进了 Joda 的思想增强了 Java 时间库


[slide]

##[Lombok](https://projectlombok.org/)

<br />

Java 程序员比较烦的一件事情之一就是要写大量的样板代码。 

<br />

所谓样板代码，是那些没有营养，却又不得不写的代码，写的时候觉得毫无技术含量，依样画葫芦，比如一个类的全参构造函数、无参构造函数、get/set方法、toString方法等等。 {:&.fadeIn}

<br />

虽然 IDE 可以自动生成，但每次更改字段又得重新生成，不够优雅！ {:&.fadeIn}

<br />


[slide]

Lombok 就能比较优雅的解决掉这个烦恼！

<br />

详情请参考 [Lombok 官网](http://projectlombok.org/)

[slide]

##[Druid](https://github.com/alibaba/druid)

<br />

>Druid 是Java语言中最好的数据库连接池。Druid 能够提供强大的监控和扩展功能。

<br />

Druid 来自阿里巴巴，在功能、性能、扩展性方面，都超过其他数据库连接池，包括 DBCP、C3P0 等。 {:&.fadeIn}

[slide]

Druid 不仅仅是一个数据库连接池，还提供了强大的监控功能，可以在 web 页面上看到连接池和 Sql 的工作情况。

<br />

其次，方便扩展。Druid 提供了 Filter-Chain 模式的扩展 API，可以自己编写 Filter 拦截 JDBC 中的任何方法，可以在上面做任何事情，比如说性能监控、SQL审计、用户名密码加密、日志等等。 {:&.fadeIn}

<br />

Druid 内置提供了用于监控的 StatFilter、日志输出的 Log 系列 Filter、防御 SQL 注入攻击的 WallFilter。 {:&.fadeIn}

<br />

在 Druid 的 GitHub 地址上有很详细的 Druid 介绍、使用  [Wiki](https://github.com/alibaba/druid/wiki/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98) {:&.fadeIn}


[slide]

##[Dubbo](http://dubbo.io/)

<br />

Dubbo 是一个阿里巴巴开源出来的一个分布式服务框架，致力于提供高性能和透明化的 RPC 远程服务调用方案，以及 SOA 服务治理方案。

[slide]

```
<bean id=“xxxService” class=“com.xxx.XxxServiceImpl” /> 

<dubbo:service interface=“com.xxx.XxxService” ref=“xxxService” /> 
	
```
<br />

服务端

[slide]

```
<dubbo:reference id=“xxxService” interface=“com.xxx.XxxService” /> 
	
```

<br />

客户端

[slide]

Dubbo 采用全 Spring 配置方式，透明化接入应用，对应用没有任何 API 侵入，只需用 Spring 加载 Dubbo 的配置即可。

<br />

Dubbo 支持各种常用的协议，如 Thrift、RMI、Hessian、WebService 等。 {:&.fadeIn}

<br />

同时也提供了注册中心、监控中心等。 {:&.fadeIn}


[slide]
##[Spring Boot](http://projects.spring.io/spring-boot/)

<br />

Spring Boot 是一个微框架，其设计目的是用来简化 Spring 应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。

[slide]

##约定大于配置！！！

<br />

Spring 平台饱受非议的一点就是大量的 XML 配置以及复杂的依赖管理，Spring Boot 可以做到 0 xml，同时 pom 文件也可以极大化的减小。


[slide]
##[JFinal](http://www.jfinal.com/)

JFinal 是基于 Java 语言的极速 WEB + ORM 框架，其核心设计目标是开发迅速、代码量少、学习简单、功能强大、轻量级、易扩展、Restful。 

<br />

>在拥有Java语言所有优势的同时再拥有 ruby、python、php 等动态语言的开发效率！为您节约更多时间，去陪恋人、家人和朋友 :)

<br />

[slide]

![](http://veryyoung.u.qiniudn.com/20151112212459.png)

快速出 demo 神器！

[slide]

类似这种的框架还有 [Play](https://www.playframework.com/)、[Grails](https://grails.org/)、[Ninja](http://www.ninjaframework.org/)、[Spark](http://sparkjava.com/) 等。



[slide]

## Others

<br/>

* Markdown {:&.fadeIn}
* Ngrok 
* Firebase 
* Bootstrap
* 热部署
* 探针监控

[slide]

##[Markdown](https://zh.wikipedia.org/zh-cn/Markdown)

<br />

Markdown 是一种轻量级标记语言，它允许人们“使用易读易写的纯文本格式编写文档，然后转换成有效的 HTML 文档”。

[slide]


##图片

<br />

```

![Foo](http://img0.bdstatic.com/img/image/4a75a05f8041bf84df4a4933667824811426747915.jpg)

```

<br />

![Foo](http://img0.bdstatic.com/img/image/4a75a05f8041bf84df4a4933667824811426747915.jpg) {:&.fadeIn}


[slide]

##强调

```
*强调* 或者 _强调_  (示例：斜体)


**加重强调** 或者 __加重强调__ (示例：粗体)


***特别强调*** 或者 ___特别强调___ (示例：粗斜体)
	
```

<br />

<br />




*强调* 或者 _强调_  (示例：斜体) {:&.fadeIn}

 
**加重强调** 或者 __加重强调__ (示例：粗体) {:&.fadeIn}

 
***特别强调*** 或者 ___特别强调___ (示例：粗斜体) {:&.fadeIn}


[slide]


##引用

<br />

```

> 这是一个引用。

```	

<br />

> 这是一个引用。 {:&.fadeIn}


[slide]


语法非常的简单，想做复杂的排版也只能依赖 HTML+CSS了， Markdown 不擅长也做不了那些事。

<br />

Markdown 比较适合那些需要经常码字或者进行文字排版的、对码字手速和排版顺畅度有要求的人群设计的，他们希望用键盘把文字内容啪啪啪地打出来后就已经排版好了，最好从头到尾都不要使用鼠标。这些人包括经常需要写文档的码农、博客写手、网站小编、出版业人士等等。  {:&.fadeIn}

[slide]

市面上也有很多可见即可得的 Markdown 编辑器，很多文本编辑器和 IDE 也在慢慢支持 Markdown。


![](http://veryyoung.u.qiniudn.com/markdow-editor-mou.png)	


很多网站都已支持 Markdown 来发文章或者评论，比如 GitHub、WordPress、 V2EX、锤子便签、简书......

[slide]

## Markdown 管理文档。

<br />

用 Markdown 可以像管理代码一样来管理文档，而且很多开源项目也都在这样干了。

<br />

MRD 放在 ChangeLog 里面，管理的是二进制的 word 文档，意味着版本控制工具的高级点的用法完全丢失了。  {:&.fadeIn}

<br />


用 Markdown + 版本控制工具来管理文档，意味着你可以使用 协作、分支、diff、history 甚至 merge 这些代码管理才有的功能。  {:&.fadeIn}


[slide]

##新花样

<br />

* [写简历](https://github.com/geekcompany/ResumeSample)  {:&.fadeIn}
* [PPT](https://github.com/ksky521/nodePPT)
* [写书](https://github.com/larrycai/kaiyuanbook/blob/master/zh/chapters/01-chapter3.markdown)
* [博客](https://jekyllrb.com/)
* [WIKI&文档](https://github.com/gollum/gollum)



[slide]
##[Ngrok](https://ngrok.com/)

<br />


>Secure tunnels to localhost


[slide]

##外网能访问需要的条件

<br />

1.	公网IP  {:&.fadeIn}
2.	路由映射
3.	80端口


[slide]

```

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


```

[slide]

##[Firebase](https://www.firebase.com/)

<br />

>Firebase can power your app's backend, including data storage, user authentication, static hosting, and more. Focus on creating extraordinary user experiences. We'll take care of the rest.

[slide]

```
<script>

var firebase = new Firebase('https://xop8xa2rcvk.firebaseio-demo.com/');

firebase.push(text);


firebase.on('child_added', function (snapshot) {
    var message = snapshot.val();
	console.log(message);
});


</script>

```
[slide]

##国内的替代品

<br />


* [野狗](https://www.wilddog.com/) {:&.fadeIn}
* [LeanCloud](https://leancloud.cn/) 
* [APICloud](http://www.apicloud.com/) 

[slide]
##[Bootstrap](http://getbootstrap.com/)

<br />

>Bootstrap is the most popular HTML, CSS, and JS framework for developing responsive, mobile first projects on the web.

<br />

简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。

[slide]

##Bootstap提供

<br />

* 简单快速的网格式布局 {:&.fadeIn}
* 优美的样式
* 兼容性良好
* 自适应
* 移动端友好
* 丰富的插件
* 主题

[slide]

##热部署

<br />

修改完代码(尤其是 Java 文件)利马生效！




[slide]

## 为什么需要热部署

<br />

Java 程序员最幸福的事情是可以在等程序编译的时候泡 Java！！ {:&.fadeIn}


[slide]

##热部署的方案

<br />

1.	Tomcat Reload {:&.fadeIn}
2.	Eclipse Debug 模式
3.	IDEA Reload
4.	Jetty
5.	Jrebel

[slide]
##Tomcat Reload

<br />

修改 server.xml 的 Host 配置，加上 reloadable="true" {:&.fadeIn}

<br />

只能热部署静态文件，修改 Java 或配置会自动重启 server，效率低下，还容易造成内存溢出、 class 找不到等 bug。 {:&.fadeIn}
 
[slide]
##Eclipse Debug 模式

<br />

Eclipse debug 模式修改完 Java 代码会自动重启 server。 {:&.fadeIn}

<br />

缺点同上~ {:&.fadeIn}

[slide]

##IDEA Reload

<br />

IDEA 在 debug 模式下设置失去焦点更新资源和 classes 

<br />

![](http://veryyoung.u.qiniudn.com/20151211144609.png)

[slide]
##缺点

<br />

只支持静态文件、Java 现有方法的更改，新增 Java 方法、类，或者改变 SpringMVC 的 RequestMapping、Spring 配置等都不会生效。 {:&.fadeIn}


[slide]

##Jetty

<br />

Jetty 会监听生成的 build 目录，遇到文件更新会自动替换掉。 {:&.fadeIn}

<br />

并不能监听源码的变更。 {:&.fadeIn}

[slide]

##Gradle 的解决方案

<br />

1.	Gradle Watch {:&.zoomIn}
2.	Gretty
3.	Continuous Build

[slide]

##[Gradle Watch](https://github.com/bluepapa32/gradle-watch-plugin)

<br />

gradle watch 的作用是监听某种类型的文件的变化，包括添加，删除和修改，然后执行预定义的任务。

<br />

```
apply plugin: 'watch'

watch {
    java {
        files files('src/main/java')
        tasks 'compileJava'
    }
}

```


[slide]

##缺点

<br />

只支持低版本 Gradle，并且已不再维护！


[slide]

##[Gretty](https://github.com/akhikhl/gretty)

<br />

>Gretty is a feature-rich gradle plugin for running web-apps on embedded servlet containers. 

[slide]

<br />

Gretty 覆盖了 jettyRun 和 tomcatRun 等 task，使用起来和普通的 jettyRun 之类的一样，但是提供了热部署的功能。

[slide]
##缺点

<br />

热部署效率差！感觉是半重启！

[slide]

##[Continuous Build](http://gradle.org/feature-spotlight-continuous-build/)

<br />

```
gradle -t

```

<br />

Gradle 2.5 的 feature，持续构建。


[slide]

##缺点

<br />

1.	需要的 Gradle 版本太高  {:&.zoomIn}
2.	实验性特性
3.	不支持 Jetty

[slide]

##[Jrebel](http://zeroturnaround.com/software/jrebel/)

<br />

>Reload Code Changes Instantly

[slide]

##瑕疵

<br />

1.	修改文件过多偶尔会异常  {:&.zoomIn}
2.	偶尔会失效
3.	昂贵



[slide]

#探针监控

<br />

安装探针，实现自动化检测

<br />

1.	[听云](http://demo.tingyun.com/overview/application)  {:&.zoomIn}
2.	[OneRASP](https://rasp.oneasp.com/demo.html)