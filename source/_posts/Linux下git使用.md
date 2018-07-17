title: Linux下git使用
date: 2017-8-8 4:15:33
tags: Linux
---
   * 在github上创建项目

 
 * 使用git clone https://github.com/xxxxxxx/xxxxx.git克隆到本地

 
 * 编辑项目

 
 * git add .（将改动添加到暂存区）

 
 * git commit -m "提交说明"

 
 * git push origin master 将本地更改推送到远程master分支。

 
 * 这样你就完成了向远程仓库的推送

 
 * 如果在github的remote上已经有了文件，会出现错误。此时应当先pull一下，即：git pull origin master然后再进行：git push origin master

 
  