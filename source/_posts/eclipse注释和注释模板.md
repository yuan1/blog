title: eclipse注释和注释模板
date: 2017-7-15 8:46:4
tags: 工具
---
  注释   
注释类型  
// 单行注释  
String type = "单行注释";  


 /*   
 * 多行注释  
 */  
String type = "多行注释";  
 /**  
 * 文档注释  
 */publicclass Dummy{}  
 快捷键

 添加/取消单行注释： Ctrl+/ 

 添加类的文档注释： Ctrl+Shift+j 

 注释模板 

  作用：定义文件、类和方法等默认的注释格式，减少手工输入的工作量。

  设置注释模板的入口：点击 Window->Preference->Java->Code Style->Code Template ，然后展开 Comments节点 。

  Comments节点 下的元素介绍：

  2. File节点（文件注释标签）
  /**   
* @Title: ${file\_name}   
* @Package ${package\_name}   
* @Description: ${todo}(用一句话描述该文件做什么)   
* @author fsjohnhuang  
* @date ${date} ${time}   
* @version V1.0   
*/  
  2. Types节点（类注释标签）
  /**   
* @ClassName: ${type\_name}   
* @Description: ${todo}(这里用一句话描述这个类的作用)   
* @author fsjohnhuang  
* @date ${date} ${time}   
*   
* ${tags}   
*/  
  2. Fields节点（字段注释标签）
  /**   
* @Fields ${field} : ${todo}(用一句话描述这个变量表示什么)   
*/  
  2. Constructor节点（构造函数注释标签）
  /**   
* <p>Title: </p>   
* <p>Description: </p>   
* ${tags}   
*/  
  2. Method节点（方法注释标签）
  /**   
* @Title: ${enclosing\_method}   
* @Description: ${todo}(这里用一句话描述这个方法的作用)   
* @param ${tags} 参数说明   
* @return ${return\_type} 返回类型   
* @throws   
*/  
  2. Overriding Methods节点（覆盖方法注释标签）
  /*  
* Title: ${enclosing\_method}  
*Description:   
* ${tags}   
* ${see\_to\_overridden}   
*/  
  2. Delegate Methods节点（代理方法注释标签）
  /**   
* ${tags}   
* ${see\_to\_target}   
*/  
  2. getter节点（getter方法注释标签）
  /**   
* @return ${bare\_field\_name}   
*/  
  2. setter节点（setter方法注释标签）
  /**   
* @param ${param} 要设置的 ${bare\_field\_name}   
*/  
 导入、导出注释模板

 在 Window->Preference->Java->Code Style->Code Template 下可导入导出注释模板。

 