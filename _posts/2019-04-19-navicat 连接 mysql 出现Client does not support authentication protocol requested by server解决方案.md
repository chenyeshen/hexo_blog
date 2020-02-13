---
layout:     post
title:      navicat 连接 mysql 出现Client does not support authentication protocol requested by server解决方案
subtitle:   学习笔记
date:       2019-04-19
author:     chenyeshen
header-img: img/img23.jpg
catalog: true
tags:
    - 数据库
    - mysql
    - navicat
---

在 window server 2012 服务器上安装navicat连接不上mysql

![img](https://chenyeshen.oss-cn-shenzhen.aliyuncs.com/oneblog/article/20190720013413030.png)

输入以下文本执行解决

```
USE mysql;

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456'; 

FLUSH PRIVILEGES;
```

 
