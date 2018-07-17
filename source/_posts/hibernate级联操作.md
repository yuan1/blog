title: hibernate级联操作
date: 2017-12-18 13:30:6
tags: Java
---
  <many-to-one name="category" class="Category" cascade="save-update">  
 <!-- 映射的字段 -->  
 <column name="categoryId"/>  
</many-to-one>  
 cascade   
 none;//默认  
 save-update;  
 delete;  
 all;  
 