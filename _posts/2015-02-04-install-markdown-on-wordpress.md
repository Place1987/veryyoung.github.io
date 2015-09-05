---
layout: post
title: Install MarkDown On Wordpress
date: 2015-02-04 23:44
author: VERYYOUNG
comments: true
categories: [Blog]
---
<p>今天突然想用markdown写博文，这样应该会方便不少。</p>

<p>开工</p>

<h3>1.下载插件。</h3>

<p>这里我选择了<a href="http://brettterpstra.com/projects/markdown-quicktags/">Markdown QuickTags</a></p>

<p>在官网看到</p>

<blockquote>
  <p>!This plugin hasn't been updated in over 2 years. It may no longer be maintained or supported and may have compatibility issues when used with more recent versions of WordPress.</p>
</blockquote>

<p>有点被惊呆</p>

<h3>2.启用插件</h3>

<p>下载完该插件之后，放入WordPress的plugins文件夹下，上传代码，然后再后台启用即可</p>

<h3>3.改变样式</h3>

<p>发现wordp对&lt;pre&gt;&lt;code&gt;的支持不太好,样式略逊</p>

<p>随便打开一个支持markdown的网站，查看源代码
找到有关code的css，复制进wordp主题css文件里
我使用的是MarkdownPad 2的浏览器预览</p>

<p>代码如下</p>

<pre><code>pre, code, tt {
  font-size: 12px;
  font-family: Consolas, "Liberation Mono", Courier, monospace;
}

code, tt {
  margin: 0 0px;
  padding: 0px 0px;
  white-space: nowrap;
  border: 1px solid #eaeaea;
  background-color: #f8f8f8;
  border-radius: 3px;
}

pre&gt;code {
  margin: 0;
  padding: 0;
  white-space: pre;
  border: none;
  background: transparent;
}

pre {
  background-color: #f8f8f8;
  border: 1px solid #ccc;
  font-size: 13px;
  line-height: 19px;
  overflow: auto;
  padding: 6px 10px;
  border-radius: 3px;
}

pre code, pre tt {
  background-color: transparent;
  border: none;
}
</code></pre>

<h3>4.使markdown生效</h3>

<p>我一般是在MarkdownPad 2写完文章，复制进WordPress文章发布的地方，点击下面的“Render”，发布即可。在发布之前还可以点左上角的“放大镜”去preview哦。</p>

<hr />

<p>好啦！可以用markdown的语法写博文啦。</p>

<hr />

<p>近期准备用markdown重构所有博文！</p>

