---
layout: post
title: Sogou笔试题之计算器实现
date: 2013-11-20 23:28
author: VERYYOUNG
comments: true
categories: [Algorithm]
---

	
		/**
		 * 【数据结构类】一种计算机,其有如下原子功能: 
		 * 1.赋值 
		 * 2.+1操作 ++a;a+1; 
		 * 3.循环,但是只支持按次数的循环for(变量名)(循环里面对变量的修改不影响 循环次数) 
		 * 4.只能处理0和正整数 
		 * 5.函数调用 fun(参数列表)
		 * 在这个计算机上编程实现变量的加法减法,乘法
		 **/
	    //add operation 
	    fun_add(a,b) 
	    {
			for(b)
				++a;
			return a;
		}
	    
	
	    //reduce one per time
		fun_dec(a)    
		{    
		    temp = 0;    
		    result = 0;    
		    for(a)    
		    {    
		        result = temp;  
		        ++temp;    
		    }    
		    return result;    
		}    
		
		//multiply operation 
		fun_multi(a, b) 
		{
			result = a;    
		    for(b)    
		        result = fun_dec(result);  
		}
		
	    //minus operation 
		fun_minus(a, b) 
		{
			result = 0;    
		    for(b)    
		        result = fun_add(result , a);    
		    return result;    
		}
	
	}

