---
layout: post
title: 利用Jrebel热部署提升工作效率
date: 2015-02-05 23:01
author: VERYYOUNG
comments: true
categories: [Java]
---
<h3>利用Jrebel提升工作效率</h3>

<p>老早就听说有Jrebel这款神器了，热部署，去官网看了看，license贵的离谱啊，300RMB per licence</p>

<p>只有用盗版咯。</p>

<p><em>阿弥陀佛</em></p>

<p>记录下流程。</p>

<h3>1.安装插件</h3>

<p>本人习惯用IDEA做开发（<em>依然是盗版，罪过</em>），找Jrebel的插件咯。 <strong>鄙视IDE的童鞋可以直接配置JVM，下面会提到的</strong></p>

<p>在IDEA Setting里的plugins可以在线安装，鄙人所处网络环境堪忧，选择离线安装，这也是本人比较推荐的一种方式。</p>

<p>移步<a href="https://plugins.jetbrains.com/plugin/4441?pr=idea">https://plugins.jetbrains.com/plugin/4441?pr=idea</a>  下载适合IDEA版本的ZIP包</p>

<p>还是在IDEA Setting里的plugins里，选择install from disk，安装成功。</p>

<h3>2.破解 （<em>罪过罪过</em>）</h3>

<p>下载最新版的国人HACK版插件，（关注“最佳人生”微信，每次有新版作者会推送的）。</p>

<p>下载完毕后，找出lib下的jrebel.jar和jrebel.lic，复制到IDEA Jrebel Plugins的lib目录下，替换，ok</p>

<h3>3.RUN RUN RUN</h3>

<p>IDEA下粗线了Run With Jrebel的选项</p>

<p>点击吧。</p>

<p>哈哈哈，是不是没跑起来，OutOfMemoryError了吧？</p>

<p><strong>配置下JVM呗。</strong></p>

<p>我在IDEA的tomcat VM OPTION下 加入了</p>

<pre><code>-Xms1024m -Xmx1024m -XX:PermSize=128M -XX:PermSize=256M
</code></pre>

<p>再启动</p>

<p>如果粗线如下log</p>

<pre><code>2015-02-05 22:42:16 JRebel:  
2015-02-05 22:42:16 JRebel:  #############################################################
2015-02-05 22:42:16 JRebel:  
2015-02-05 22:42:16 JRebel:  JRebel Agent 6.0.3 (201501261446)
2015-02-05 22:42:16 JRebel:  (c) Copyright ZeroTurnaround AS, Estonia, Tartu.
2015-02-05 22:42:16 JRebel:  
2015-02-05 22:42:16 JRebel:  Over the last 1 days JRebel prevented
2015-02-05 22:42:16 JRebel:  at least 4 redeploys/restarts saving you about 0.2 hours.
2015-02-05 22:42:16 JRebel:  
2015-02-05 22:42:16 JRebel:  Licensed to anonymous-user
2015-02-05 22:42:16 JRebel:   with the following restrictions: 
2015-02-05 22:42:16 JRebel:   ####### Cracked by anonymous-user, For FUN! Unlimited! Enjoy! ######
2015-02-05 22:42:16 JRebel:  
2015-02-05 22:42:16 JRebel:  License type: perpetual
2015-02-05 22:42:16 JRebel:  
2015-02-05 22:42:16 JRebel:  
2015-02-05 22:42:16 JRebel:  #############################################################
2015-02-05 22:42:16 JRebel:  
Connected to the target VM, address: '127.0.0.1:64146', transport: 'socket'
</code></pre>

<p>恭喜你，再也不用每次修改完一行代码，重新RUN，然后思考人生了！！</p>

<p>试了下，改完代码鼠标移出IDEA，哗啦啦编译起来了，然后告诉我替换掉了的class的个数。</p>

<p>然后就起效啦！！</p>

<hr />

<h4>现在再来说不用IDE怎么办。</h4>

<p>在Java的VM arguments 输入如下参数：</p>

<pre><code>-noverify
-agentpath:JREBEL_HOME/lib/jrebel64.dll
#Linux用这个：-agentpath:JREBEL_HOME/jrebel_running/lib/libjrebel64.so
#Mac OS用这个：-agentpath:JREBEL_HOME/jrebel_running/lib/libjrebel64.dylib
-Drebel.dirs=WORKSPACE/webapp/WEB-INF/classes
-Drebel.disable_update=true
-DJAVA_OPTS=-Xms256m -Xmx256m -XX:MaxNewSize=512m
</code></pre>

<p>上述参数的相关说明：
-agentpath: 这个是你使用的JRebel Agent版本的lib包的路径(路径后缀不要写成jrebel.jar)，注意其中的斜线方向。
-Drebel.dirs ：这个是你要监控的项目的 class 文件路径
-Drebel.disable_update: 设为true,就不会联网检查更新
-DJAVA_OPTS: 这个选项不是必须，当内存溢出的时候或其它特殊情况下才需要设置它的参数大小。</p>

<p>JREBEL_HOME代表Jerbel的放置目录，WORKSPACE代表工作目录</p>

<h1>完事！尽情提高工作效率吧！</h1>

