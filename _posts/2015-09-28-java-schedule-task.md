---
layout: post
title: Java 常用定时任务方案
date: 2015-9-28 10:05:34
author: VERYYOUNG
comments: true
categories: [Java]
---
定时任务是非常常见的需求，比如定期的去汇总数据，定期的清除垃圾等。
Java 提供了很多定时任务的方案，下面简单的列举一下。

<!-- more -->

----------

1.  利用 thread 的sleep
    新开一个线程，死循环运行，通过 sleep 的达到定时运行的效果。
    
            public static void main(String[] args) {
                
                final long timeInterval = 1000;
                
                Runnable runnable = new Runnable() {
                    public void run() {
                        while (true) {
                            System.out.println(System.currentTimeMillis());
                            try {
                                Thread.sleep(timeInterval);
                            } catch (InterruptedException e) {
                                e.printStackTrace();
                            }
                        }
                    }
                };
                
                Thread thread = new Thread(runnable);
                thread.start();
            }
    
    实现很简单，但功能很弱，比如不能设定第一次运行时间。


2.  使用 Timer、TimerTask 

    Timer 是一种定时器工具，用来在一个后台线程计划执行指定任务，而 TimerTask 一个抽象类，它的子类代表一个可以被 Timer 计划的任务。
    
            public static void main(String[] args) {
    
                final long delay = 0;
                final long timeInterval = 1000;
        
                TimerTask task = new TimerTask() {
                    @Override
                    public void run() {
                        System.out.println(System.currentTimeMillis());
                    }
                };
        
                Timer timer = new Timer();
                timer.schedule(task, delay, timeInterval);
            }
            
    
    Timer 可以很方便的去根据条件取消任务的调度。调用
        
        timer.cancle();
    
    即可。
    
    因为 Java 不是实时的，所以，我们在上个程序中表达的原义并不能够严格执行，例如有时可能资源调度紧张1.5秒以后才执行下一次，有时候又0.5秒执行。
    如果我们调用的是 scheduleAtFixedRate，那么 Timer 会尽量让你的 timeTask 执行的频率保持在1秒一次。

3.  使用 ScheduledExecutorService

    ScheduledExecutorService 是 java.util.concurrent 包里，做为并发工具类被引进的。
    相比于Timer的单线程，它是通过线程池的方式来执行任务的。
    
        public static void main(String[] args) {
    
            final long delay = 0;
            final long timeInterval = 1000;
    
            Runnable runnable = new Runnable() {
                public void run() {
                    System.out.println(System.currentTimeMillis());
                }
            };
    
            ScheduledExecutorService service = Executors.newSingleThreadScheduledExecutor();
            service.scheduleAtFixedRate(runnable, delay, timeInterval, TimeUnit.MILLISECONDS);
        }
    
    
4.  使用 spring-task

    spring-task 是 Spring 自带的任务调度工具，可以将它看成一个轻量级的 Quartz，而且使用起来比 Quartz 简单许多。
    
    使用很简单，在 spring 的 xml 配置文件中简单的配置下
    
        <context:component-scan annotation-config="true" base-package="me.veryyoung.task"/>
    
        <task:scheduler id="scheduler" pool-size="10"/>
        <task:executor id="executor" pool-size="10"/>
        <task:annotation-driven scheduler="scheduler" executor="executor"/>
        
        
    
    在需要调度的方法上 加上 @Scheduled 就行。
    
    
        @Scheduled(fixedDelay = 1000)
        public void schedule() {
            System.out.println(System.currentTimeMillis());
        }
        
        
    支持 cron 表达式。


5.  [Quartz](http://quartz-scheduler.org/)

      Quartz对任务调度的领域问题进行了高度的抽象，提出了调度器、作业任务和触发器这3个核心的概念。
      支持丰富多样的调度方法，可以满足各种常规及特殊需求，并且提供了分布式和集群支持。
      
      Quartz 作业调度框架所提供的 API 在两方面都表现极佳：既全面强大，又易于使用。Quartz 可以用于简单的作业触发，也可以用于复杂的 JDBC 持久的作业存储和执行。



