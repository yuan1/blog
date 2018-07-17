title: jQuery取得select选中的值
date: 2017-11-14 5:31:45
tags: JavaScript
---
  记录一下。

 本来以为jQuery(“#select1”).val();是取得选中的值，

 那么jQuery(“#select1”).text();就是取得的文本。

 这是不正确的，正确做法是：

 jQuery("#select1 option:selected").text();  
  
functioncheckNxsSel(){  
 varnxsSel=jQuery("#nxslxSel option:selected").text();;  
 if(nxsSel !=""){  
 $.messager.alert(&apos;提示&apos;, nxsSel,&apos;info&apos;);  
 $("#nxslxTr").css("display"," table-row ");  
 }else{  
 $.messager.alert(&apos;提示&apos;, nxsSel,&apos;info&apos;);  
 $("#nxslxTr").css("display","none");  
 }  
   
}  
 table-row  
此元素会作为一个表格行显示（类似 ）。

 