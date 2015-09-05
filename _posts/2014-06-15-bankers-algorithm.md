---
layout: post
title: 银行家算法
date: 2014-06-15 21:38
author: VERYYOUNG
comments: true
categories: [Algorithm]
---

一．实验名称：银行家算法

二．实验目的：
   银行家算法是避免死锁的一种重要方法，通过编写 一个简单的银行家算法程序，加深了解有关资源申请、避免死锁等概念，并体会和了解死锁和避免死锁的具体实施方法。

三．实验原理说明：

   银行家算法是一种最有代表性的避免死锁的算法。在避免死锁方法中允许进程动态地申请资源，但系统在进行资源分配之前，应先计算此次分配资源的安全性，若分配不会导致系统进入不安全状态，则分配，否则等待。

　　　银行家算法是由操作系统执行，每当一个进程请求资源。算法由拒绝或延期的请求，如果它确定接受该请求可以把系统处于不安全状态（即一个可能发生死锁）来避免死锁。当一个新进程进入一个系统，它必须声明它可能曾经声称每个资源类型的实例的最大数目;显然，该数不得超过资源的系统中的总数。此外，当一个进程都有要求所有资源必须在有限时间内归还。

　　　对于银行家算法的工作，需要知道以下三件事情： 
    1. 每个线程有可能请求多少资源？
　　　2. 每个线程目前持有多少资源？
　　　3. 对于每种资源，系统持有多少？
　　　
　　　仅当满足以下条件时，资源可用被分配给一个线程：
　　　要求≤最大，因为过程已经越过了它提出的最大要求设定其他错误条件。 
　　　要求≤可用，否则进程等待，直到资源可用。
　　　
四：算法流程图：

<img src="http://img.blog.163.com/photo/1HUzjbGGobUsBo__7EUIMg==/3384736594946684439.jpg" alt="http://img.blog.163.com/photo/1HUzjbGGobUsBo__7EUIMg==/3384736594946684439.jpg" />

五:算法实现
实验环境：Ubuntu14.04  Java8  IntelliJ IDEA13

代码如下：


	package me.veryyoung.banker;
	
	/**
	 * Created by veryyoung on 14-6-15.
	 */
	
	import javax.swing.JOptionPane;
	
	public class Main {
	    /**五:算法实现
	
	     * @param args the command line arguments
	     */
	    public static void main(String[] args) {
	        int n = Integer.parseInt(JOptionPane.showInputDialog(&quot;Number Of Process:&quot;));
	        int m = Integer.parseInt(JOptionPane.showInputDialog(&quot;Resource Type Number:&quot;));
	
	        int available[] = new int[m];
	        int max[][] = new int[n][m];
	        int allocation[][] = new int[n][m];
	        int need[][] = new int[n][m];
	        String sequence = &quot;&quot;;
	
	        for (int i = 0; i &lt; m; i++) {
	            available[i] = Integer.parseInt(JOptionPane.showInputDialog(&quot;Number Of Available Resource &quot; + (i) + &quot;:&quot;));
	        }
	
	        for (int i = 0; i &lt; n; i++) {
	            for (int j = 0; j &lt; m; j++) {
	                allocation[i][j] = Integer.parseInt(JOptionPane.showInputDialog(&quot;Allocation P &quot; + (i) + &quot; for R &quot; + (j) + &quot;:&quot;));
	
	            }
	        }
	        for (int i = 0; i &lt; n; i++) {
	            for (int j = 0; j &lt; m; j++) {
	
	                max[i][j] = Integer.parseInt(JOptionPane.showInputDialog(&quot;MAX P &quot; + (i) + &quot; for R &quot; + (j) + &quot;:&quot;));
	                need[i][j] = max[i][j] - allocation[i][j];
	            }
	        }
	        int work[] = available;
	        boolean finish[] = new boolean[n];
	
	        for (int i = 0; i &lt; n; i++) {
	            finish[i] = false;
	        }
	
	        boolean check = true;
	        while (check) {
	            check = false;
	            for (int i = 0; i &lt; n; i++) {
	                if (!finish[i]) {
	                    int j;
	                    for (j = 0; j &lt; m; j++) {
	                        if (need[i][j] &gt; work[j]) {
	                            break;
	                        }
	                    }
	
	                    if (j == m) {
	                        for (j = 0; j &lt; m; j++) {
	                            work[j] = work[j] + allocation[i][j];
	                        }
	                        finish[i] = true;
	                        check = true;
	                        sequence += i + &quot;, &quot;;
	                    }
	                }
	            }
	        }
	
	        int i;
	        for (i = 0; i &lt; n; i++) {
	            if (!finish[i])
	                break;
	        }
	
	        if (i == n) {
	            JOptionPane.showMessageDialog(null, &quot;SAFE And Sequence is:&quot; + sequence);
	        } else {
	            JOptionPane.showMessageDialog(null, &quot;DEAD LOCK&quot;);
	        }
	    }
	}



六：实验总结

经过几天的操作系统课程设计，我学习到了很多东西。这次课程设计的内容是银行家算法，我用的编程工具是Linux系统下的IntelliJ IDEA13，语言使用的是JAVA8语言，目的是模拟实现处理机避免死锁；通过模拟实现算法，我更进一步地学习了JAVA语言，这使我的编程能力得到了提高。当然最重要的是我更深地理解了对于死锁的避免，死锁是会影响并发执行的，是操作系统最需要解决得问题。解决死锁，我们要检测一个安全状态，虽然并非所有的不安全状态都会产生死锁状态，但系统进入不安全状态时，便可能进而进入死锁状态后，当系统在进行资源管理时，如果对进城申请的资源分配不当，可能会使系统进入死锁状态，因而后面到来的进程也无法顺利执行。银行家算法中，要对当前申请资源的进程申请资源的数目进行判断，如果可以试分配，则试求出一个安全序列，如果可以求出，则说明给这个进程分配资源后系统不会进入不安全状态，将该进程申请的资源分配给他，若求不出安全序列，则说明将资源分配给该进程后系统会进入不安全状态，所以就使该进程进入阻塞状态，等待以后可以分配资源时再执行该进程，然后系统继续服务其它进程。通过这样一个过程，可以有效避免系统进入死锁状态。反之，只要系统处于安全状态，系统便可避免进入死锁状态。因此，避免死锁的实质在于——如何使系统不进入不安全状态。。


