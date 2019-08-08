---
title: PrintWriter页面输出JavaScript页面跳转
date: 2017-4-17 3:59:39
tags: Java
---

```java
PrintWriter out=response.getWriter();  
out.print("<script>alert('"+returnStr+"');window.location.href='forward.jsp';</script>");  
out.flush();  
out.close(); 
``` 
 