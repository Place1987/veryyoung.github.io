---
layout: post
title: sea.js jquery not defined
date: 2015-9-11 16:11:26
author: VERYYOUNG
comments: true
categories: [Front End]
---

用sea.js的preload去加载bootstrap和jquery，会经常出现

	$ is not defined

<!-- more -->

----------

大概如下配置的：

	seajs.config({
		base: '/static/js/modules/',
		alias: {
		'jquery' : 'jquery.js',
		'bootstrap' : 'bootstrap/js/bootstrap.min.js'
		},
		preload : ['jquery', 'bootstrap'],
		charset : 'utf-8'
	})



首先得把所有引用的模块都得打成CMD模块。

用类似如下的代码：

	define(['jquery'], function(require, exports, module){
	
	});

包好之后还是会出现以上描述的问题。



原因是因为 bootstrap 也依赖了 jquery 。

而 preload 的加载数组是没有次序依赖的。和 seajs.use(array) 一样。

可以如下配置

	// 将 jQuery 暴露到全局
	seajs.modify('jquery', function(require, exports) {
	  window.jQuery = window.$ = exports
	})

或者在每个页面 use js 的时候都 use jquery。

其实也可以在common文件里面

	<scrpit src = "../jquery.js" ></scrpit>




参考：

1. [https://github.com/seajs/seajs/issues/286](https://github.com/seajs/seajs/issues/286)
2. [https://groups.google.com/forum/#!topic/seajs/pYhDVPNt4DI](https://groups.google.com/forum/#!topic/seajs/pYhDVPNt4DI)








