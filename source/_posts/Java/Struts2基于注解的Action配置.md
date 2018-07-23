---
title: Struts2基于注解的Action配置
date: 2017-7-14 20:47:22
tags: Java
---
使用注解来配置Action的最大好处就是可以实现零配置，但是事务都是有利有弊的，使用方便，维护起来就没那么方便了。
要使用注解方式，我们必须添加一个额外包：
struts2-convention-plugin-2.x.x.jar。
虽说是零配置的，但struts.xml还是少不了的，配置如下：  
```java
<?xml version="1.0" encoding="UTF-8" ?>   
<!DOCTYPE struts PUBLIC   
"-//Apache Software Foundation//DTD Struts Configuration 2.1.7//EN"   
"http://struts.apache.org/dtds/struts-2.1.7.dtd">   
<struts>   
    <!-- 请求参数的编码方式-->   
    <constant name="struts.i18n.encoding" value="UTF-8"/>   
    <!-- 指定被struts2处理的请求后缀类型。多个用逗号隔开-->   
    <constant name="struts.action.extension" value="action,do,htm"/>   
    <!-- 当struts.xml改动后，是否重新加载。默认值为false(生产环境下使用),开发阶段最好打开 -->   
    <constant name="struts.configuration.xml.reload" value="true"/>   
    <!-- 是否使用struts的开发模式。开发模式会有更多的调试信息。默认值为false(生产环境下使用),开发阶段最好打开 -->   
    <constant name="struts.devMode" value="false"/>   
    <!-- 设置浏览器是否缓存静态内容。默认值为true(生产环境下使用),开发阶段最好关闭 -->   
    <constant name="struts.serve.static.browserCache" value="false" />   
    <!-- 指定由spring负责action对象的创建  
    <constant name="struts.objectFactory" value="spring" />   
    -->   
    <!-- 是否开启动态方法调用-->   
    <constant name="struts.enable.DynamicMethodInvocation" value="false"/>   
</struts>  
```

action类的注解：

```java
package com.web.action;   
  
import org.apache.struts2.convention.annotation.Action;  
import org.apache.struts2.convention.annotation.ExceptionMapping;  
import org.apache.struts2.convention.annotation.ExceptionMappings;  
import org.apache.struts2.convention.annotation.Namespace;  
import org.apache.struts2.convention.annotation.ParentPackage;  
import org.apache.struts2.convention.annotation.Result;  
import org.apache.struts2.convention.annotation.Results;  
import com.opensymphony.xwork2.ActionSupport;  
  
/**   
* Struts2基于注解的Action配置  
*   
*/   
  
@ParentPackage("struts-default")   
@Namespace("/annotation/test")   
@Results( { @Result(name = "success", location = "/main.jsp"),   
@Result(name = "error", location = "/error.jsp") })   
@ExceptionMappings( { @ExceptionMapping(exception = "java.lange.RuntimeException", result = "error") })   
public class LoginAction extends ActionSupport {   
    private static final long serialVersionUID = 2730268055700929183L;   
    private String loginName;   
    private String password;   
       
    @Action("login") //或者写成 @Action(value = "login")   
    public String login() throws Exception {  
        if ("yjd".equals(loginName) && "yjd".equals(password)) {  
            return SUCCESS;  
        } else {  
            return ERROR;  
        }  
    }  
      
    @Action(value = "add", results = { @Result(name = "success", location = "/index.jsp") })  
    public String add() throws Exception {  
        return SUCCESS;  
    }  
      
    public String getLoginName() {  
        return loginName;  
    }  
      
    public void setLoginName(String loginName) {  
        this.loginName = loginName;  
    }  
      
    public String getPassword() {  
        return password;  
    }  
      
    public void setPassword(String password) {  
        this.password= password;  
    }  
  
}  
```

这样就完成了一个基于注解的action配置。 

总结常用的注解如下：  
Namespace：指定命名空间。  
ParentPackage：指定父包。  
Result：提供了Action结果的映射。（一个结果的映射）  
Results：“Result”注解列表  
ResultPath：指定结果页面的基路径。  
Action：指定Action的访问URL。  
Actions：“Action”注解列表。  
ExceptionMapping：指定异常映射。（映射一个声明异常）  
ExceptionMappings：一级声明异常的数组。  
InterceptorRef：拦截器引用。  
InterceptorRefs：拦截器引用组。  


 