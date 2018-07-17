title: PrintWriter页面输出JavaScript页面跳转
date: 2017-4-17 3:59:39
tags: Java
---
  PrintWriter out=response.getWriter();  
out.print("<script>alert(&apos;"+returnStr+"&apos;);window.location.href=&apos;forward.jsp&apos;;</script>");  
out.flush();  
out.close();  
 