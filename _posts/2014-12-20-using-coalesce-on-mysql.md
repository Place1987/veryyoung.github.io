---
layout: post
title: Mysql Coalesce 用法
date: 2014-12-20 21:51
author: VERYYOUNG
comments: true
categories: [Database]
---
项目中mysql 查询 sum()的时候，没有匹配的项目，居然返回了null

这个npe真是莫名其妙啊！！

查询之后才知道mysql sum如果没匹配是null，不是0！！！

什么烂设计！！！

解决办法：
1.在程序里判断null

2.用coalesce

 mysql 函数coalesce()，作用是返回传入的参数中第一个非null的值
如SELECT COALESCE(NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 1);
返回1

coalesce(字段，0)  类似于if else，  如果字段为空则根据设置返回你想要的结果0



