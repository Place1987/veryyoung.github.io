---
layout: post
title: 从物理文件恢复 InnoDB 数据
category: [Database]
date: 2016-06-21
author: VERYYOUNG
comments: true
---

之前做了一个服务给公司在用，已经给事业部八十多人分配了账号。结果有一天，突然显示数据库连不上了。

然后赶紧处理，重启 Mysql 会一直 hung 住，到处查日志都没有，无奈之下，只能重装 Mysql。


在重装 Mysql 之前，备份了数据库的物理文件。物理文件是指数据库存放数据的那个文件夹（在 linux 下是 ```/var/lib/mysql```
, Mac 下是 ```/usr/local/var/mysql/``` ）下对应数据库名的文件夹。

重装完事之后，把物理文件夹复制过去，重启 Mysql，能看到对应的数据库了，但是在查询数据的时候，报错了：```table database.tableName not exist```。

<!-- more -->


在网上查询了下，发现 InnoDB 和 Myisam 不同！！！

Myisam 是独享表空间，直接体现在数据库文件夹下的物理文件中，而 Mysql，则是共享表空间，存储方式使用.ibdata文件，所有表共同使用一个ibdata文件。


意思是，备份物理文件夹是不够的，还得带上表空间的文件，而我在备份数据之前删除了 ```ibdata1, ib_logfile0 和 ib_logfile1```。


---- 

当时真是紧张死了，特别怕数据找不回来，如果找不回来，就得再给那八十多人重新分配账号了。。。

然后开始各种找方案，查了 N 多资料，最后找到了 [superuser](https://superuser.com) 的一个[讨论](https://superuser.com/questions/675445/mysql-innodb-lost-tables-but-files-exist)。

上面解释了 Mysql InnoDB 表结构的一些解释，并给出了解决方案。

按照步骤开始执行。

## STEP #1

确保备份了 ```.frm`` 和 ```.ibd``` 文件，这是恢复数据的根本。

## STEP #2

执行对应 table 的建表语句，确保建表语句一定得和对应文件的建表语句一样！

## STEP #3

丢弃掉表空间，执行以下语句。

```
ALTER TABLE table_name DISCARD TABLESPACE;

```

## STEP #4

导入对应的物理文件。

```
cd /var/lib/mysql/mydb
cp table_name.ibd .
chown mysql:mysql table_name.ibd

```

## STEP #5

导入表空间

```ALTER TABLE table_name IMPORT TABLESPACE; ```

我在这一步出了问题。

```
ERROR 1808 (HY000): Schema mismatch (Table has ROW_TYPE_DYNAMIC row format, .ibd file has ROW_TYPE_COMPACT row format.)

```

建表一句的 row format 和 .ibd 文件对应的表格不 match。

干掉表，在建表语句 末尾加上 ```ROW_FORMAT=compact```，重复前面的操作。


## STEP #6

```SELECT * FROM table_name```

如果能得到正确的结果，恭喜！！！数据回来了！！

数据找回来的时候，已经凌晨三点多了。。累哭😢了。

# 反思

1.  一定要定时备份数据。
2.  不要想当然，比如用 Myisam 的方式来备份 InnoDB。
3.  必要情况下开启 bin-log，多一种数据保障手段。


附录： Mysql 文理文件解释

```
MyISAM引擎的文件：
.myd 即 my data，表数据文件
.myi 即 my index，索引文件
.log 日志文件。
```
```
InnoDB引擎的文件：
采用表空间（tablespace）来管理数据，存储表数据和索引，
InnoDB数据库文件（即InnoDB文件集，ib-file set）：
ibdata1、ibdata2等：系统表空间文件，存储InnoDB系统信息和用户数据库表数据和索引，所有表共用。
.ibd文件：单表表空间文件，每个表使用一个表空间文件（file per table），存放用户数据库表数据和索引。
.frm文件: 用来保存每个数据表的元数据(meta)信息，包括表结构的定义等，
日志文件： ib_logfile1、ib_logfile2
```