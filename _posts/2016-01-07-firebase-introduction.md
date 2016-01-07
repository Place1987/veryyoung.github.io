---
layout: post
title: firebase：0 后端代码实现实时交互
date: 2016-1-7 23:32:02
author: VERYYOUNG
comments: true
categories: [Others]
---

>Firebase can power your app's backend, including data storage, user authentication, static hosting, and more. Focus on creating extraordinary user experiences. We'll take care of the rest.

使用 Firebase ，开发者无需担心数据存储问题，无需架设自己的服务器，就可以让自己的 APP 或 web 应用实现实时交互功能。


<!-- more -->

----------

前段时间参加了一个内部的黑客马拉松，需要做实时交互，如果用 MongoDB + WebSocket 实现挺麻烦的，然后果断的采用了 Firebase。

数据交互的核心代码如下：

    <script>

        var firebase = new Firebase('https://xop8xa2rcvk.firebaseio-demo.com/');

        firebase.push(text);


        firebase.on('child_added', function (snapshot) {
            var message = snapshot.val();
            console.log(message);
        });


    </script>
    
哈哈，就是这么简单！

new Firebase 就生成了一个 “聊天室”， push 就把数据推送到服务器了，然后可以实时监听数据的变化，这么复杂繁琐的功能就这几行代码就搞定了！！

[Firebase 官网](https://www.firebase.com/) 有很详细教程，跟着走一遍，五分钟就大概了解了。

Firebase 的这个思路非常不错，这样会给开发者提供非常大的便捷，开发者可以 0 后端代码，不需要服务器和数据库都能实现数据存储、传输等功能了。

-----

Firebase 被 Google 收购了，被 Google 收购也就意味着在国内使用会不太顺畅。

国内的替代品比较多，现在也很火。

1.  [ApiCloud](http://www.apicloud.com/)
2.  [LeanCloud](https://leancloud.cn/)
3.  [野狗](https://www.wilddog.com/)