---
layout: post
title: Mysql auto_increment 不连续
category: [Database]
date: 2016-05-04
author: VERYYOUNG
comments: true
---

今天在批量插入数据的时候遇到了奇怪的现象，明明 60 多行数据 id 居然到了 105，搞得我还以为是数据重复插入了呢。

Check 之后才知道，原来是自增 id 不连续。


<!-- more -->

Google 一番才知道，这是 Mysql 的优化策略。

Mysql 以前（5.1.22 前）用表锁来保持自增字段的连续性，表锁在批量插入的时候，性能会很差，很容易造成 SQL 拥堵。

后来（5.1.22 后） Mysql 采用了新的方式，会预估批量插入大概的行数，先生成 ID（可能会有多的，多了总比少了好，哈哈），然后插入的时候取这些 id，这样就能
并发批量插入了，性能棒棒哒。

好吧，这其实就是我之前遇到的 id 不连续的问题了。

------

其实之前公司做的 id 生成器，也是先生成 id 再分配，也会存在浪费，这个情有可原。

------

Mysql innodb 引擎可以设置 ```innodb_autoinc_lock_mode```.

有以下三种选项：

```
innodb_autoinc_lock_mode = 0 
innodb_autoinc_lock_mode = 1 
innodb_autoinc_lock_mode = 2 
```


```0``` 是传统模式，使用表锁。
```1``` 是默认模式，Simple inserts 模式预估行数，先生成序列，可能会存在序列浪费，Bulk inserts，继续用表锁。
```2``` 全部放弃表锁，预估行数，先生成序列，可能会存在序列浪费。

    Simple inserts：执行时可以确定行数
    Bulk inserts：执行时行数不确定，load data/insert … select/replace … insert
    Mixed-mode inserts：只有部分行使用auto_increment值，如insert … on duplicate key update
    
    
参考 [https://dev.mysql.com/doc/refman/5.7/en/innodb-auto-increment-handling.html](https://dev.mysql.com/doc/refman/5.7/en/innodb-auto-increment-handling.html)