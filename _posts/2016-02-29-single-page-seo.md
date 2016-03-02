---
layout: post
title: 单页面架构的 SEO 优化
date: 2016-2-29 14:06:18
author: VERYYOUNG
comments: true
categories: [Others]
---

单页面架构的 dom 结构是用 js 动态构建出来的，而搜索引擎抓取的时候是不管 js 的，这样单页面架构是很不利于 SEO 的，而 SEO 对于一个对外的应用来说是非常重要的，放弃 SEO 等于放弃了网站的最大的流量入口：搜索引擎。

单页面应用 SEO 优化的思路就是判断请求是否来自搜索引擎，如果是搜索引擎在爬取页面，提供一个无界面的浏览器去访问网页，得到通过 js 渲染过后的 html 代码，再返回给搜索引擎。

下面说说[搜狗新颜](http://xinyan.cn)是怎么做的。

<!-- more -->

# 1.去掉 url 中的井号

单页面应用的链接中一般会带有 # 号（url hash），这对搜索引擎来说是非常不友好的，得把 # 去掉。

前端一个个去，注意不要有遗漏就行了。

去完之后，[http://xinyan.cn/#item/list/](http://xinyan.cn/#item/list/) 会变成 [http://xinyan.cn/item/list/](http://xinyan.cn/item/list/)，这时候访问必然会 404，后端需要做对应的响应。

拦截所有的 url 请求（过滤掉静态文件，restfull 接口），forward 到 index.jsp (单页面的主体页面)。

后端代码类似如下 


    if (needForward(request)) {
        request.getRequestDispatcher("/index.jsp").forward(request, response);
        return;
    }
    


# 2.对爬虫来的请求单独处理

如果请求来自爬虫，则由后端去响应请求，突出采用某种方案渲染好后的 html 页面源码；如果请求来自普通用户，直接按照原来的方案，用 js 去渲染 dom。


## 2.1 如何判断请求是否来自爬虫

爬虫在爬取页面的时候，都会在 request header 里面带上 USER-AGENT 来标示身份。

常见的搜索引擎 UA 可以参考 [http://www.wilf.cn/post/search-engine-bots.html](http://www.wilf.cn/post/search-engine-bots.html)。

后端的大致代码如下


    /**
     * 判断请求是否来自爬虫
     *
     * @param request
     * @return
     */
    public static boolean isSpider(HttpServletRequest request) {
        String ua = request.getHeader("USER-AGENT");
        if (StringUtils.isEmpty(ua)) {
            return false;
        }
        if (ua.contains("Baidu") || ua.contains("Google") || ua.contains("Yahoo") || ua.contains("Sogou")
                || ua.contains("360") || ua.contains("bing") || ua.contains("Soso") || ua.contains("Youdao")
                || ua.contains("Easou")) {
            return true;
        }
        return false;
    }
    
    

## 2.2 针对来自爬虫的请求单独响应

单页面的 SEO 都需要借助于 [Headless browser](https://en.wikipedia.org/wiki/Headless_browser)，通过 Headless browser 能开启一个无界面的浏览器，请求页面，将渲染好的页面源码返回给后端。

Github 上有个仓库列举出了常用的 Headless browser 以及对编程语言、系统环境的支持程度。

地址[https://github.com/dhamaniasad/HeadlessBrowsers](https://github.com/dhamaniasad/HeadlessBrowsers)

试了几个 Java 的方案，对 Js 的支持都不太靠谱，最后尝试了使用好评度最高的 [PhantomJS](http://phantomjs.org/)。

PhantomJs 对 Js 的支持非常完美，渲染出来的页面和 Js 渲染出来的一样。


PhantomJS 是基于命令行的工具，需要用后端语言来调用命令行，得到命令行的输出，最后返回给前端。




# 3. 遇到的一些问题以及解决方案

## 3.1 在 Windows 能得到输出，在 Linux 得不到

相同的一套代码，在本机（Windows） 运行的好好的，在 QA 环境却没有任何输出，而在 QA 环境直接执行命令是有返回结果的。

遇到这个问题之后一直怀疑是 Java Runtime.getRuntime().exec(cmd) 之后遇到的问题，采用了网上的很多方案都不能解决。

纠结了很久之后才发现原因是 QA 环境没有访问外网的权限，导致没输出，而在命令行测试的时候访问的是内网的 url。


之前代码里面做的是接收到请求之后，直接把请求 url 转给 PhantomJS，而请求的 url 是 xinyan.cn 这种，服务器是没有访问外网权限的。

解决方案：把请求转发到 "http://localhost:" + request.getLocalPort() + request.getRequestURI()。

比如请求 url 是 [http://xinyan.cn/item/list/](http://xinyan.cn/item/list/)，转发到 [http://localhost:8080/item/list/](http://localhost:8080/item/list/)。

相当于是自己请求自己，这样就克服了服务器不能访问外网的问题，而且响应速度也大大的提升了。



## 3.2 PhantomJS 抓到的数据乱码

在执行请求执行设定

    phantom.outputEncoding = "gb2312";
    
问题解决！







