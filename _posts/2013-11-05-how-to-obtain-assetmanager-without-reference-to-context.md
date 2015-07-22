---
layout: post
title: How to obtain AssetManager without reference to Context?
date: 2013-11-05 18:49
author: VERYYOUNG
comments: true
categories: [Android]
---
<p>I have a class that needs to obtain a reference to it's application's AssetManager. This class does not extend any sort of android UI class, so it doesn't have a getContext() method, or anything similar. Is there some sort of static Context.getCurrentApplicationContext() type of method?</p>

<blockquote>
  <p>To clarify: my class is intended to be used like a library, for other applications. It has no associated AndroidManifest.xml or control over the context which is calling it.</p>
</blockquote>

<h3>The key to this problem is :</h3>

<ol>
<li>Create a subclass of Application, for instance public class App extends Application </li>
<li>Set the android:name attribute of your <application> tag in the AndroidManifest.xml to point to your new class, e.g. android:name=".App"</li>
<li>In the onCreate() method of your app instance, save your context (e.g. this) to a static field named app and create a static method that returns this field, e.g. getApp():</li>
</ol>

<h3>This is how it should look:</h3>

<pre><code>public class App extends Application{

    private static Context mContext;

    @Override
    public void onCreate() {
        super.onCreate();
        mContext = this;
    }

    public static Context getContext(){
        return mContext;
    }
}
</code></pre>

<hr />

<p>Now you can use: <pre><code>App.getContext()</code></pre> whenever you want to get a context, and then 
<pre><code>getAssetManager()</code></pre> or <pre><code>App.getContext().getAssetManager()</code></pre>.</p>

<hr />

<p>refer <a href="http://stackoverflow.com/questions/4410328/how-to-obtain-assetmanager-without-reference-to-context">http://stackoverflow.com/questions/4410328/how-to-obtain-assetmanager-without-reference-to-context</a></p>
