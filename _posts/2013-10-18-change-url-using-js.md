---
layout: post
title: 使用 JavaScript 修改浏览器 URL 地址栏
date: 2013-10-18 20:48
author: VERYYOUNG
comments: true
categories: [Front End]
---
<h3>现在的浏览器里,有一个十分有趣的功能</h3>

<p>你可以在不刷新页面的情况下修改浏览器URL;在浏览过程中.你可以将浏览历史储存起来，当你在浏览器点击后退按钮的时候，你可以冲浏览历史上获得回退的信息，这听起来并不复杂，是可以实现的，我们来编写些代码。来看看它是如何工作的。</p>

<pre><code>var stateObject = {};
var title = "Wow Title";
var newUrl = "/my/awesome/url";
history.pushState(stateObject,title,newUrl);
</code></pre>

<p>History 对象 pushState() 这个方法有3个参数,你可以从上面的例子看到。第一个参数，是一个Json对象 , 在你储存有关当前URl的任意历史信息.第二个参数,title 就相当于传递一个文档的标题 ，第三个参数是用来传递新的URL. 你将看到浏览器的地址栏发生变化而当前页面并没刷新。</p>

<p>让我们看一个例子，在这个例子中我们将在每个独立的URL中存储一些任意数据。</p>

<pre><code>for(i=0;i&lt;5;i++){
    var stateObject = {id: i};
    var title = "Wow Title "+i;
    var newUrl = "/my/awesome/url/"+i;
    history.pushState(stateObject,title,newUrl);
}
</code></pre>

<p>现在运行，点击浏览器的返回按钮，查看URL是怎么改变的。对于每次URL的改变，是因为它存储了历史状态“id”以及对应的值。但是我们怎么重新获得历史状态，并且在此基础上做些事情呢？我们需要对“popstate”添加事件监听器，这将会在每次历史对象的状态改变的时候触发。</p>

<pre><code>for(i=0;i&lt;5;i++){
    var stateObject = {id: i};
    var title = "Wow Title "+i;
    var newUrl = "/my/awesome/url/"+i;
    history.pushState(stateObject,title,newUrl);
    alert(i);
}

window.addEventListener('popstate', function(event) {
readState(event.state);
});

function readState(data){
    alert(data.id);
}
</code></pre>

<p>现在你会看到无论什么时候你点击返回按钮，一个“popstate”事件就会被触发。我们的事件侦听器然后检索历史状态对象与之关联的URL,并提示“id”的值。</p>

<h3>它是非常的简单和有趣，不是吗？</h3>

