---
title: hibernate-configuration
date: 2017-2-28 9:13:7
tags: Java
---
```
<hibernate-configuration>  
    <session-factory>  
        <propertyname="connection.driver\_class">com.mysql.jdbc.Driver</property>  
        <propertyname="connection.url">jdbc:mysql://localhost:3306/hibernate-1</property>  
        <propertyname="connection.username">root</property>  
        <propertyname="connection.password">root</property>  
        <property name="dialect">org.hibernate.dialect.MySQLDialect</property>  
        <propertyname="show\_sql">true</property>  
        <propertyname="format\_sql">true</property>  
        <propertyname="hbm2ddl.auto">create</property>  
        <mappingresource="com/yuan/model/Customer.hbm.xml"/>  
    </session-factory>  
</hibernate-configuration>  
```
 