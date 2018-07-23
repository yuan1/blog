---
title: MySQL命令
date: 2017-5-9 7:26:52
tags: 数据库
---

注意：MySQL中每个命令后都要以分号;结尾。
```bash
* 显示数据库
mysql> show databases; 
+----------+  
| Database |  
+----------+  
| mysql |  
| test |  
+----------+  
2 rows in set (0.04 sec)  
Mysql刚安装完有两个数据库：mysql和test。mysql库非常重要，它里面有MySQL的系统信息，我们改密码和新增用户，实际上就是用这个库中的相关表进行操作。

* 显示数据库中的表
mysql> use mysql;（打开库，对每个库进行操作就要打开此库，类似于foxpro ）  
* Database changed   
mysql> show tables;
+-----------------+  
| Tables\_in\_mysql |  
+-----------------+  
| columns\_priv |  
| db |  
| func |  
| host |  
| tables\_priv |  
| user |  
+-----------------+  
6 rows in set (0.01 sec)  
* 显示数据表的结构：  
 describe 表名;
* 显示表中的记录：  
 select * from 表名;  
 例如：显示mysql库中user表中的纪录。所有能对MySQL用户操作的用户都在此表中。  
 Select * from user;
* 建库：  
 create database 库名;  
 例如：创建一个名字位aaa的库  
 mysql> create databases aaa;
* 建表： 
use 库名；   
create table 表名 (字段设定列表)；  
例如：在刚创建的aaa库中建立表name,表中有id(序号，自动增长)，xm（姓名）,xb（性别）,csny（出身年月）四个字段  
use aaa;  
mysql> create table name (id int(3) auto\_increment not null primary key, xm char(8),xb char(2),csny date);  
可以用describe命令察看刚建立的表结构。  
mysql> describe name;   
 +-------+---------+------+-----+---------+----------------+  
 | Field | Type | Null | Key | Default | Extra |  
 +-------+---------+------+-----+---------+----------------+  
 | id | int(3) | | PRI | NULL | auto\_increment |  
 | xm | char(8) | YES | | NULL | |  
 | xb | char(2) | YES | | NULL | |  
 | csny | date | YES | | NULL | |  
 +-------+---------+------+-----+---------+----------------+  
  * 增加记录  
 例如：增加几条相关纪录。
mysql> insert into name values(张三,男,1971-10-01);  
mysql> insert into name values(白云,女,1972-05-20);  
可用select命令来验证结果。   
mysql> select * from name;  
+----+------+------+------------+  
| id | xm | xb | csny |  
+----+------+------+------------+  
| 1 | 张三 | 男 | 1971-10-01 |  
| 2 | 白云 | 女 | 1972-05-20 |  
+----+------+------+------------+  
* 修改纪录  
例如：将张三的出生年月改为1971-01-10  
mysql> update name set csny='1971-01-10' where xm='张三';
* 删除纪录  
例如：删除张三的纪录。  
mysql> delete from name where xm='张三';
* 删库和删表  
drop database 库名;   
drop table 表名；  
* 增加MySQL用户
格式：grant select on 数据库.* to 用户名@登录主机 identified by "密码"  
例1、增加一个用户user\_1密码为123，让他可以在任何主机上登录，并对所有数据库有查询、插入、修改、删除的权限。首先用以root用户连入MySQL，然后键入以下命令：  
mysql> grant select,insert,update,delete on *.* to user\_1@"%" Identified by "123";
例1增加的用户是十分危险的，如果知道了user\_1的密码，那么他就可以在网上的任何一台电脑上登录你的MySQL数据库并对你的数据为所欲为了，解决办法见例2。  

例2、增加一个用户user\_2密码为123,让此用户只可以在localhost上登录，并可以对数据库aaa进行查询、插入、修改、删除的操作（localhost指本地主机，即MySQL数据库所在的那台主机），这样用户即使用知道user\_2的密码，他也无法从网上直接访问数据库，只能通过MYSQL主机来操作aaa库。  
mysql>grant select,insert,update,delete on aaa.* to user\_2@localhost identified by "123";
用新增的用户如果登录不了MySQL，在登录时用如下命令：
mysql -u user\_1 -p -h 192.168.113.50 （-h后跟的是要登录主机的ip地址）
* 备份与恢复
备份
例如：将上例创建的aaa库备份到文件back\_aaa中  
[root@test1 root]# cd /home/data/mysql  
(进入到库目录，本例库已由val/lib/mysql转到/home/data/mysql，见上述第七部分内容)  
[root@test1 mysql]# mysqldump -u root -p --opt aaa > back\_aaa
恢复
[root@test mysql]# mysql -u root -p ccc < back\_aaa
```
	 
	  
  