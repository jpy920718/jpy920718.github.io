---
title: Docker下安装mysql
date: 2019-02-20 11:54:20
tags: 
    - Docker
    - Mysql
    - Navicat
---
~~假设已经安装过docker~~
#### docker 查找镜像
```bash
    docker search mysql
```
#### docker 拉取镜像
```bash
    docker pull mysql // 安装最新mysql
    docker pull mysql:8.0.13 // 安装指定版本
```

#### docker 查看本地镜像列表
```bash
    docker images
```
![6fbdb6bc589bbbdd1e4cffd9d5970690.jpeg](/images/6fbdb6bc589bbbdd1e4cffd9d5970690.jpeg)

#### docker 启动mysql
<!--more-->
```bash
    docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql
```
![2cafd4485451f000b262fe788c63ba90.jpeg](/images/2cafd4485451f000b262fe788c63ba90.jpeg)

出现如上图的错误，通过错误提示，刚刚设置的容器名已存在，删除或重命名，选择删除！！！

#### docker 删除容器
1. 列出容器列表

```bash
    docker ps -a // 列出所有容器列表包括未运行的
```
![d659a4b169ae7ea93d46cc0ce015ba15.jpeg](/images/d659a4b169ae7ea93d46cc0ce015ba15.jpeg)

或者直接查看容器id
```bash
    docker ps -a -q // 列出所有容器id
```
![b885f9e3d98887cc93fcb67cfa15ebb6.jpeg](/images/b885f9e3d98887cc93fcb67cfa15ebb6.jpeg)

2. 删除
docker rm：删除一个或多少容器
docker rm [OPTIONS] CONTAINER [CONTAINER.]

    -f :通过SIGKILL信号强制删除一个运行中的容器

    -l :移除容器间的网络连接，而非容器本身

    -v :-v 删除与容器关联的卷
  
  
```bash
    docker rm -f 72d8c2388a8c
```
![a62dbeb9173d646dc467762c8c51831f.jpeg](/images/a62dbeb9173d646dc467762c8c51831f.jpeg)

在执行查看列表命令

```bash
    docker ps -a -q
```
![935497cd7a8dcdf3ad4d51ad4ba32755.jpeg](/images/935497cd7a8dcdf3ad4d51ad4ba32755.jpeg)

此时容器已被删除，再去执行启动mysql的命令

```bash
docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql
```
![ced0394304523c95ee6430bb6a2e3596.jpeg](/images/ced0394304523c95ee6430bb6a2e3596.jpeg)
启动成功

#### 进入容器
```bash
    docker exec -it mysql bash
```
![c08845d5e9744730b1ccb1aa4fea395b.png](/images/c08845d5e9744730b1ccb1aa4fea395b.png)


#### 登录mysql

```bash
mysql -u root -p
```

![fbf41abb6ac233da9ec3e02d2f2132bb.png](/images/fbf41abb6ac233da9ec3e02d2f2132bb.png)

控制台docker安装mysql和连接mysql完成。

> 如果使用navicat 连接mysql会出现客户端连接不上的问题解决方法
> 1. 降低mysql版本低于8
> 2. 查看下一遍文章可看到解决问题

