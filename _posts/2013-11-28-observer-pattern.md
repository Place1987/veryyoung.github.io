---
layout: post
title: 观察者模式
date: 2013-11-28 10:40
author: VERYYOUNG
comments: true
categories: [Design Patterns]
---
观察者模式很好理解，类似于邮件订阅和RSS订阅.
当我们浏览一些博客或wiki时，经常会看到RSS图标，就这的意思是，当你订阅了该文章，如果后续有更新，会及时通知你。
其实，简单来讲就一句话：当一个对象变化时，其它依赖该对象的对象都会收到通知，并且随着变化！
对象之间是一种一对多的关系。先来看看关系图：
<a href="http://veryyoung.u.qiniudn.com/7niu_uml.png"><img src="http://veryyoung.u.qiniudn.com/7niu_uml.png" alt="" title="uml" width="500" height="304" class="alignnone size-medium wp-image-92" /></a>
我解释下这些类的作用：SubjectClient类就是我们的主对象，Observer1和Observer2是依赖于AbstactSubject的对象，当AbstactSubject变化时，Observer1和Observer2必然变化。AbstractSubject类中定义着需要监控的对象列表，可以对其进行修改：增加或删除被监控对象，且当SubjectClient变化时，负责通知在列表内存在的对象。我们看实现代码：
一个IObserver接口：

	public interface IObserver {
	    public void update();
	}


两个实现类：

	public class Observer1 implements IObserver {
	
	    @Override
	    public void update() {
	        System.out.println("observer1 has received");
	    }
	}



	public class Observer2 implements IObserver {
	
	    @Override
	    public void update() {
	        System.out.println("observer2 has received");
	    }
	}


Subject接口及实现类：

	public interface Subject  {
	    public void add(IObserver observer);
	    public void delete(IObserver observer);
	    public void notifyObservers();
	    public void operation();
	}


	public class SubjectClient extends AbstractSubject {
	    @Override
	    public void operation() {
	        System.out.println("update self");
	        notifyObservers();
	    }
	}




	public class SubjectClient extends AbstractSubject {
	    @Override
	    public void operation() {
	        System.out.println("update self");
	        notifyObservers();
	    }
	}


测试类：

	public class ObserverTest{
	    public static void main(String[] args){
	        Subject subject = new SubjectClient();
	        subject.add(new Observer1());
	        subject.add(new Observer2());
	        subject.operation();
	    }
	}


输出：

	update self!
	observer1 has received!
	observer2 has received!
