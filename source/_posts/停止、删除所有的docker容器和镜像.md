---
title: 停止、删除所有的docker容器和镜像
tags: [Docker,Linux]
categories:
  - Docker
toc: false
date: 2019-08-12 16:02:31
---

#### 列出所有的容器 ID
```bash
docker ps -aq
```
#### 停止所有的容器
```bash
docker stop $(docker ps -aq)
```
#### 删除所有的容器
```bash
docker rm $(docker ps -aq)
```
#### 删除所有的镜像
```bash
docker rmi $(docker images -q)
```
#### 复制文件
```bash
docker cp mycontainer:/opt/file.txt /opt/local/
docker cp /opt/local/file.txt mycontainer:/opt/
```

####  docker1.13增加了专门清理资源(container、image、网络)的命令
```bash
docker container prune
docker image prune
docker image prune --force --all 或者 docker image prune -f -a : 删除所有不使用的镜像
docker container prune -f: 删除所有停止的容器
```