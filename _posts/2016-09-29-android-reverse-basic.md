---
layout: post
title: Android 逆向基础
category: [Android]
date: 2016-09-29
author: VERYYOUNG
comments: true
---

Android 的防护做的不太好，很容易被逆向。
如果不采取保护措施，很有可能会被人利用，造成非常严重的后果。

下面讲讲 Android 逆向的一些基础。

<!-- more -->

## APK 的组成

首先说下 apk 包的组成。

apk == Android Package， 其实是压缩包的一种，解压之后就能看到类似开发阶段的结构了。

| 文件或目录        | 解释           |
| ------------- |:-------------:|
| AndroidManifest.xml      | Android清单文件，用于描述该应用程序的名字、版本号、所需权限、注册的服务、链接的其他应用程序。 |
| META-INF/      | 文件清单、签名信息      | 
| res/ | 资源文件夹      |   
| libs/ | 依赖包，一般是 .so 文件      |   
| res/ | 资源文件，比如布局 xml、图片      |    
| assets/ | 一些原始的文件，比如配置文件等，原封打进 apk      |    
| resources.ars | 存放静态值，如 string.xml、array.xml文件中定义的值；资源文件映射。  | 
| classes.dex/ | Dalvik dex 文件包（类似于 Java class jar 包），可能会有多个。      |   



## Android 逆向工具

### [AXMLPrinter](https://github.com/rednaga/axmlprinter)

Android apk 直接 解压后得到的 xml 文件都是加密过的二进制文件，人类不可读。

这款工具可以很轻松的完成。

 ```java -jar axmlprinter.jar AndroidManifest.xml```

### [dex2jar](https://github.com/pxb1988/dex2jar)

这款工具可以把 Dalvik 虚拟机的 dex 文件转为 Java 平台的 class 文件包，也就是传统的 Java Jar 包。

```sh dex2jar.sh classes.dex ```

### [JD-GUI](http://jd.benow.ca/)

由 dex2jar 得到普通的 Jar 包之后，就有很多方法 decode 了。

JD-GUI 是一个主流的 Jar decode 工具。

使用它能直接打开 Jar 包，查看源码。

当然，也有很多其他工具，比如 [IntelliJ IDEA](https://www.jetbrains.com/idea/) 对 Jar 包反编译有着默认的支持。


### [apktool](https://ibotpeaches.github.io/Apktool/)

>apktool is a tool for reverse engineering Android apk files.

apktool 能对 Android apk 进行反编译，得到逆向过后的资源文件和 Java 代码（以 smali 的形式）。

使用起来很简单：

```apktool d test.apk```

就能把 test.apk 反编译，然后进行阅读和修改。

apktool 也可以用来把之前反编译过后的文件进行再打包。

``` apktool b test  ```

使用 apktool 可以用来修改 Android apk，如果仅仅需要修改静态文件，只需要在 strings.xml 中找到对应的字符串进行替换就行，
修改静态文件（如音乐、图片）同理。

但修改 Java 代码可能就比较困难了。要有一定的 smali 代码阅读能力，并且需要在一堆混淆过的 smali 代码中找到突破口更加困难。



### [sign](https://github.com/appium/sign)

前一步修改过的 apk 文件需要重新签名才能安装。

使用 sign 可以很方便的完成这件事情。

``` java -jar sign.jar test.apk ```

需要注意的是，签名后的 apk 和之前的 apk 签名肯定不同，有些 apk 会对签名做校验，同时，应用市场也会各种报签名不匹配的警告。



### [jad-x](https://github.com/skylot/jadx)

使用 dex2jar、jd-gui 还是非常麻烦的， jadx 可以一键帮我们做成这套流程，并且提供了 GUI。

强烈推荐。


jad-x 有个 bug，就是不能识别多 dex，用 jad-x 直接反编译只能得到默认 dex 的结果。而一个 Android apk 可能由多个 dex 组成，
比如微信就有三个。

本人的做法是解压 apk，分别用 jad-x 逆向各个 dex，用 jd-gui 打开之后，左上角的 save，保存代码到多个文件夹，然后 merge 在一起。

Mac 的 finder 自带 merge 文件夹功能。在拖拽文件夹到目标时按住 option 键，然后选择合并就行了。

也可以在命令行下执行：

```op -R /folder1 /folder2```


## Xposed

Xposed 可以让 Android 平台发挥出最强性能，能在不改变 apk 本身的情况下，改变 apk 的行为。 

关于 Xposed 的详细介绍可以参考 [屌炸天的 Xposed 框架](/blog/2016/09/24/fucking-powerfull-xposed.html)。


-------

很多人发邮件咨询我 Android 逆向的诀窍，其实并没有什么诀窍或者秘诀可言。

关于 Android 逆向，耐心非常重要，在一堆混淆过后的代码中挣扎是一件很痛苦的事情，很容易有挫折感，但找到入口的感觉还是非常爽歪歪的哈哈😝。

诀窍没有，技巧可能有几条吧~

1.  从人类能感知到的地方开始入手。比如通过界面上的字，或者 Toast 开始入手，慢慢往后找。
2.  抓包。抓包之后，搜索对应包的字段，肯定有对应模型和返回结果对应的！~
3.  通过 Log 或者 Toast，可以修改 apk 植入，也可以用 xposed 挂钩子。


--- 

## 如何保护 apk？

1. 代码混淆 (所谓的代码混淆就是把变量变成 abc 等乱七八糟的，降低可读性)
2. 检查签名 (在代码里面检查 apk 的 checksum，不过这段代码也可能被干掉哈哈)
3. 使用 ndk（用 ndk 编写的代码逆向难度会高很多）
4. 网络请求加密传输，防止被抓包
5. 服务端一定要做 check，因为客户端是很不可靠的！
6. 使用热发布（微信就用 tinker 对抗 xposed） 



## 推荐书籍

- [Android软件安全与逆向分析](https://book.douban.com/subject/20556210/)
- [Android安全攻防权威指南](https://book.douban.com/subject/26348151/)