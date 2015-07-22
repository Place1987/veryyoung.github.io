---
layout: post
title: Leetcode Two Sum
date: 2014-04-29 21:53
author: VERYYOUNG
comments: true
categories: [Algorithm]
---
题目链接： <a href="http://oj.leetcode.com/problems/two-sum/" title="http://oj.leetcode.com/problems/two-sum/">http://oj.leetcode.com/problems/two-sum/</a> 
题目内容：
Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2

题目的大致意思是给定一个数组，找出数组中的两个数，使得两个数的和等于target

最直观的思想就是让数组中的数两两相加，判断和是否等于target，时间复杂度为O（n*n） 
很显然，不够快！

接下来想到的是排序，然后维护两个下标，第一个指向第一个数，第二个指向最后一个数，计算下标处两个数的和sum
如果sum==target 找到了
如果sum>target 后面的大了，所以第二个下标往前移动
如果sum<target 前面的小了，所以第一个下标往后移动
时间复杂度是O(nlgn) + O(n) = O(nlgn)

基于排序的还有一种算法：
就是找到一个数，然后在剩余数字中二分查找target减去该数的数
时间复杂度依然是O(nlgn)

前两种算法时间主要消耗在排序上了

有没有办法优化呢？答案是肯定的！
用空间换时间！
new一个map，每次扫描数组，如果map不存在该数，把target减去该数的下标放入map，即  map.put(target - numbers[i], i);
如果存在，则可查找出下标了，代码如下：

[code]
    public int[] twoSum(int[] numbers, int target) {
        int length = numbers.length;
        if (length &lt; 2) return null;
        Map&lt;Integer, Integer&gt; map = new HashMap&lt;Integer, Integer&gt;();
        int[] returnNums = new int[2];
        for (int i = 0; i &lt; length; i++) {
            if (!map.containsKey(numbers[i])) {
                map.put(target - numbers[i], i);
            } else {
                int index = map.get(numbers[i]);
                if (index &lt; i) {
                    returnNums[0] = index + 1;
                    returnNums[1] = i + 1;
                }
            }
        }
        return returnNums;
    }
[/code]
此算法空间复杂度和时间复杂度都是O(n) ，已经做到最优了！
同时还有一优点就是没打乱原来的数组（基于排序的算法都乱拉！）
