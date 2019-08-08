---
title: HibernateUtil.save
date: 2017-10-15 12:3:19
tags: Java
---
```java
Sessionsession=null;  
try{  
    session=HibernateUtil.getSession();  
    session.beginTransaction();  
    session.save(customer);  
    session.getTransaction().commit();  
}catch(Exceptione){  
    e.printStackTrace();  
    session.getTransaction().rollback();  
}finally{  
    HibernateUtil.closeSession();  
}  
```
 