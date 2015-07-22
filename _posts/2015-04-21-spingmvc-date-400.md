---
layout: post
title: SpingMVC接收Date 400
date: 2015-04-21 12:29
author: VERYYOUNG
comments: true
categories: [Java]
---
<p>springmvc在接收Date型表单的时候会报400</p>

<h2>需要指定具体的类型编辑器。</h2>

<p>1.在BaseController中增加方法initBinder，并使用注解@InitBinder标注，那么spring mvc在绑定表单之前，都会先注册这些编辑器。剩下的控制器都继承该类。</p>

<pre><code>@InitBinder
public void initBinder(WebDataBinder binder) {
    SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
    dateFormat.setLenient(false);
    binder.registerCustomEditor(Date.class, new CustomDateEditor(dateFormat, false));
}
</code></pre>

<p>2.实现WebBindingInitializer</p>

<pre><code>/**
 * Initialize web bindings
 */
public class MyAppBindingInitializer implements WebBindingInitializer {

    /**
     * Date pattern applied to all the web app dates
     */
    public static final String DATE_PATTERN = "yyyy-MM-dd"

    public void initBinder(WebDataBinder binder, WebRequest request) {
        // Date editor with pattern
        SimpleDateFormat dateFormat = new SimpleDateFormat(DATE_PATTERN);
        dateFormat.setLenient(false);
        binder.registerCustomEditor(Date.class, new CustomDateEditor(dateFormat, false));

        // Trim Strings
        binder.registerCustomEditor(String.class, new StringTrimmerEditor(true));
        // Number editors
        binder.registerCustomEditor(Integer.class, new CustomNumberEditor(Integer.class, true));
        binder.registerCustomEditor(Long.class, new CustomNumberEditor(Long.class, true));

        // Custom types
        binder.registerCustomEditor(Profile.class, new ProfileEditor());
        binder.registerCustomEditor(OrderType.class, new OrderTypeEditor());
    }

}
</code></pre>

<p>在xml里注册</p>

<pre><code> &lt;!-- Binder used to convert strings to other types in the web tier --&gt;
&lt;bean class="org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter"&gt;
    &lt;property name="webBindingInitializer"&gt;
        &lt;bean class="my.app.MyAppBindingInitializer "/&gt;
    &lt;/property&gt;
&lt;/bean&gt;
</code></pre>

