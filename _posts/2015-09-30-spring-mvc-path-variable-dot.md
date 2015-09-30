---
layout: post
title: SpringMVC PathVariable 丢失小数点后面的数据
date: 2015-9-30 11:17:10
author: VERYYOUNG
comments: true
categories: [Java]
---
SpringMVC 默认情况下会丢失小数点后面的数据，比如传入22.5只能得到22，传入邮箱如 user@gmail.com 只能得到 user@gmail

<!-- more -->

----------

SpringMVC 默认情况下会把小数点后面的东西当做文件后缀去处理，过滤掉。

解决方案有如下两种。

1.  使用正则表达式。

    假如原来是
    
        @RequestMapping("{email}")
        
    改为
    
        @RequestMapping("{email}:.+")
        
        
2.  修改 Spring 配置
    
    如果你不太在意文件的后缀名，可以修改 Spring 的配置。
    
    在
    
        <mvc:annotation-driven>
        
    中加入
    
        <mvc:path-matching registered-suffixes-only="true"/>
    
    




<br>
参考：[https://stackoverflow.com/questions/16332092/spring-mvc-pathvariable-with-dot-is-getting-truncated](https://stackoverflow.com/questions/16332092/spring-mvc-pathvariable-with-dot-is-getting-truncated)


