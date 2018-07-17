title: Hibernate关系映射
date: 2018-7-9 4:37:55
tags: Java
---
  多对一单向映射 –> hibernate=-4  
 <many-to-onename="category"class="com.yuan.hibernate.Category"fetch="join">  
 <columnname="CATEGORYID"/>  
 </many-to-one>  
privateCategorycategory;  


 多对一双向映射 –> hibernate-5  
<many-to-onename="category"class="com.yuan.hibernate.Category"fetch="join">  
 <columnname="CATEGORY"/>  
</many-to-one>  


  <setname="book"table="BOOK"inverse="false"lazy="true">  
 <key>  
 <columnname="ID"/>  
 </key>  
 <one-to-manyclass="com.yuan.hibernate.Book"/>  
 </set>  
privateSet<Book>book;  
 一对一主键关系映射 –> hibernate-6  
<one-to-onename="user"class="com.yuan.model.User"></one-to-one>  
<one-to-onename="idCard"class="com.yuan.model.IdCard"></one-to-one>  
privateUseruser;  
privateIdCardidCard;  


 一对一主键外键关系映射 – > hibernate-7  
<many-to-onename="idCard"update="true"/>  
privateIdCardidCard;  


 多对多关系映射 – > hibernate-8  
<setname="students"table="STUDENT\_COURSE"inverse="false"lazy="true">  
 <key>  
 <columnname="COURSEID"/>  
 </key>  
 <many-to-manyclass="com.yuan.model.Student"column="STUDENTID"/>  
</set>  
```  


   
   
   
   
   
  
privateSetstudents;  
privateSetcourses;  
```

 