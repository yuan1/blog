---
title: Java中双精度double，后面的小数位设置小数位为2
date: 2017-4-23 7:25:48
tags: [Java,Double]
categories:
  - Java
---
```java
DecimalFormat dcmFmt = new DecimalFormat("0.00");  
double db = 12333.353;  
System.out.println(dcmFmt.format(db));  
```