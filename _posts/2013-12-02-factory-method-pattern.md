---
layout: post
title: 工厂方法模式
date: 2013-12-02 20:20
author: VERYYOUNG
comments: true
categories: [Design Patterns]
---
在面向对象程序设计中，工厂通常是一个用来创建其他对象的对象。工厂是构造方法的抽象，用来实现不同的分配方案。
工厂对象通常包含一个或多个方法，用来创建这个工厂所能创建的各种类型的对象。这些方法可能接收参数，用来指定对象创建的方式，最后返回创建的对象。
有时，特定类型对象的控制过程比简单地创建一个对象更复杂。在这种情况下，工厂对象就派上用场了。工厂对象可能会动态地创建产品对象的类，或者从对象池中返回一个对象，或者对所创建的对象进行复杂的配置，或者应用其他的操作。
这些类型的对象很有用。几个不同的设计模式都应用了工厂的概念，并可以使用在很多语言中。例如，在《设计模式》一书中，像工厂方法模式、抽象工厂模式、生成器模式，甚至是单例模式都应用了工厂的概念。
举例如下：（我们举一个发送邮件和短信的例子）
UML图如下：
<img src="http://veryyoung.u.qiniudn.com/7niu_decorator.png" alt="" />
首先，创建二者的共同接口：
<pre lang="java">
public interface Sender {
	public void send();
}
</pre>
其次，创建实现类：
<pre lang="java">
public class SmsSender implements Sender {

	@Override
	public void send() {
		// TODO Auto-generated method stub
		System.out.println("SmsSender invoke!");
		
	}

}
</pre>


<pre lang="java">
public class MailSender implements Sender {

	@Override
	public void send() {
		// TODO Auto-generated method stub
		System.out.println("mail sender invoke!");

	}

}
</pre>
最后，建工厂类：
<pre lang="java">
public class SendFactory {
	
	public static Sender produceMail(){
		return new MailSender();
	}
	
	public static Sender produceSms(){
		return new SmsSender();
	}
	
	
}
</pre>

测试类:
<pre lang="java">
public class FactoryTest {
	public static void main(String[] args) {
		Sender sender = SendFactory.produceMail();
		sender.send();
	}

}
</pre>


下列情况可以考虑使用工厂方法模式：
创建对象需要大量重复的代码。
创建对象需要访问某些信息，而这些信息不应该包含在复合类中。
创建对象的生命周期必须集中管理，以保证在整个程序中具有一致的行为。

