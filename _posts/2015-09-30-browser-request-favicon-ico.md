---
layout: post
title: favicon.ico 的一些优化意见
date: 2015-9-30 14:33:06
author: VERYYOUNG
comments: true
categories: [Front End]
---
大部分浏览器都会请求当前网页根目录下的 /favicon.ico ,如果处理得不得当，会返回 404，有的甚至会引其它意想不到的错误，比如被拦截器拦截到。

<!-- more -->

----------
各个浏览器请求 /favicon.ico  的策略会不同。

Chrome 每次访问自动请求，FireFox  第一次访问请求，IE 不请求（需页面设置)，国产浏览器的策略大都和 IE 相同。

----------

浏览器请求 /favicon.ico 的地址也可能不同。（真是涨姿势了！）

Chrome、Firefox 浏览器默认会请求 link 的 href 所对应的图标，如果不存在 link， 则去请求 http://host:port/favicon.ico；

搜狗、IE 等浏览器默认会请求 link 的 href 所对应的图标，如果不存在 link，不请求。

360 等国产浏览器默认会请求 link 的 href 所对应的图标，如果不存在， 则去请求 http://host/favicon.ico，忽略掉端口。

----------

建议：

1.  配置根目录能访问到的 favicon.ico
2.  尽量在每个页面 link href favicon.ico
3.  如果你的网站带端口，那么尤其要注意360等浏览器，它们在请求 favicon.ico 的时候会忽略端口号的。
4.  在 SpringMVC 可以在 webapp 目录下放置一个 favicon.ico， 然后在 web.xml 中配置
        
        <servlet-mapping>
                <servlet-name>default</servlet-name>
                <url-pattern>/favicon.ico</url-pattern>
         </servlet-mapping>
    
5.  最好用 nginx 代理 /favicon.ico，设置一个比较长的过期时间，同时不打印访问 ico 相关的日志。

        location /favicon.ico {  
            root /data/asserts/;  
            gzip_static on;  
            expires max;  
            add_header Cache-Control public;
            access_log off;
        }  
    
    