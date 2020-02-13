---
layout:     post
title:      Linux怎么恢复root密码
subtitle:   学习笔记
date:       2019-10-07
author:     chenyeshen
header-img: img/mg26.jpg
catalog: true
tags:
    - Linux
    - root密码
---

# 单用户模式的密码恢复

### 1. 重启Linux系统，按下“e” 键

![](https://raw.githubusercontent.com/mukeyeshen/picos/master/img/20191007232957.png)

### 2. 继续按下“e”键，找到带有kerner字样的那一行，然后再次按下“e”键

![](https://raw.githubusercontent.com/mukeyeshen/picos/master/img/20191007233311.png)

### 3. 在quiet后面空一格然后输入single 

![](https://raw.githubusercontent.com/mukeyeshen/picos/master/img/20191007233545.png)

### 4.完成后回车（enter键） 找到root这行按下“b”键盘

![](https://raw.githubusercontent.com/mukeyeshen/picos/master/img/20191007233908.png)



### 5. 随即进入这么界面

![](https://raw.githubusercontent.com/mukeyeshen/picos/master/img/20191007234100.png)

### 6. 更改密码 输入指令  passwd  root 输入更新密码即可

![](https://raw.githubusercontent.com/mukeyeshen/picos/master/img/20191007234441.png)