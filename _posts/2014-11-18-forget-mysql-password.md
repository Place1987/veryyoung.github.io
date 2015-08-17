---
layout: post
title: 忘记mysql密码
date: 2014-11-18 15:30
author: VERYYOUNG
comments: true
categories: [Database]
---

mysql密码忘记了，各种google，终于重置了，在这里记录下。

1.停止mysql 

	 service mysqld stop

2.修改/etc/my.cnf 

在mysqld下加入skip-grant-tables    

修改后如下 

	[mysqld]
	datadir=/var/lib/mysql
	socket=/var/lib/mysql/mysql.sock
	user=mysql
	skip-grant-tables
	# Disabling symbolic-links is recommended to prevent assorted security risks
	symbolic-links=0
	default-storage-engine=MYISAM
	###youhua
	#skip-innodb
	open_files_limit=10240
	#back_log = 100
	max_connections = 1000
	max_connect_errors = 5000
	table_cache = 100
	external-locking = FALSE
	max_allowed_packet = 16M
	sort_buffer_size = 128K
	join_buffer_size = 128K
	thread_cache_size = 100
	thread_concurrency = 8
	query_cache_size = 128M
	query_cache_limit = 2M
	"/etc/my.cnf" 47L, 1160C


3.重启mysql  
	
	service mysqld start


4.登陆mysql  

	mysql -uroot 

5.修改密码：


	mysql> update mysql.user set password=PASSWORD('password') where user='root' ;
	Query OK, 4 rows affected (0.03 sec)
	Rows matched: 4  Changed: 4  Warnings: 0
	
	mysql> FLUSH PRIVILEGES ;
	Query OK, 0 rows affected (0.01 sec)
	
	mysql>quit;


6.修改/etc/my.cnf 回之前的模样


7.重启Mysql

	serivce mysqld restart
