---
layout: post
title: Mysql数字排序
date: 2015-8-17 13:40:46
author: VERYYOUNG
comments: true
categories: [Database]
---


今天遇到一个需求，需要对计算过后的结果进行排序，结果出现了类似

	1 10 11 12 13 14 15 16 17 18 19 2 3 4 5 6 7 8 9

这样的排序结果

很显然，mysql把它当字符串去排序了。

#解决方案

1. 使用CAST把字符串转为数字再排序

		SELECT * FROM  table_name ORDER BY CAST(field_name AS UNSIGNED) 

2. 将字段*1或者+0可以将MySQL字符串字段按数值排序

		SELECT * FROM table_name ORDER BY field_name*1 desc

    或者

		SELECT * FROM table_name ORDER BY field_name+0 desc 
3. 使用MySQL绝对值函数ABS

		SELECT * FROM table_name ORDER BY ABS（field_name) desc 








