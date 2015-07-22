---
layout: post
title: Mybatis学习笔记
date: 2014-12-10 21:19
author: VERYYOUNG
comments: true
categories: [Java]
---
最近一个项目用Mybatis在做Dao层。

感受了一下，没Hibernate用起来方便，比如insert、update这些都得自己手写sql...

但是可控性确实强了不少，而且入手也极快。

下面记录一些使用过程中需要注意的地方，以后Mybatis遇到的问题都往这贴。

1.简化配置 ：
  （1）、 每次加一个Entity写typeAliases神马的神烦，换成
  [java]&lt;package name=&quot;com.package.entity&quot;/&gt;[/java]啥的就ok咯
  顺带在xml配置上mapper的basePackage
  （2）、每次加完mapper.xml还要注册，又是神烦啊。如下配置就好了。
[java]
    &lt;bean id=&quot;infoSessionFactory&quot; class=&quot;org.mybatis.spring.SqlSessionFactoryBean&quot;&gt;
		&lt;property name=&quot;dataSource&quot; ref=&quot;infoDataSource&quot; /&gt;
        &lt;property name=&quot;configLocation&quot; value=&quot;classpath:mybatis/mybatis-info-config.xml&quot;/&gt;
        &lt;property name=&quot;mapperLocations&quot; value=&quot;classpath:mybatis/mapper/info/*.xml&quot;/&gt;
    &lt;/bean&gt;
[/java]

2.多参数查询。
（1）、传Map或者对象。
能传对象当然好咯，不能传对象用map貌似有点不直观，在sercve里面调用的时候还得把mapper的key写对，不太爽。
（2）、用占位符，类似#{0}、#{1}....  使用方便，但是在in查询，用传入一个枚举的list的时候貌似不work，不知道是不是mybatis的bug，有时间读读源码。

3.神烦的in查询。
还好mybatis支持类似jstl 的foreach语句。可以类似如下写
[java]

    &lt;select id=&quot;listByStatus&quot; resultType=&quot;User&quot; parameterType=&quot;map&quot;&gt;
        SELECT * FROM table where status in
        &lt;foreach collection=&quot;statusList&quot; open=&quot;(&quot; close=&quot;)&quot; index=&quot;&quot; item=&quot;status&quot; separator=&quot;,&quot;&gt;
            #{status}
        &lt;/foreach&gt;
        order by timeCreated limit #{start},#{end}
    &lt;/select&gt;

[/java]

我觉得这里应该可以简化下，读取sql的时候遇到in，看看后面的是否为list 或者array，如果是，动态拼接字符比较好，省得用foreach这种东东。
嘿嘿！有机会改了发个pr！

4.动态sql。
 mybatis 提供了if else foreach when 这些类似jstl的语法，
see <a href="http://mybatis.github.io/mybatis-3/zh/dynamic-sql.html" title="http://mybatis.github.io/mybatis-3/zh/dynamic-sql.html" target="_blank">http://mybatis.github.io/mybatis-3/zh/dynamic-sql.html</a>

5.对象嵌套。
加入user entity里含有userInfo
insert的时候用 #{userInfo.place}这样的，可多重嵌套。
select的时候用as，如 select id as "userId" 这样的，as后面的字符要于user 属性存在对应关系。



 
