title: MYSQL-ERROR-1862
date: 2018-12-10 8:15:1
tags: 数据库
---
  遇到错误：  
ERROR 1862 (HY000): Your password has expired. To log in you must  
change it using a client that supports expired passwords.

 原因是：  
MySQL 5.6 introduces password-expiration capability, to enable database administrators to expire account passwords and require users to reset their password. 

 所以只需重新修改下密码即可，修改方式如下：  
以root权限登录mysql：（这里我的账户是root，密码也是root）  
mysql -uroot -proot  
然后更改密码：  
SET PASSWORD = PASSWORD('root');

 OK,可以正常使用了。

 