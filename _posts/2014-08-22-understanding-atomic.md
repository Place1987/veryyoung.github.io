---
layout: post
title: 理解Atomic
date: 2014-08-22 23:36
author: VERYYOUNG
comments: true
categories: [Java]
---

Atomic一词跟原子有点关系，后者曾被人认为是最小物质的单位。
计算机中的Atomic是指不能分割成若干部分的意思。如果一段代码被认为是Atomic，则表示这段代码在执行过程中，是不能被中断的。
通常来说，原子指令由硬件提供，供软件来实现原子方法（某个线程进入该方法后，就不会被中断，直到其执行完成）。


DK1.5的原子包：java.util.concurrent.atomic

这个包里面提供了一组原子类。其基本的特性就是在多线程环境下，当有多个线程同时执行这些类的实例包含的方法时，具有排他性，即当某个线程进入方法，执行其中的指令时，不会被其他线程打断，而别的线程就像自旋锁一样，一直等到该方法执行完成，才由JVM从等待队列中选择一个另一个线程进入，这只是一种逻辑上的理解。实际上是借助硬件的相关指令来实现的，不会阻塞线程(或者说只是在硬件级别上阻塞了)。


其中的类可以分成4组

AtomicBoolean，AtomicInteger，AtomicLong，AtomicReference

AtomicIntegerArray，AtomicLongArray

AtomicLongFieldUpdater，AtomicIntegerFieldUpdater，
AtomicReferenceFieldUpdater

AtomicMarkableReference，AtomicStampedReference，AtomicReferenceArray


Atomic类的作用

使得让对单一数据的操作，实现了原子化

使用Atomic类构建复杂的，无需阻塞的代码

访问对2个或2个以上的atomic变量（或者对单个atomic变量进行2次或2次以上的操作）通常认为是需要同步的，以达到让这些操作能被作为一个原子单元。

2.1 AtomicBoolean , AtomicInteger, AtomicLong, 

AtomicReference

这四种基本类型用来处理布尔，整数，长整数，对象四种数据。

构造函数（两个构造函数）

默认的构造函数：初始化的数据分别是false，0，0，null

带参构造函数：参数为初始化的数据

set( )和get( )方法：可以原子地设定和获取atomic的数据。类似于volatile，保证数据会在主存中设置或读取

getAndSet( )方法

原子的将变量设定为新数据，同时返回先前的旧数据

其本质是get( )操作，然后做set( )操作。尽管这2个操作都是atomic，但是他们合并在一起的时候，就不是atomic。在Java的源程序的级别上，如果不依赖synchronized的机制来完成这个工作，是不可能的。只有依靠native方法才可以。

compareAndSet( ) 和weakCompareAndSet( )方法

这两个方法都是conditional modifier方法。这2个方法接受2个参数，一个是期望数据(expected)，一个是新数据(new)；如果atomic里面的数据和期望数据一致，则将新数据设定给atomic的数据，返回true，表明成功；否则就不设定，并返回false。

对于AtomicInteger、AtomicLong还提供了一些特别的方法。

getAndIncrement( )、incrementAndGet( )、getAndDecrement( )、decrementAndGet ( )、addAndGet( )、getAndAdd( )以实现一些加法，减法原子操作。

(注意 --i、++i不是原子操作，其中包含有3个操作步骤：第一步，读取i；第二步，加1或减1；第三步：写回内存)


设计原子类主要用作各种构造块，用于实现非阻塞数据结构和相关的基础结构类。compareAndSet 方法不是锁定的常规替换方法。仅当对象的重要更新限定于单个 变量时才应用它。

原子类不是 java.lang.Integer 和相关类的通用替换方法。它们不定义诸如 hashCode 和 compareTo 之类的方法。（因为原子变量是可变的，所以对于哈希表键来说，它们不是好的选择。）另外，仅为那些通常在预期应用程序中使用的类型提供类。例如，没有表示 byte 的原子类。这种情况不常见，如果要这样做，可以使用 AtomicInteger 来保持 byte 值，并进行适当的强制转换。也可以使用 Float.floatToIntBits 和 Float.intBitstoFloat 转换来保持 float 值，使用 Double.doubleToLongBits 和 Double.longBitsToDouble 转换来保持 double 值。


注意：Atomic变量从Java5才开始提供！
