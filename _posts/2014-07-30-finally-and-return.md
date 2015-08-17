---
layout: post
title: finally 与 return 
date: 2014-07-30 09:20
author: VERYYOUNG
comments: true
categories: [Java]
---

这个问题在NetEase电话面试的时候被问到过，完全蒙了。。。

return 之后程序不是停止了么？？？

finally不是一定要执行么？？？

finally里面再return??What is the fuck???


写了如下的程序测试了一下，可以先别看答案，猜猜结果。

	
	public class ReturnTest {
	    public static void main(String[] args) {
	        System.out.println("=============test1==================");
	        System.out.println(test1());
	        System.out.println("===============================");
	        System.out.println("=============test1_1==================");
	        System.out.println(test1_1());
	        System.out.println("===============================");
	        System.out.println("\n============test2===================");
	        System.out.println(test2());
	        System.out.println("===============================");
	        System.out.println("\n============test2_1===================");
	        System.out.println(test2_1());
	        System.out.println("===============================");
	        System.out.println("\n============test3===================");
	        System.out.println(test3());
	        System.out.println("===============================");
	        System.out.println("\n============test3_1===================");
	        System.out.println(test3_1());
	        System.out.println("===============================");
	    }
	
	    public static String test1() {
	        String a = "in try";
	        try {
	            return a;
	        } catch (Exception e) {
	        } finally {
	            a = "in finally";
	            System.out.println("do finally");
	        }
	        return a;
	    }
	
	    public static String test1_1() {
	        String a = "in try";
	        try {
	            return a;
	        } catch (Exception e) {
	        } finally {
	            a = "in finally";
	            System.out.println("do finally");
	            return a;
	        }
	    }
	
	    public static int test2() {
	        int a = 1;
	        try {
	            return a;
	        } catch (Exception e) {
	        } finally {
	            a = 2;
	            System.out.println("do finally");
	        }
	        return a;
	    }
	
	    public static int test2_1() {
	        int a = 1;
	        try {
	            return a;
	        } catch (Exception e) {
	        } finally {
	            a = 2;
	            System.out.println("do finally");
	            return a;
	        }
	    }
	
	    public static Helper test3() {
	        Helper a = new Helper();
	        a.a = 1;
	        try {
	            return a;
	        } catch (Exception e) {
	        } finally {
	            a.a = 2;
	            System.out.println("do finally");
	        }
	        return a;
	    }
	
	    public static Helper test3_1() {
	        Helper a = new Helper();
	        a.a = 1;
	        try {
	            return a;
	        } catch (Exception e) {
	        } finally {
	            a.a = 2;
	            System.out.println("do finally");
	            return a;
	        }
	    }
	
	    static class Helper {
	        int a;
	
	        public String toString() {
	            return String.valueOf(a);
	        }
	    }
	
	}




结果如下：

	=============test1==================
	do finally
	in try
	===============================
	=============test1_1==================
	do finally
	in finally
	===============================
	
	============test2===================
	do finally
	1
	===============================
	
	============test2_1===================
	do finally
	2
	===============================
	
	============test3===================
	do finally
	2
	===============================
	
	============test3_1===================
	do finally
	2
	===============================

很好理解了。


#结论：

在try catch块里return的时候，finally也会被执行。

return 语句会把后面的值复制到一份用来返回，如果return的是基本类型的，finally里对变量的改动将不起效果，如果return 的是引用类型的，改动将可以起效果。

finally里的return语句会把try catch块里的return语句效果给覆盖掉。

看来return语句并不一定都是函数的出口，执行return时，只是把return后面的值复制了一份到返回值变量里去了。看来最佳实践是：


最好把return放到方法尾而不要在try cath 里return

不要在try catch块和finally块里都包含return

如果在try catch块里return, 则不要在finally块里操作被return的变量

