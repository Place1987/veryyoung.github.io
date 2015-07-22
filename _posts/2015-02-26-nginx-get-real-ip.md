---
layout: post
title: Nginx得到反向代理前的真实IP
date: 2015-02-26 16:14
author: VERYYOUNG
comments: true
categories: [HTTP]
---
<h3>Nginx得到反向代理前的真实IP</h3>

<p>Java Servlet可以通过request.getRemoteAddr()得到请求的客户端的IP</p>

<p>现在一般情况下都不是直接用Tomcat或者Jetty这样的web容器，都会在前面加上Nginx或者Tengine之类的静态Web容器来反向代理。
由于经过了Nginx转发请求，通过request.getRemoteAddr()得到的IP就成了127.0.0.1
可以在Nginx配置里加上</p>

<pre><code>    proxy_set_header x-forwarded-for $proxy_add_x_forwarded_for;
</code></pre>

<p>这个意思是在nginx做反向代理的时候把代理前的地址放到http header 的 x-forwarded-for 中，然后如下获取：
     public static String getIP(HttpServletRequest request) {
        String IP = request.getRemoteAddr();
        String forwarded = request.getHeader("x-forwarded-for");</p>

<pre><code>    if (forwarded != null) {
        forwarded = forwarded.split(",", 2)[0];
        if (pattern.matcher(forwarded).matches()) {
            return forwarded;
        }
    }
    if (pattern.matcher(IP).matches()) {
        return IP;
    } else {
        logger.warn("IP is not valid.[IP=" + IP + "]");
        return "";
    }
}
</code></pre>
