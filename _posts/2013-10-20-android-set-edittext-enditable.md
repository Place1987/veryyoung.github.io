---
layout: post
title: Android开发：设置文本输入框是否可编辑
date: 2013-10-20 00:38
author: VERYYOUNG
comments: true
categories: [Android]
---
<p>Android开发在layout配置文件中添加一个EditText：</p>

<pre><code>    &lt;EditText android:id="@+id/timeEt"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:cursorVisible="false"
    android:editable="false"/&gt;
</code></pre>

<p>最后一行提示：android:editable is deprecated: Use inputType instead，原来editable属性已经过时，google不再建议用户使用，可以用inputType属性代替，但是inputType属性值列表中并没有表示不可编辑的，经过多次尝试，发现可以用android:focusable设置：</p>

<pre><code>&lt;EditText android:id="@+id/dateEt"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:cursorVisible="false"
     android:focusable="false"/&gt;
</code></pre>

<p>参考  <a href="http://stackoverflow.com/questions/3928711/how-to-make-edittext-not-editable">http://stackoverflow.com/questions/3928711/how-to-make-edittext-not-editable</a></p>

