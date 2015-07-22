---
layout: post
title: 解决SpringMVC返回Json乱码
date: 2014-12-10 21:34
author: VERYYOUNG
comments: true
categories: [Java]
---
使用@responseBody注解返回json乱码了

Google了一下，找出了以下代码。
[java]
public class StringHttpMessageConverter extends AbstractHttpMessageConverter&lt;String&gt; {    
    
    public static final Charset DEFAULT_CHARSET = Charset.forName(&quot;ISO-8859-1&quot;);    
.....
[/java]

What's the fuck!
SpringMVC默认编码模式是ISO-8859-1

这里不得不提的是与StringHttpMessageConverter 同级的类MappingJacksonHttpMessageConverter，天知道是什么原因：同一个作者，对于这两个类，默认字符集一个是ISO-8859-1，一个是UTF-8。 

既然事已如此，那就想办法把这个地方用到的ISO-8859-1也改成UTF-8了。有两个思路： 
1. 重新实现StringHttpMessageConverter 的 getDefaultContentType

实现之后，配置org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter为自己实现的StringHttpMessageConverter 

2.反射！
还记得<a href="http://www.veryyoung.me/?p=147" title="http://www.veryyoung.me/?p=147" target="_blank">http://www.veryyoung.me/?p=147</a>
这篇文章简单粗暴的做法吗？直接通过反射修改代码，肯定行得通。

3、网上有人建议在每个controller的方法RequestMapping上加上 produces = "text/html;charset=UTF-8"
比较简洁，但重复工作太多。

4.Google出来的方法，最优方案。
在web.xml里加入如下filter
[java]
    &lt;filter&gt;
        &lt;filter-name&gt;CharacterEncodingFilter&lt;/filter-name&gt;
        &lt;filter-class&gt;org.springframework.web.filter.CharacterEncodingFilter&lt;/filter-class&gt;
        &lt;init-param&gt;
            &lt;param-name&gt;encoding&lt;/param-name&gt;
            &lt;param-value&gt;utf-8&lt;/param-value&gt;
        &lt;/init-param&gt;
    &lt;/filter&gt;
    &lt;filter-mapping&gt;
        &lt;filter-name&gt;CharacterEncodingFilter&lt;/filter-name&gt;
        &lt;url-pattern&gt;/*&lt;/url-pattern&gt;
    &lt;/filter-mapping&gt;
[/java]
