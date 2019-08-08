---
title: '''sql_mode=only_full_group_by''问题解决'
tags: Blog
categories:
  - MySQL
toc: false
date: 2019-06-06 15:34:35
---

问题：
```java
java.sql.SQLSyntaxErrorException: Expression #1 of 
SELECT list is not in GROUP BY clause and contains nonaggregated column 'admin.u.USER_ID' 
which is not functionally dependent on columns in GROUP BY clause; 
this is incompatible with sql_mode=only_full_group_by

```
解决办法：

```sql

SET GLOBAL sql_mode=(SELECT REPLACE(@@sql_mode,'ONLY_FULL_GROUP_BY',''));

```