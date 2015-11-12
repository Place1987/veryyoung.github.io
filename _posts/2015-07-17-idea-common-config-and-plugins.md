---
layout: post
title: IDEA 常用配制和插件
date: 2015-07-17 15:28
author: VERYYOUNG
comments: true
categories: [Java]
---

正如IDEA官方说的，


>IntelliJ IDEA IS The Most Intelligent Java IDE



习惯 Eclipse、NetBeans 和其他 IDE 或者文本编辑器的童鞋可能比较难适应 IDEA，但付出一点时间好好学学这个 IDE 是很有必要的，熟悉之后用这工具简直是一种享受。



下面提几点常用的设置和插件。

###设置

####1.安装主题。

[http://www.ideacolorthemes.org/](http://www.ideacolorthemes.org/) 上很有多很好看的 IDEA 主题，可以选择自己喜欢的下载下来，然后 File -> Import Settings ，马上大变样，好看极了，保证你再也不想看 Eclipse 那种上个世纪的丑样了！！

####2.显示行号.

Settings->Editor->Appearance 标签项，勾选Show line numbers

####3.快捷键设置

Settings->KeyMap ，可以随意自定义各种快捷键

墙裂推荐一个快捷键“Double shift”，可以搜索任何你想要的东西!

####4.插件

Settings->Plugins ，搜索你想安装的插件就能在线安装了，比 Eclipse 安装插件要方便许多！
下面是一些常见的插件。

##### [Lombok](http://plugins.jetbrains.com/plugin/631)
如果你在用 Lombok，就得装个这个插件啦，省掉一堆 getter、setter，有关 Lombok 的详细介绍参考 [使用 Lombok 来缩减 Java 代码](../blog/2015/10/08/use-lombok-to-reduce-your-java-code.html)

##### [CheckStyle](http://plugins.jetbrains.com/plugin/1065)
通过检查对代码编码格式，命名约定，Javadoc，类设计等方面进行代码规范和风格的检查，从而有效约束开发人员更好地遵循代码编写规范。

##### [FindBugs](https://plugins.jetbrains.com/plugin/3847) 
FindBugs 通过检查类文件或 JAR 文件，将字节码与一组缺陷模式进行对比从而发现代码缺陷，完成静态代码分析，可以找出常见的 bug 或者可能潜在 bug 的地方。

##### [Jrebel](https://plugins.jetbrains.com/plugin/4441)
热部署神器，改完代码直接生效，不用重启啦！

具体参考 [利用Jrebel热部署提升工作效率](/blog/2015/02/05/using-jrebel-hot-deployment-making-work-efficiency.html)

##### [CamelCase](https://plugins.jetbrains.com/plugin/7160)
可以切换变量命名风格，如 SogouInc、sogouInc、sogou—inc、SOGOU_INC

##### [RestClient](https://plugins.jetbrains.com/plugin/5951)
可用来调试 HTTP 接口，相当于 IDE 版的 POSTMAN

##### [CodeGlance](https://plugins.jetbrains.com/plugin/7275)
生成右侧代码缩略图，用过 Sublime 的肯定知道 ^_^

##### [GsonFormat](https://plugins.jetbrains.com/plugin/7654)
把 Json 数据转为 Java 对象，很实用的！！！

##### [AceJump](https://plugins.jetbrains.com/plugin/7086)
Emacs 用户肯定知道是干嘛的！！

所谓 AceJump，就是你按快捷键进入 AceJump 模式后（默认是 Ctrl+J），再按任一个字符，插件就会在屏幕中这个字符的所有出现位置都打上标签，你只要再按一下标签的字符，就能把光标移到该位置上。换言之，你要移动光标时，眼睛一直看着目标位置就行了，根本不用管光标的当前位置，非常舒服。

##### [LiveEdit](https://plugins.jetbrains.com/plugin/7007)
Intellij IDEA 默认自动保存的，根本不用 Ctrl+S，LiveEdit 能自动更新浏览器里的网页，所以F5也省了

如果是是双屏的话，基本上所敲即所得了。

##### [Key Promoter](https://plugins.jetbrains.com/plugin/4455)
Key Promoter 会统计你用键盘或鼠标操作了某功能几次，对应的快捷键是啥，或者建议你给常用的功能绑定快捷键。

---


还有一些用法和插件可以参考 [http://www.zhihu.com/question/20783392](http://www.zhihu.com/question/20783392)
