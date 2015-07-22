---
layout: post
title: 装饰模式
date: 2013-11-28 23:19
author: VERYYOUNG
comments: true
categories: [Design Patterns]
---
顾名思义，装饰模式就是给一个对象增加一些新的功能，而且是动态的，要求装饰对象和被装饰对象实现同一个接口，装饰对象持有被装饰对象的实例，关系图如下：
<img src="http://veryyoung.u.qiniudn.com/7niu_decorator.png" alt="decorator" />

Source类是被装饰类，Decorator类是一个装饰类，可以为Source类动态的添加一些功能，代码如下：
<pre lang="java">
public interface Sourceable {
    public void method();
}
</pre>

<pre lang="java">
public class Source implements Sourceable {
    @Override
    public void method() {
        System.out.println("the original method!");
    }
}
</pre>

<pre lang="java">
public class Decorator implements Sourceable {
    private Sourceable source;
    public Decorator(Sourceable source){
        this.source=source;

    }
    @Override
    public void method() {
        System.out.println("before decoratro");
        source.method();
        System.out.println("after decoratro");
    }
}
</pre>

测试类：

<pre lang="java">
public class DecoratorTest {
    public static void main(String[] args) {
        Sourceable source = new Source();
        Sourceable obj = new Decorator(source);
        obj.method();

    }

}
</pre>
输出：
before decorator!
the original method!
after decorator!
装饰器模式的应用场景：
1、需要扩展一个类的功能。
2、动态的为一个对象增加功能，而且还能动态撤销。（继承不能做到这一点，继承的功能是静态的，不能动态增删。）

继承属于扩展形式之一，但不见得是达到弹性设计的最佳方式。
在我们的设计中，应该允许行为可以被扩展，而无须修改现有的代码。
组合和委托可用于在运行时动态地加上新的行为。
除了继承，装饰者模式也可以让我们扩展行为。
装饰者模式意味着一群装饰者类， 这些类用来包装具体组件。
装饰者类反映出被装饰的组件类型（事实上，他们具有相同的类型，都经过接口或继承实现）。
装饰者可以在被装饰者的行为前面与/或后面加上自己的行为， 甚至将被装饰者的行为整个取代掉，而达到特定的目的。
你可以用无数个装饰者包装一个组件。
装饰者一般对组件的客户是透明的，除非客户程序依赖于组件的具体类型。
装饰者会导致设计中出现许多小对象，如果过度使用，会让程序变得很复杂

Tips：Java I/O源码大量的使用了装饰模式，读读I/O相信肯定能理解装饰模式
