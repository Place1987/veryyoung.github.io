---
layout: post
title: Java Annotation
date: 2015-01-05 21:28
author: VERYYOUNG
comments: true
categories: [Java]
---
<p>最近突然发现Java注解真心神器。一行简单的注解可以搞定N多事情。简直不能再方便了。</p>

<p>注解可以看成是一个接口，注解实例就是一个实现了该接口的动态代理类。 注解大多是用做对某个类、方法、字段进行说明，标识的。以便在程序运行期间我们通 过反射获得该字段或方法的注解的实例，来决定该做些什么处理或不该进行什么处理。</p>

<p>定义和调用注解的方法都很简单，这里就不说明了。</p>

<p>重点说明下怎么让注解work起来。</p>

<p>注解本身并不会做任何事情，它需要工具支持才会有用。比如JUnit4的@Test注解自身不会做任何事情，JUnit会识别并调用所有标识为@Test的方法，这种识别处理一般是采用代理模式，通过反射来调用。</p>

<p>大致代码如下</p>

<pre><code>import java.lang.annotation.Annotation;
import java.lang.reflect.Method;


public class ReadAnnotationInfoTest {
public static void main(String[] args) throws Exception {
    //测试AnnotationTest类，得到此类的类对象
    Class c = Class.forName(&amp;quot;className&amp;quot;);

    //获取该类所有声明的方法
    Method[] methods = c.getDeclaredMethods();

    //声明注解集合
    Annotation[] annotations;

    //遍历所有的方法得到各方法上面的注解信息
    for (Method method : methods) {
        //获取每个方法上面所声明的所有注解信息
        annotations = method.getDeclaredAnnotations();

        //再遍历所有的注解，打印其基本信息
        for (Annotation an : annotations) {
            System.out.println("方法名为：" + method.getName() + " 其上面的注解为：" +
                an.annotationType().getSimpleName());

            Method[] meths = an.annotationType().getDeclaredMethods();

            //遍历每个注解的所有变量
            for (Method meth : meths) {
                System.out.println("注解的变量名为：" + meth.getName());
            }
        }
    }
}
</code></pre>


<p>这个类可以得到类上的所有注解信息。 然后就可以根据需要植入代码段之类的了。</p>

