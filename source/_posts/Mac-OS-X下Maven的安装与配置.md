---
title: Mac-OS-X下Maven的安装与配置
date: 2017-2-6 16:41:44
tags: [Mac,Maven]
categories:
  - Mac
---
#### 下载Maven
到Maven官网下载安装包，选择下载Binary zip archive。下载完了之后，解压到一个目录，比如Users/lmy/maven。
#### 设置Maven环境变量
打开终端，输入以下命令，编辑bash\_profile  
$ nano ~/.bash\_profile  
添加以下代码在最后，保存并退出：
```
# maven  
export M2\_HOME=/Users/lmy/maven  
export PATH=$PATH:$M2\_HOME/bin  
```

#### 输入命令使bash_profile生效
$ source ~/.bash_profile

#### 查看Maven是否安装成功
$ mvn -v  
如果输出以下信息，说明maven安装成功了
```
$ mvn -v  
Apache Maven 3.3.9 (bb52d8502b132ec0a5a3f4c09453c07478323dc5; 2015-11-11T00:41:47+08:00)  
Maven home: /Users/yerl/maven  
Java version: 1.8.0_45, vendor: Oracle Corporation  
Java home: /Library/Java/JavaVirtualMachines/jdk1.8.0_45.jdk/Contents/Home/jre  
Default locale: zh_CN, platform encoding: UTF-8  
OS name: "mac os x", version: "10.11.5", arch: "x86_64", family: "mac"
```  
 