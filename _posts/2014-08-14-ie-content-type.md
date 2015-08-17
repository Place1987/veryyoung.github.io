---
layout: post
title: IE解释Content-Type
date: 2014-08-14 17:54
author: VERYYOUNG
comments: true
categories: [Uncategorized]
---

做客户的一个专题，四个静态页面。

点击新窗口打开，target="_blank"

上线之后，客户打电话过来，反映IE会显示是文件，只能下载，不能打开。
纳闷了！！！怎么回事？

页面后缀是special/1  2 3 4

首先想到的是，是否IE不支持数字作为后缀？

在IE console中修改页面代码，改为1.html，能正常弹出一个404页面。
修改controller，改为special/first ...

重新提交，用ie再次打开，fuck，还是下载....
蛋疼了！！

继续console

找到

	 Content-Type:*/*;charset=UTF-8

正常情况下应该是

	 Content-Type:text/html;charset=UTF-8

好吧，明白了，controller里面没有设定Content-Type，
一些现代浏览器可以识别，IE直接当成文件了...

解决办法很简单，加上一句

	 @Produces(MediaType.TEXT_HTML)

以后老实的设定好类型！
