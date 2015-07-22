---
layout: post
title: Splunk的安装及配置
date: 2015-02-07 22:52
author: VERYYOUNG
comments: true
categories: [Linux]
---
<h2>Splunk的安装及配置</h2>

<p>Splunk 是一个运行于多平台环境下的日志分析软件和系统故障诊断工具。
Splunk 可以支持任何服务器产生的日志，其对日志进行处理的方式是进行高效索引之后让管理员可以对日志中出现的各种情况进行搜索，并且通过非常好的图形化的方式展现出来。</p>

<p>简单介绍下安装及配置流程</p>

<h3>1.下载</h3>

<p>上<a href="http://splunk.com/">splunk官网</a>,选择Free Download，选择对应的操作系统版本，点击开始下载。 其实不能直接下啊，得先注册账户啊，和Jdk下载一样。
老老实实注册吧。注册完毕，登陆，继续Free Download，终于可以了。
发现其实不用注册都行，前提是你知道下载地址。这里给个splunk-6.2.1-245427-Linux-x86_64.tgz的下载地址 <a href="http://download.splunk.com/products/splunk/releases/6.2.1/splunk/linux/splunk-6.2.1-245427-Linux-x86_64.tgz">http://download.splunk.com/products/splunk/releases/6.2.1/splunk/linux/splunk-6.2.1-245427-Linux-x86_64.tgz</a></p>

<h4>再教下怎么找下载链接。</h4>

<p>找下载链接，当看到如下界面时
<img src="http://veryyoung.u.qiniudn.com/splunk-01.png" alt="splunk-01" />
F12，或者右键核审元素，查看源代码，找到该dom，地址找到咯！！</p>

<p><img src="http://veryyoung.u.qiniudn.com/splunk-02.png" alt="splunk-02" />
<em>我居然还去注册了账户，妈蛋。</em></p>

<h3>2.安装</h3>

<p><a href="splunk.com">splunk.com</a>有个<a href="http://docs.splunk.com/Documentation/Splunk/latest/Installation/InstallonLinux">官网指导文档</a>，对着跑吧。</p>

<pre><code>cd /opt
wget http://download.splunk.com/products/splunk/releases/6.2.1/splunk/linux/splunk-6.2.1-245427-Linux-x86_64.tgz
tar zxvf splunk-6.2.1-245427-Linux-x86_64.tgz
</code></pre>

<p>解压完毕，splunk已经算安装好了。</p>

<p>先别启动，splunk默认端口是8080，我的机器8080端口已经被tomcat
占用了。
得换端口咯。</p>

<pre><code>cd splunk/bin/

./splunk set  web-port 9000
</code></pre>

<p>默认端口被设置为9000啦</p>

<h3>3.配置</h3>

<p>开始启动吧</p>

<pre><code>./splunk start
</code></pre>

<p>然后打开浏览器 访问 host:port吧。
打开之后，需要登录，登录框上面写着默认账号为 admin，密码为changeme
好的，change you
把密码改为你想改的密码，登录进去吧。</p>

<p>进去之后的界面大概是这样的
<img src="http://veryyoung.u.qiniudn.com/splunk-03.png" alt="splunk-03" /></p>

<p>这时候splunk是没有任何数据的。
点击添加数据咯。
有如下几种类别可以添加
<img src="http://veryyoung.u.qiniudn.com/splunk-04.png" alt="splunk-04" /></p>

<p>我选择的是文件目录，指定到对应的tomcat，next ，next，搞定。</p>

<p>顺便说一下，选择目录的时候吓死我了，机器的目录全被列举出来了。
<img src="http://veryyoung.u.qiniudn.com/splunk-05.png" alt="splunk-05" />
有点小不安全，所以一定要保护好splunk密码啊.</p>

<hr />

<p>好了，以后再也不用进服务器找日志了，图形化界面，强大的搜索语句和分析监控和报告，再好不过了。</p>

<hr />

<p>免费版只有每日500M的份额，需求量大于这个的得买licence哦！</p>

