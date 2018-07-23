---
title: Javascript通过el计算年龄
date: 2017-2-21 18:26:20
tags: Javascript
---

```javascript
<script type="text/javascript">  
    var nowdate =newDate();  
    var brithday ="${sepeList.birthDate}";  
    var age =nowdate.getFullYear() - brithday.substr(0,4);  
    document.write(age);  
</script>  
```
 