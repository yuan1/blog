---
title: Jhipster
date: 2017-6-4 14:37:39
tags: Java
---
#### 1.简介
JHipster或者称Java Hipster，是一个应用代码产生器，能够创建Spring Boot + AngularJS的应用。开源项目地址：JHipster/Github。

JHipster使用Node.js和Yeoman产生Java应用代码，使用Maven(Gradle)运行产生的代码，产生代码有如下关键特征：

* src/main/java 目录有Spring Boot 配置类在config包中，
* JHipster使用Spring的Java 配置，没有XML配置。
* JPA实体或MongoDB文档类是在domain包. JPA实体使用缓存和auto-generated 主键配置. 如果你使用JHipster产生你的JPA实体, 可以创建1:N和N:N关系。
* 在repostiory包中是Spring Data 仓储.
* 可选，你有通常@Service-beans 在服务层. 这些服务通常是配置为事务的 安全的业务对象。
* REST 端点存在web.rest 包中, 支持Spring MVC的REST
* JHipster也产生 Liquibase 改变日志文件，用来处理数据库更新，增加一个实体将创建特定的schema更新，这将会版本化，当应用重启时可被执行。
* 集成Spring的 Test 上下文测试支持.
* JHipster 创建完整可用的Angular 前端，使用CRUD来管理你产生的实体。

#### 2.技术简介

客户端技术栈

* 单页面Web应用:
+ 响应式页面设计
+ HTML5 Boilerplate
+ Responsive Web Design with Twitter Bootstrap
+ Angular 4 or AngularJS v1.x
+ 兼容 IE11+ 和其他现代浏览器
+ 完整的国际化支持，基于 Angular Translate
+ 可选 Sass 用于 CSS 设计
+ 可选 Spring Websocket 来实现 WebSocket
  
* 强大的 Yeoman 开发工作流:
+ 使用 Yarn or Bower 可以轻松的安装 JavaScript 类库
+ 使用 Webpack or Gulp.js 构建, 优化项目, 支持 live reload
+ 使用 Karma, Headless Chrome and Protractor进行测试  
那么，如果单页面应用不能满足你的需求呢？
+ 支持 Thymeleaf 模板引擎, 用于在服务端渲染页面
  
服务端技术栈

* 一个完整的 Spring 应用:
+ Spring Boot 用于简化应用配置
+ Maven 或者 Gradle 用于构建，测试和运行应用
+ “development” 和 “production” 配置文件 (支持 Maven 和 Gradle)
+ Spring Security
+ Spring MVC REST + Jackson
+ 可选的 WebSocket 支持 – 基于 Spring Websocket
+ Spring Data JPA + Bean 验证
+ 使用 Liquibase 实现数据库自动更新
+ Elasticsearch 支持对数据库的搜索功能
+ 支持像MongoDB 这样的 document-oriented NoSQL 数据库
+ 支持像Cassandra 这样的 column-oriented NoSQL 数据库
  
* 支持生产环境：
+ Monitoring with Metrics 监控运行状态
+ 支持 ehcache (本地缓存) 或者 hazelcast (分布式缓存)
+ 可选的 HTTP session 集群 – 基于 hazelcast
+ 优化的静态资源(gzip filter, HTTP cache headers)
+ 日志管理 Logback, 可在运行时配置
+ HikariCP 连接池，用于性能优化
+ 可以将应用构建成一个标准的 WAR 文件或者一个可执行的 JAR 文件
+ Full Docker and Docker Compose support
  
#### 3.其他

需要安装的环境

* JDK8+
* Maven或者Gradle
* NodeJS
* MySQL
* GIT
* IDE
构建方式

使用yarn命令进行安装  
安装 Yeoman: yarn global add yo@1.8.5  
安装 JHipster: yarn global add generator-jhipster

 