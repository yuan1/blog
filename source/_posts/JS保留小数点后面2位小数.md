---
title: JS保留小数点后面2位小数
date: 2017-7-21 10:43:31
tags: [JS]
categories:
  - Html
---
1. 最笨的办法...我就怎么干的

```javascript
function get(){  
    var s = 22.127456 + "";  
    var str = s.substring(0,s.indexOf(".") + 3);  
    alert(str);  
} 
```
 
2. 正则表达式效果不错

```javascript
<script type="text/javascript">  
    onload = function(){  
        var a = "23.456322";  
        var aNew;  
        var re = /([0-9]+\.[0-9]{2})[0-9]*/;  
        aNew = a.replace(re,"$1");  
        alert(aNew);  
    }  
</script>  

```
3. 他就比较聪明了...

```javascript
<script>  
    var num=22.127456;  
    alert( Math.round(num*100)/100);  
</script>  
```
4. 会用新鲜东西的朋友... 但是需要 IE5.5+才支持。

```javascript
<script>  
    var num=22.127456;  
    alert( num.toFixed(2));  
</script>  
```
 