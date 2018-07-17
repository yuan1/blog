title: string类型转为double
date: 2017-9-22 17:8:48
tags: Java
---
  精度的问题！用基本类型的double类型进行运算可能会丢失精度。而且特别大的数又没法处理。所以如果用BigDecimal这个类问题就解决了。这个类在java.Math包下。它可以处理任意精度的数据。对于楼主出现的问题，我从新写了段代码，供楼主参考。但是主要是还得查看API！代码如下：  
import java.math.*;  
public class oopp  
{  
 public static void main(String[] args)  
 {  
 String a="1467000000";  
 double aa=Double.parseDouble(a);  
 BigDecimal beichushu=new BigDecimal(aa);  
 BigDecimal chushu=new BigDecimal(100000000);  
 BigDecimal result=beichushu.divide(chushu,new MathContext(4));//MathConText(4)表示结果精确4位！  
 boolean isTrue=String.valueOf(result).equals("14.67");  
 System.out.println("1467000000除以100000000="+result);  
 System.out.println(result+"与14.67比较的结果是"+isTrue);  
 }  
}  


 