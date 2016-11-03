---
layout: post
title: 异常关机引起 Mysql 损坏
category: [Database]
date: 2016-11-03
author: VERYYOUNG
comments: true
---

VPS 上部署的网页突然打不开了，服务器连 SSH 都登录不上去。

登录服务提供商的网页，才发现如下通告：

![2016110336121WechatIMG37.jpeg](http://78rd4j.com1.z0.glb.clouddn.com/2016110336121WechatIMG37.jpeg)

大意是 VPS 可能被人攻破了，利用 SMTP 在大量发生垃圾邮件，然后服务提供商直接把机器给关机了。 

开机并修改密码之后，发现网站连不上 Mysql 了，检查了一下，发现 Mysql 死掉了。


<!-- more -->

启动 Mysql， hung 住，查看 error.log。

```tail -f /var/log/mysql/error.log```


```
2016-11-02 14:07:01 11140 [Note] InnoDB: Database was not shutdown normally!
2016-11-02 14:07:01 11140 [Note] InnoDB: Starting crash recovery.
2016-11-02 14:07:01 11140 [Note] InnoDB: Reading tablespace information from the .ibd files...
2016-11-02 14:07:01 11140 [ERROR] InnoDB: Attempted to open a previously opened tablespace. Previous tablespace shadowsocks/node uses space ID: 8 at filepath: ./shadowsocks/node.ibd. Cannot open tablespace sspanel/admin which uses space ID: 8 at filepath: ./sspanel/admin.ibd
2016-11-02 14:07:01 7f6eead6c740  InnoDB: Operating system error number 2 in a file operation.
InnoDB: The error means the system cannot find the path specified.
InnoDB: If you are installing InnoDB, remember that you must create
InnoDB: directories yourself, InnoDB does not create them.
InnoDB: Error: could not open single-table tablespace file ./sspanel/admin.ibd
InnoDB: We do not continue the crash recovery, because the table may become
InnoDB: corrupt if we cannot apply the log records in the InnoDB log to it.
InnoDB: To fix the problem and start mysqld:
InnoDB: 1) If there is a permission problem in the file and mysqld cannot
InnoDB: open the file, you should modify the permissions.
InnoDB: 2) If the table is not needed, or you can restore it from a backup,
InnoDB: then you can remove the .ibd file, and InnoDB will do a normal
InnoDB: crash recovery and ignore that table.
InnoDB: 3) If the file system or the disk is broken, and you cannot remove
InnoDB: the .ibd file, you can set innodb_force_recovery > 0 in my.cnf
InnoDB: and force InnoDB to continue crash recovery here.
```

大意是表空间坏了，需要移损坏的表文件，或者修改 ```innodb_force_recovery>0``` 来启动 Mysql recovery 模式。

```vi /etc/mysql/mysql.conf.d/mysqld.cnf```

在 ```mysqld``` 节点下加入  ``` innodb_force_recovery = 0 ```

重启 Mysql，Mysql 能连上了，但是无法写入数据：```Table is read only```。
重新修改 mysqld.cnf，注释掉 innodb_force_recovery。

再重启，又挂了！！！

```
2016-11-02 14:10:39 12573 [ERROR] InnoDB: Failed to find tablespace for table '"shadowsocks"."member"' in the cache. Attempting to load the tablespace with space id 9.
```

大概意思是表空间被占了。

反正我已经备份数据库了，直接删库吧！~

```
mysql> drop database shadowsocks;
ERROR 2013 (HY000): Lost connection to MySQL server during query
```

没成功。。直接导入 sql 覆盖数据吧！结果又失败了：

```
 Tablespace for table '`shadowsocks`.`admin`' exists. Please DISCARD the tablespace before IMPORT.
```

按照提示 discard 表空间
```
ALTER TABLE admin DISCARD TABLESPACE;
```

结果：
```
Error : Unknown table `shadowsocks.admin`
Error : Table ``shadowsocks.admin`` doesn't exist
```

按照网上的提示，直接删除掉 Mysql 物理文件，然后create database，再导入数据，报错：table exists。

最后的解决方案很暴力：

create 一个 别的名字的 database，然后导入 sql 就行了。

其实 innodb 多个数据库共用表空间，如果没有其它 database 的情况，直接把全局的表空间文件 ibdata1、ib_logfile0、ib_logfile1 删除掉，
再重建 Mysql 或许是个更彻底的方案。

或者也可以参考 [从物理文件恢复 InnoDB 数据](/blog/2016/06/21/restore-innodb-data-physical.html) 来曲线重建表空间。