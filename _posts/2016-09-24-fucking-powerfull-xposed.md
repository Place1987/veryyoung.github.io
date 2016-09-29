---
layout: post
title: 屌炸天的 Xposed 框架
category: [Android]
date: 2016-09-24
author: VERYYOUNG
comments: true
---

感觉国内的应用市场都很流氓，在 V 友的推荐下，知道了 [酷市场](http://www.coolapk.com/)， 上面的应用质量比较高，有很多始发应用。
而在这些始发应用中，最多的就是顶着绿色 Android 机器人头像的 Xposed 框架啦！

<!-- more -->

然后开始了解了一下，并尝试着去编写 Xposed 插件，感觉真特么强大！！

### 首先解释下什么是 Xposed 框架。

来看看官方的解释

>Xposed is a framework for modules that can change the behavior of the system and apps without touching any APKs. That's great because it means that modules can work for different versions and even ROMs without any changes (as long as the original code was not changed too much). 

简单说起来，就是在不改变 App 代码、不改变 Rom 的情况下，去影响 App 的行为。

我擦，这不是 AOP 吗？哈哈~

Xposed 可以拦截 method，然后在方法执行前或方法执行后做一些事情，甚至去阻止 method 的执行，基于这个原理甚至可以修改手机的串号、定位，等等各种信息。


### 说说 Xposed 插件开发流程

#### 1. AndroidManifest.xml 配置

这个和普通的 Android 应用开发截然不同了，但需要配置的东西非常少，给个例子，copy 之后修改吧

```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="me.veryyoung.dingding.unrecallled">

    <application android:label="防止钉钉撤回">
        <meta-data
            android:name="xposedmodule"
            android:value="true" />
        <meta-data
            android:name="xposeddescription"
            android:value="在本机上保留对方要撤回的钉钉消息。" />
        <meta-data
            android:name="xposedminversion"
            android:value="30" />
    </application>
</manifest>

```
反正都是些文本信息。

#### 2.  导入 XposedBridgeApi.jar 包

可以直接复制到 libs 里面去，也可以通过 gradle 去添加，没什么好说的

#### 3.  代码编写

需要通过 Xposed 提供的方法，去 hook 一个 method，然后 method 执行前、后 等去完成你需要做的事情。

直接给段代码例子吧


```java

public class Main implements IXposedHookLoadPackage {

    private static final String DINGDING_PACKAGE_NAME = "com.alibaba.android.rimet";

    private static final String MAP_CLASS_NAME = "com.alibaba.wukong.im.message.MessageImpl";
    private static final String MAP_FUNCTION_NAME = "recallStatus";

    @Override
    public void handleLoadPackage(final LoadPackageParam lpparam) throws Throwable {


        if (lpparam.packageName.equals(DINGDING_PACKAGE_NAME)) {

            //map
            findAndHookMethod(MAP_CLASS_NAME, lpparam.classLoader, MAP_FUNCTION_NAME, new XC_MethodHook() {
                @Override
                protected void afterHookedMethod(MethodHookParam param) throws Throwable {
                    param.setResult(0);
                }
            });
        }
    }
}

```

这个意思是，拦截钉钉的 ```com.alibaba.wukong.im.message.MessageImpl``` 类下的 ```recallStatus``` 方法，然后把返回结果设置为 0。

而这个的功能是，在本地保留对方撤回的消息。

哈哈，是不是很邪恶？~~

#### 4.  配置插件入口

在 assets 目录下，新建一个叫 xposed_init 的文件，里面配置下项目的入口类

在我的例子中，这个类是 ```me.veryyoung.dingding.unrecallled.Main```


### 需要补充的地方

1.  hook 到 method 之后，你可以利用 LoadPackageParam 的 classLoader 去加载 app 里面的各种类，通过反射去取各种值，调用各种方法，太厉害了有米有？！！！
2.  代码每次改完必须重启Android 手机
3.  找到切人点，得依靠 Android 反编译的技术，这个说来可话长了。。
4.  必须 Root，且安装 Xposed 框架，有变砖风险哦。


### Some Examples

下面贴几个比较牛逼的 Xposed 插件的酷市场地址

- [运动修改器](http://www.coolapk.com/apk/name.caiyao.sporteditor): 修改QQ健康和微信运动里的步数。
- [阻止运行](http://www.coolapk.com/apk/me.piebridge.forcestopgb): “阻止运行”通过劫持几个系统API，阻止程序在你不使用时运行。
- [绿色守护](http://www.coolapk.com/apk/com.oasisfeng.greenify): 『绿色守护』帮助你甄别那些对系统全局性能和耗电量有不良影响的应用程序，并通过独特的『绿色化』技术，阻止它们消耗您的电池电量，占用您的宝贵内存。经过『绿色化』工艺处理的应用，在您没有主动启动它们的时候，无法『偷偷』运行，而在您正常启动它们时仍然拥有完整的功能和体验，正如iPhone应用那样！
- [WechatUnrecalled](http://www.coolapk.com/apk/com.fkzhang.wechatunrecalled): 防止微信撤回聊天消息和朋友圈回复。
- [微信红包插件](http://www.coolapk.com/apk/me.veryyoung.wechat.luckymoney): 自动抢微信红包，我自己写的哈哈。
- [QQ红包插件](http://www.coolapk.com/apk/me.veryyoung.qq.luckymoney): 自动抢QQ红包，也是我写的
- [钉钉红包插件](http://www.coolapk.com/apk/me.veryyoung.dingding.luckymoney): 自动抢钉钉红包，同上
- [随机游戏插件](http://www.coolapk.com/apk/me.veryyoung.wechat.randomgame): 随机游戏插件是一款可以在微信随机游戏——猜拳和骰子中按照设定得出结果的 xposed 模块， 也是我写的！



-----

我的 [Github](https://github.com/veryyoung) 上有各种 Xposed 框架的源码，希望有兴趣的同学能一起学习，顺手点个 star，哈哈。