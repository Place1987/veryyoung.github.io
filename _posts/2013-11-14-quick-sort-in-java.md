---
layout: post
title: Java版快排
date: 2013-11-14 09:29
author: VERYYOUNG
comments: true
categories: [Algorithm]
---
昨天去某土豪公司笔试,最后一题竟然是红果果的写快排,偶竟然写不出来,长期没写算法了.......
网上关于快速排序的算法原理和算法实现都比较多，不过java是实现并不多，而且部分实现很难理解，和思路有点不搭调。所以整理了这篇文章。如果有不妥之处还请建议。首先先复习一些基础。

1、算法概念。

快速排序（Quicksort）是对冒泡排序的一种改进。由C. A. R. Hoare在1962年提出。

2、算法思想。

通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

3、实现思路。

①以中间个关键字 为控制字，将 [K 1 ,K 2 ,…,K n ] 分成两个子区，使左区所有关键字小于等于 K[mid] ，右区所有关键字大于等于 K[mid] ，最后控制字居两个子区中间的适当位置。在子区内数据尚处于无序状态。 
②把左区作为一个整体，用①的步骤进行处理，右区进行相同的处理。（即递归）
③重复第①、②步，直到左区处理完毕。

4.实现代码


	
	public class QuickSort {
		public static void quickSort(int[] array, int start, int end) {
			int lower = start;
			int higher = end;
			if (end > start) {
				int mid = array[(start + end) / 2];
	
				while (lower <= higher) {
					while ((lower++ < end) && (array[lower] < mid))
						lower++;
					while ((higher-- > start) && (array[higher] > mid))
						higher--;
					if (lower <= higher) {
						swap(array, lower, higher);
						lower++;
						higher--;
					}
				}
				if(start<higher){
					quickSort(array, start, higher);
				}
				if(lower<end){
					quickSort(array, lower, end);
				}
			}
		}
	
		public static void swap(int[] array, int i, int j) {
			int temp = array[i];
			array[i] = array[j];
			array[j] = temp;
		}
		
		public static void main(String[] args) {
			int[] array = {2,3,5,1,4,6,10,5,8};
			quickSort(array, 0, array.length-1);
			for (int i : array) {
				System.out.print(i+"  ");
			}
		}
	}


