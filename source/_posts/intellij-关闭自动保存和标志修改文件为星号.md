---
title: intellij 关闭自动保存和标志修改文件为星号
tags: Blog
categories: []
toc: false
date: 2019-03-27 12:15:52
---

去掉默认保存， 
File—>settings—->System Settings—>去掉勾选synchronize files on frame or editor tab activation和去掉勾选save files on frame deactivation 
![image.png](/images/2019/03/27/fb268810-5046-11e9-90c0-4f7fca1d99be.png)
```bash
synchronize files on frame or editor tab activation，就是当前应用是intellij时，自动保存文件，比如从浏览器切换到intellij，intellij就是active，会自动保存。
save files on frame deactivation,就是从intellij切换到其他应用时，保存文件。

```
标志修改文件为星号，
File—->Settings—–>Editor—->General—->Editor tabs—->勾选 mark modified files as asterisk 
![image.png](/images/2019/03/27/9dbba010-5047-11e9-ba39-b1292a252a76.png)