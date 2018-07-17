title: HibernateUtil.save
date: 2018-6-5 12:3:19
tags: Java
---
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
 