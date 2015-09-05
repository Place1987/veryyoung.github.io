---
layout: post
title: Mysql In 子查询慢
date: 2015-8-17 14:29:23
author: VERYYOUNG
comments: true
categories: [Database]
---

前几天做一个需求用到了sql in 子查询，
大概sql如下
		
	SELECT * FROM table_a WHERE id IN (SELECT id FROM table_id_list)

执行时间150m，完全没法忍受

单独执行
	
	SELECT id FROM table_id_list
秒查，只有七八行结果。


把查询结果写死在sql中

	SELECT * FROM table_a WHERE id IN (1,2,3,4,5)

依然秒查



----------

解决方案

1. 再把ID列表select一次
	
	SELECT * FROM table_a WHERE id IN (SELECT id from(SELECT id FROM table_id_list))
秒查。（至今没搞明白原因）

2. 使用join
	
	SELECT * FROM table_a JOIN (SELECT id FROM table_id_list) id_list ON table_a.id = id_list.id
   
推荐！


参考[http://stackoverflow.com/questions/5018284/mysql-in-queries-terribly-slow-with-subquery-but-fast-with-explicit-values](http://stackoverflow.com/questions/5018284/mysql-in-queries-terribly-slow-with-subquery-but-fast-with-explicit-values "http://stackoverflow.com/questions/5018284/mysql-in-queries-terribly-slow-with-subquery-but-fast-with-explicit-values")	







