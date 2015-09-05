---
layout: post
title: Sogou笔试题之求无限循环小数循环节
date: 2013-11-17 00:34
author: VERYYOUNG
comments: true
categories: [Algorithm]
---
   这道题目是搜狗笔试题第一道大题,求无限循环小数的循环节,例如1/7=0.14285714285714285,则循环节为428571
拿到这道题目第一想法就是当作普通字符串来处理,依次截取前面部分与后面部分进行比较,直到找到重复的,则重复部分为循环节
侥幸进了面试,面试官第一题就问我这题的解题思路,我把思路讲给他听,被他抓了N了Bug,最后也找不出好的解决方案,于是第一题就以失败告终...

   回来之后,用笔算了一下,发现了规律,思路如下:

      回想我们使用手算时如何发现循环节： 
	  如果除得的余数等于0，则说明整除； 
	  如果除得的余数不等于0，则将余数乘以10，继续相除； 
	  直到发现两次获得的余数相等，则找到了循环节。
	  以下程序用一个ArrayList来存储余数，当某次求得的余数在这个ArrayList里面已存在，则循环找到
   
代码如下：

	import java.util.ArrayList;
	import java.util.List;
	
	public class CircleDigitsInDivision {
	
		/**
		 * 题目：求循环节，若整除则返回NULL，否则返回循环节
		 * 解答： 回想我们使用手算时如何发现循环节： 
		 * -如果除得的余数等于0，则说明整除； 
		 * -如果除得的余数不等于0，则将余数乘以10，继续相除； 
		 * -直到发现两次获得的余数相等，则找到了循环节。
		 * 以下程序用一个ArrayList来存储余数，当某次求得的余数在这个ArrayList里面已存在，则循环找到
		 */
		public static void main(String[] args) {
			int dividend=1;
			for(int i=1;i<50;i++){
				String str = circleDigits(dividend,i);
				if(str!=null){
					System.out.println(dividend+"/"+i+"-"+str+"-"+(0.0+dividend)/i);
				}
			}
		}
	
		public static String circleDigits(int dividend, int divisor) {
			if (dividend < 0 || divisor <= 0) {
				return null;
			}
			if (dividend % divisor == 0) {
				return null;
			}
			List<Integer> quotientList = new ArrayList<Integer>();//store a/b
			List<Integer> leftList = new ArrayList<Integer>();//store a%b
			int left= dividend % divisor;
			while(!leftList.contains(left)){
				leftList.add(left);
				left*=10;
				int quotient=left / divisor;
				quotientList.add(quotient);
				left%=divisor;
				if(left==0){
					return null;
				}
			}
			int circleBegin=leftList.indexOf(left);
			quotientList = quotientList.subList(circleBegin,quotientList.size());
			StringBuilder sb=new StringBuilder();
			for(int i=0,len=quotientList.size();i<len;i++){
				sb.append(quotientList.get(i));
			}
			return sb.toString();
		}
	}
