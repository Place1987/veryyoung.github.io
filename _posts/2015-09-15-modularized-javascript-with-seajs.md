---
layout: post
title: 使用 SeaJS进行JavaScript模块化编程
date: 2015-9-15 10:54:49
author: VERYYOUNG
comments: true
categories: [Front End]
---

传统的JavaScript编程很容易出现难以管理的现象，如依赖复杂、方法名冲突等各方面的弊端，SeaJS可以解决这个问题。


<!-- more -->

----------

SeaJS的是支付宝著名前端工程师开发的一个前端模块化开发框架。

SeaJS是一个遵循CommonJS规范的JavaScript模块加载框架，可以实现JavaScript的模块化开发及加载机制。

Sea.js 追求简单、自然的代码书写和组织方式，具有以下核心特性：

1.	简单友好的模块定义规范：Sea.js 遵循 CMD 规范，可以像 Node.js 一般书写模块代码。
2.	自然直观的代码组织方式：依赖的自动加载、配置的简洁清晰，可以让我们更多地享受编码的乐趣。
3.	Sea.js 还提供常用插件，非常有助于开发调试和性能优化，并具有丰富的可扩展接口。

使用Sea.js有如下好处:

1.	更好的分离	
2.	更好的代码组织方式
3.	按需加载
4.	避免命名冲突
5.	更好的依赖处理

用起来很简单

	// 所有模块都通过 define 来定义
	define(function(require, exports, module) {
	
		// 通过 require 引入依赖
		var $ = require('jquery');
		var Spinning = require('./spinning');
		
		// 通过 exports 对外提供接口
		exports.doSomething = ...
		
		// 或者通过 module.exports 提供整个接口
		module.exports = ...
	
	});
	



类似的项目还有：RequireJS、CommonJS 等


参考：

1.	[SeaJS官网](http://seajs.org/)
2.	[Javascript模块化编程（一）：模块的写法](http://www.ruanyifeng.com/blog/2012/10/javascript_module.html)
3.	[前端模块化开发的价值](https://github.com/seajs/seajs/issues/547)
4.	[SeaJS代码维护地址](https://github.com/seajs/seajs)
5.	[玉伯博客](https://lifesinger.github.io/)

