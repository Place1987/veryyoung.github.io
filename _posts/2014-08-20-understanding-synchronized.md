---
layout: post
title: 理解synchronized
date: 2014-08-20 15:58
author: VERYYOUNG
comments: true
categories: [Java]
---
Synchronized 是Java语言的关键字，可用来给对象和方法或者代码块加锁。
当它锁定一个方法或者一个代码块的时候，同一时刻最多只有一个线程执行这个段代码。
当两个并发线程访问同一个对象object中的这个加锁同步代码块时，一个时间内只能有一个线程得到执行。
另一个线程必须等待当前线程执行完这个代码块以后才能执行该代码块。
然而，当一个线程访问object的一个加锁代码块时，另一个线程仍然可以访问该object中的非加锁代码块。

synchronized关键字可以作为函数的修饰符，也可作为函数内的语句，也就是平时说的同步方法和同步语句块。
如果再细的分类，synchronized可作用于instance变量、object reference（对象引用）、static函数和class literals(类名称字面常量)身上。
在进一步阐述之前，我们需要明确几点：
A．无论synchronized关键字加在方法上还是对象上，它取得的锁都是对象，而不是把一段代码或函数当作锁――而且同步方法很可能还会被其他线程的对象访问。
B．每个对象只有一个锁（lock）与之相关联。
C．实现同步是要很大的系统开销作为代价的，甚至可能造成死锁，所以尽量避免无谓的同步控制。

还有一些技巧可以让我们对共享资源的同步访问更加安全：
1．  定义private 的instance变量+它的 get方法，而不要定义public/protected的instance变量。如果将变量定义为public，对象在外界可以绕过同步方法的控制而直接取得它，并改动它。这也是JavaBean的标准实现方式之一。
2．  如果instance变量是一个对象，如数组或ArrayList什么的，那上述方法仍然不安全，因为当外界对象通过get方法拿到这个instance对象的引用后，又将其指向另一个对象，那么这个private变量也就变了，岂不是很危险。 这个时候就需要将get方法也加上synchronized同步，并且，只返回这个private对象的clone()――这样，调用端得到的就是对象副本的引用了。
