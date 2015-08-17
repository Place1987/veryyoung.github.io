---
layout: post
title: 基于Mysql bin-log恢复数据
date: 2015-01-28 22:27
author: VERYYOUNG
comments: true
categories: [Database]
---

N久之前的一个遗留sql，今天一个同事用上了

一条update语句，漏了where语句，直接全表更新，花了一张表.....


悔恨得要命啊！！！！

没办法，赶紧想办法恢复！！！

mysql如果开启了bin-log的功能，可找出bin-log，基于bin-log用mysqlbinlog命令去恢复数据。

下面是mysqlbinlog的一些介绍<a href="http://dev.mysql.com/doc/refman/5.0/en/mysqlbinlog.html" title="http://dev.mysql.com/doc/refman/5.0/en/mysqlbinlog.html" target="_blank">http://dev.mysql.com/doc/refman/5.0/en/mysqlbinlog.html</a>


大致用法如下

	mysqlbinlog --start-date="" --stop-date= "" mysql_binglog.00001 >  back.sql


执行该命令能得到start-date 到 stop-date之间的所有sql语句


得到sql语句之后，找出对应的update语句，用“#”注释掉，在本地数据库source该sql，就能得除去该update的所有sql语句执行之后最终的数据了。


导入线上数据库，完事！！！


折腾了好几个小时，以后一定不允许自己犯这种低级错误了！！！！

各位读者希望你们永远不会因为update或者delete没加where导致这种问题来回复数据，这种错误不应该发生！！



后来想了想，既然bin-log这么强大，完全可以用它来做增量备份，效果应该很不错。
得到某一区间的sql语句，然后往备份库里source该sql，做成一个定时任务。


【开启bin-log】
找到my.cnf（一般在/etc/mysql/my.cnf）在mysqld结点下新增 

	log-bin=/etc/mysql/binlog

后面的路径自由发挥
配置完毕重启mysql，bin-log就生效了。



