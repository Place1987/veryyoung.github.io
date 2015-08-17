---
layout: post
title: 理解Lock
date: 2014-08-21 21:12
author: VERYYOUNG
comments: true
categories: [Java]
---
Lock是java.util.concurrent.locks包下的接口。


Lock 实现提供了比使用synchronized 方法和语句可获得的更广泛的锁定操作，它能以更优雅的方式处理线程同步问题。


锁像synchronized同步块一样，是一种线程同步机制，但比Java中的synchronized同步块更复杂。因为锁（以及其它更高级的线程同步机制）是由synchronized同步块的方式实现的，所以我们还不能完全摆脱synchronized关键字（这说的是Java 5之前的情况）。

自Java 5开始，java.util.concurrent.locks包中包含了一些锁的实现，因此你不用去实现自己的锁了。但是你仍然需要去了解怎样使用这些锁，且了解这些实现背后的理论也是很有用处的。

Java中可以使用Lock和Synchronized的可以实现对某个共享资源的同步，同时也可以实现对某些过程的原子性操作。

Lock可以使用Condition进行线程之间的调度，Synchronized则使用Object对象本身的notify, wait, notityAll调度机制，这两种调度机制有什么异同呢？

Condition是Java5以后出现的机制，它有更好的灵活性，而且在一个对象里面可以有多个Condition（即对象监视器),则线程可以注册在不同的Condition，从而可以有选择性的调度线程，更加灵活。

Synchronized就相当于整个对象只有一个单一的Condition（即该对象本身）所有的线程都注册在它身上，线程调度的时候之后调度所有得注册线程，没有选择权，会出现相当大的问题 。

所以，Lock 实现提供了比使用 synchronized 方法和语句可获得的更广泛的锁定操作。此实现允许更灵活的结构，可以具有差别很大的属性，可以支持多个相关的 Condition 对象。

锁是控制多个线程对共享资源进行访问的工具。通常，锁提供了对共享资源的独占访问。一次只能有一个线程获得锁，对共享资源的所有访问都需要首先获得锁。不过，某些锁可能允许对共享资源并发访问，如 ReadWriteLock 的读取锁。

synchronized 方法或语句的使用提供了对与每个对象相关的隐式监视器锁的访问，但却强制所有锁获取和释放均要出现在一个块结构中：当获取了多个锁时，它们必须以相反的顺序释放，且必须在与所有锁被获取时相同的词法范围内释放所有锁。

虽然 synchronized 方法和语句的范围机制使得使用监视器锁编程方便了很多，而且还帮助避免了很多涉及到锁的常见编程错误，但有时也需要以更为灵活的方式使用锁。例如，某些遍历并发访问的数据结果的算法要求使用 "hand-over-hand" 或 "chain locking"：获取节点 A 的锁，然后再获取节点 B 的锁，然后释放 A 并获取 C，然后释放 B 并获取 D，依此类推。Lock 接口的实现允许锁在不同的作用范围内获取和释放，并允许以任何顺序获取和释放多个锁，从而支持使用这种技术。

需要注意的是，用sychronized修饰的方法或者语句块在代码执行完之后锁自动释放，而用Lock需要我们手动释放锁，所以为了保证锁最终被释放(发生异常情况)，要把互斥区放在try内，释放锁放在finally内。
