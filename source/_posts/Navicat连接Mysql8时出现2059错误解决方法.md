---
title: Navicat连接Mysql8时出现2059错误解决方法
date: 2019-02-20 16:03:18
tags: 
    - Mysql
    - Navicat
---

[Docker下安装Mysql](./Docker下安装Mysql.md)

当使用低版本的navicat链接mysql8+版本是 会出现2509的错误，原因是因为mysql8+之后使用的caching_sha2_password验证方式，而之前的mysql版本中加密规则是mysql_native_password。
解决方法就是将验证方式改为以前版本(5.7及以下)使用的验证方式mysql_native_password

windows：
```bash
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
Mac：
```bash
ALTER user 'root'@'%' IDENTIFIED BY '123456' PASSWORD EXPIRE NEVER;
ALTER user 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456’;
FLUSH PRIVILEGES;
```
'root'可以改为你自己定义的用户名，'localhost'指的是该用户开放的IP，可以是'localhost'(仅本机访问，相当于127.0.0.1)，可以是具体的'*.*.*.*'(具体某一IP)，也可以时'%'(所有IP均可访问)。
password = 你设置的密码

参考：https://blog.csdn.net/qq_35436635/article/details/80126029

<!--more-->