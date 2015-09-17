---
layout: post
title: AMD与CMD异同
date: 2015-9-17 20:58:45
author: VERYYOUNG
comments: true
categories: [Front End]
---

近来 AMD 和 CMD 的讨论异常的激烈，他们到底有哪些相同或不同的呢？


<!-- more -->

----------

本来想写篇文章说明一下，结果随便 Google 一下，发现 SeaJS 的作者玉伯已经说的很明白了！

直接贴链接吧！

1.	[SeaJS 与 RequireJS 的异同](https://github.com/seajs/seajs/issues/277)
2.	[AMD 和 CMD 的区别有哪些？](http://www.zhihu.com/question/20351507)

玉伯很耐心的在 Github 和知乎等地方很耐心的解答网友的问题，非常赞！！

-----------

个人理解：

SeaJS 和 RequireJS 都是为前端模块化编程提供的解决方案。

最大的不同点在于 SeaJS 是懒执行，RequireJS 是提前执行。

AMD 的性能会好一点，因为 RequireJS 会预先加载所有的模块，直到使用的时候才执行（会浪费资源）;
CMD 只有真正需要的时候才加载依赖，性能会差点。

前端开发和后端不同，后端绝大多数情况下是需要用的时候才加载模块，这样能避免浪费。

前端每次请求一个资源都会新开一个 http 请求，会很浪费资源，不如一次加载完的好。

所以可能后端开发者可能会比较习惯 CMD 的思想， 而前端开发者为了提高效率（减少 http 消耗，但可能会加载没执行到的模块）会使用 AMD 。


另外如果把整个网站的 JS 都打成一个包，就木有 CMD 这个概念了!





