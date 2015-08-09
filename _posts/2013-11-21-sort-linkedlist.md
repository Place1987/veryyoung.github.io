---
layout: post
title: Sogou笔试题之对链表排序
date: 2013-11-21 08:41
author: VERYYOUNG
comments: true
categories: [Algorithm]
---

   【数据结构类】实现一个对链表排序的算法,C`C++可以使用std∶∶list<int>
   Java使用LinkedList<lnteger>
   要求先描述算法,然后再实现,算法效率尽可能高效。
基本思想 
快速排序（Quicksort）是对冒泡排序的一种改进。由C. A. R. Hoare在1962年提出。它的基本思想是：通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。 

算法过程 
设要排序的数组是A[0]……A[N-1]，首先任意选取一个数据（通常选用第一个数据）作为关键数据，然后将所有比它小的数都放到它前面，所有比它大的数都放到它后面，这个过程称为一趟快速排序。一趟快速排序的算法是： 
　　1）设置两个变量I、J，排序开始的时候：I=1，J=N； 
　　2）以第一个数组元素作为关键数据，赋值给X，即 X=A[1]； 
　　3）从J开始向前搜索，即由后开始向前搜索（J=J-1），找到第一个小于X的值，让该值与X交换； 
　　4）从I开始向后搜索，即由前开始向后搜索（I=I+1），找到第一个大于X的值，让该值与X交换； 
　　5）重复第3、4步，直到 I=J； 
　　例如：待排序的数组A的值分别是：（初始关键数据：X=49） 
　　A[0] 、 A[1]、 A[2]、 A[3]、 A[4]、 A[5]、 A[6]： 
　　49 38 65 97 76 13 27 
　　进行第一次交换后： 27 38 65 97 76 13 49 
　　( 按照算法的第三步从后面开始找) 
　　进行第二次交换后： 27 38 49 97 76 13 65 
　　( 按照算法的第四步从前面开始找>X的值，65>49,两者交换，此时：I=3 ) 
　　进行第三次交换后： 27 38 13 97 76 49 65 
　　( 按照算法的第五步将又一次执行算法的第三步从后开始找 
　　进行第四次交换后： 27 38 13 49 76 97 65 
　　( 按照算法的第四步从前面开始找大于X的值，97>49,两者交换，此时：J=4 ) 
　　此时再执行第三步的时候就发现I=J，从而结束一躺快速排序，那么经过一趟快速排序之后的结果是：27 38 13 49 76 97 65，即所以大于49的数全部在49的后面，所以小于49的数全部在49的前面。 
　　快速排序就是递归调用此过程——在以49为中点分割这个数据序列，分别对前面一部分和后面一部分进行类似的快速排序，从而完成全部数据序列的快速排序，最后把此数据序列变成一个有序的序列，根据这种思想对于上述数组A的快速排序的全过程如图6所示： 
　　初始状态 {49 38 65 97 76 13 27} 
　　进行一次快速排序之后划分为 {27 38 13} 49 {76 97 65} 
　　分别对前后两部分进行快速排序 {27 38 13} 经第三步和第四步交换后变成 {13 27 38} 完成排序。 
　　{76 97 65} 经第三步和第四步交换后变成 {65 76 97} 完成排序。 

代码如下：
<pre lang="java">
public class ListSort {
	public static void quickSort(LinkedList<Integer> list, int left, int right) {
		if (left > right)
			return;
		int i = left;
		int j = right;
		int temp = list.get(left);
		while (i != j) {
			while (list.get(j) >= temp && j > i)
				j--;
			if (j > i)
				list.set(i++, list.get(j));
			while (list.get(i) <= temp && j > i)
				i++;
			if (j > i)
				list.set(j--, list.get(i));
		}
		list.set(i, temp);
		quickSort(list, left, i - 1);
		quickSort(list, i + 1, right);
	}

	public static void main(String[] args) {
		LinkedList<Integer> list = new LinkedList<Integer>();
		for (int i = 0; i < 10; i++) {
			list.add((int) (Math.random() * 9));
		}

		quickSort(list, 0, list.size() - 1);

		for (Integer integer : list) {
			System.out.print(integer + "  ");
		}

	}
}
</pre>

