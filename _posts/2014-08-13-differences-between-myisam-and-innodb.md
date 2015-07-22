---
layout: post
title: MyISAM与InnoDB对比
date: 2014-08-13 22:46
author: VERYYOUNG
comments: true
categories: [Database]
---
Mysql数据库中最常使用的两种表类型为 InnoDB和MyISAM。这两种类型各有优缺点，视具体应用而定。 

InnoDB 给 MySQL 提供了具有事务(commit)、回滚(rollback)和崩溃修复能力(crash recovery capabilities)的事务安全(transaction-safe (ACID compliant))型表。 
InnoDB 提供了行锁(locking on row level)，提供与 Oracle 类型一致的不加锁读取(non-locking read in SELECTs)。这些特性均提高了多用户并发操作的性能表现。   
在InnoDB表中不需要扩大锁定(lock escalation)，因为 InnoDB 的列锁定(row level locks)适宜非常小的空间。 
InnoDB 是 MySQL 上第一个提供外键约束(FOREIGN KEY constraints)的表引擎。 
InnoDB 的设计目标是处理大容量数据库系统，它的 CPU 利用率是其它基于磁盘的关系数据库引擎所不能比的。 
在技术上，InnoDB 是一套放在 MySQL 后台的完整数据库系统，InnoDB 在主内存中建立其专用的缓冲池用于高速缓冲数据和索引。 
InnoDB 把数据和索引存放在表空间里，可能包含多个文件，这与其它的不一样，举例来说，在 MyISAM 中，表被存放在单独的文件中。 
InnoDB 表的大小只受限于操作系统的文件大小，一般为 2 GB。 
InnoDB所有的表都保存在同一个数据文件 ibdata1 中（也可能是多个文件，或者是独立的表空间文件）, 相对来说比较不好备份，免费的方案可以是拷贝数据文件、备份 binlog，或者用 mysqldump。 



MyISAM 是MySQL5.5前的缺省存贮引擎 . 每张MyISAM 表被存放在三个文件 。frm 文件存放表格定义。 数据文件是MYD (MYData) 。 索引文件是MYI (MYIndex) 引伸。 
因为MyISAM相对简单所以在效率上要优于InnoDB..小型应用使用MyISAM是不错的选择. MyISAM表是保存成文件的形式,在跨平台的数据转移中使用MyISAM存储会省去不少的麻烦。 


以下是一些细节和具体实现的差别： 
   1.InnoDB不支持FULLTEXT类型的索引，但可基于sphinx实现。 
   2.InnoDB 中不保存表的具体行数，也就是说，执行select count(*) from table时，InnoDB要扫描一遍整个表来计算有多少行，但是MyISAM只要简单的读出保存好的行数即可。注意的是，当count(*)语句包含 where条件时，两种表的操作是一样的。 
   3.对于AUTO_INCREMENT类型的字段，InnoDB中必须包含只有该字段的索引，但是在MyISAM表中，可以和其他字段一起建立联合索 引。 
   4.DELETE FROM table时，InnoDB不会重新建立表，而是一行一行的删除。 
   5.LOAD TABLE FROM MASTER操作对InnoDB是不起作用的，解决方法是首先把InnoDB表改成MyISAM表，导入数据后再改成InnoDB表，但是对于使用的额外 的InnoDB特性（例如外键）的表不适用。 
   MyISAM类型的二进制数据文件可以在不同操作系统中迁移。 
   另外，InnoDB表的行锁也不是绝对的，假如在执行一个SQL语句时MySQL不能确定要扫描的范围，InnoDB表同样会锁全表，例如update table set num=1 where name like “%aaa%” 再另外，使用两种的选择： 
    如果你的数据执行大量的INSERT或UPDATE，出于性能方面的考虑，应该使用InnoDB表。 
    如果执行大量的 SELECT，MyISAM是更好的选择。 
    若需要使用事务处理，但是原来的数据表使用的是myisam，就需要改为bdb或者innodb，这样基于 myisam的程序，将类型改为innodb后，其程序不用改动…… 综上所述，任何一种表都不是万能的，只有恰当的针对业务类型来选择合适的表类型，才能最大的发挥MySQL的性能优势。  
     MyISAM类型的表强调的是性能，其执行数度比InnoDB类型更快，但是不提供事务支持，而InnoDB提供事务支持以及外部键等高级数据库功能。这样就可以根据数据表不同的用处是用不同的存储类型。 
    另外，MyISAM类型的二进制数据文件可以在不同操作系统中迁移。也就是可以直接从Windows系统拷贝到linux系统中使用。 
