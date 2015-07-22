---
layout: post
title: 解决@ResponseBody 406
date: 2015-03-18 17:20
author: VERYYOUNG
comments: true
categories: [Java]
---
<h2>#解决@ResponseBody 406</h2>

<p>使用SpringMvc的 @ResponseBody，想返回Json，出现406
<img src="http://ww1.sinaimg.cn/large/9732f922jw1eqa03mar9nj20qn078wg5.jpg" alt="" /></p>

<p>经google得知需要如下配置。</p>

<pre><code>&lt;bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter"&gt;
    &lt;property name="messageConverters"&gt;
        &lt;list&gt;
            &lt;ref bean="mappingJackson2HttpMessageConverter" /&gt;&lt;!-- json转换器 --&gt;
        &lt;/list&gt;
    &lt;/property&gt;
&lt;/bean&gt;
</code></pre>

<p>not work，继续报错。</p>

<pre><code>org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter#0' defined in ServletContext resource [/WEB-INF/springmvc-servlet.xml]: Initialization of bean failed; nested exception is java.lang.NoClassDefFoundError: com/fasterxml/jackson/databind/ObjectMapper
</code></pre>

<p>很明显了，少了jackson的依赖。</p>

<p>在pom里添加</p>

<pre><code>    &lt;dependency&gt;
        &lt;groupId&gt;com.fasterxml.jackson.core&lt;/groupId&gt;
        &lt;artifactId&gt;jackson-core&lt;/artifactId&gt;
        &lt;version&gt;2.5.1&lt;/version&gt;
    &lt;/dependency&gt;
    &lt;dependency&gt;
        &lt;groupId&gt;com.fasterxml.jackson.core&lt;/groupId&gt;
        &lt;artifactId&gt;jackson-databind&lt;/artifactId&gt;
        &lt;version&gt;2.5.1&lt;/version&gt;
    &lt;/dependency&gt;
</code></pre>

<p>done！</p>

<p><img src="http://ww2.sinaimg.cn/large/9732f922jw1eqa073d3rjj21290ehn3v.jpg" alt="" /></p>

