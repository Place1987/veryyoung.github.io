---
layout: post
title: Tomcat分布式Session共享
date: 2015-07-20 13:43
author: VERYYOUNG
comments: true
categories: [Web Server]
---
<h1>tomcat-redis-session-manager</h1>

<p>用tomcat默认的方式来管理session是很有问题的，比如项目重启tomcat，用户会话就会丢失，这样用户体验非常糟糕。应用只要稍微上点规模或者需要多机负载，这是必须做的工作了。</p>

<hr />

<p>web server自带解决方案有2：</p>

<ol>
<li><p>tomcat有自带的session共享方式cluster，多个tomcat实时复制session。缺点是服务器之间会频繁的进行数据同步，如果在不同机器上网络开销会非常大，而且数据同步会有延迟的，这可能导致数据不一致，还有缺点就是session在每台机器都保有一份，太浪费资源了！</p></li>
<li><p>ngnix有基于ip hash转发的策略，用这个来保证每个IP每次访问到的都是同一个tomcat实例。缺点很明显，在多用共享同一IP的情况下一点负载均衡的作用都木有了。</p></li>
</ol>

<hr />

<p>很自然能想到的方法就是把tomcat的session交给memcached或者redis去集中管理。这样不管tomcat如何增加减少或者重启，和session都没关系。</p>

<p>本来打算自己实现一套，上git随便搜了下，发现早就有现成的解决方案了。
<a href="https://github.com/jcoleman/tomcat-redis-session-manager" title="https://github.com/jcoleman/tomcat-redis-session-manager">https://github.com/jcoleman/tomcat-redis-session-manager</a></p>

<h3>使用方法很简单:</h3>

<ol>
<li><code>git clone git@github.com:jcoleman/tomcat-redis-session-manager.git</code></li>
<li><code>gradle build -x test  copyJars</code> 最好build之前注释掉build.gradle里面的maven私仓</li>
<li>复制   tomcat-redis-session-manager-{version}.jar commons-pool2-2.2.jar jedis-2.5.2.jar 到每个tomcat的lib目录下</li>
<li><p>修改tomcat/conf/context.xml 
加入<code>&lt;Valve className="com.orangefunction.tomcat.redissessions.RedisSessionHandlerValve" /&gt;
&lt;Manager className="com.orangefunction.tomcat.redissessions.RedisSessionManager" host="localhost" port="6379" database="0" maxInactiveInterval="60" /&gt;</code></p></li>
<li><p>启动两个tomcat（如果是同一台机器需要指定不同的端口）</p></li>
<li>在nginx conf增加upstream，指定这两天tomcat的访问url</li>
<li><code>nginx -s reload</code>   </li>
<li>测试。访问任意一台tomcat，然后<code>redis-cli</code>
可以看到session已写入redis，再访问另外一台，session不变</li>
</ol>

<hr>
<h3>原理</h3>
tomcat提供了`org.apache.catalina.session.ManagerBase`基类来扩展session管理。
在对应生成session之后管理session的地方存储到jedis，然后getSession也从jedis取。
