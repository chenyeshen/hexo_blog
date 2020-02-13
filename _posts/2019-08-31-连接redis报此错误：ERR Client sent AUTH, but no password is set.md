---
layout:     post
title:      连接redis报此错误：ERR Client sent AUTH, but no password is set
subtitle:   学习笔记
date:       2019-09-01
author:     chenyeshen
header-img: img/img9.jpg
catalog: true
tags:
    - Redis
    - 报错笔记
   
---

```
127.0.0.1:6379> auth 123456
ERR Client sent AUTH, but no password is set
```

设置其密码

```
redis 127.0.0.1:6379> CONFIG SET requirepass "123456"
OK
redis 127.0.0.1:6379> AUTH 123456
Ok
```


设置下这个配置密码就好了

最简单的启动方式是直接双击redis-server.exe 如果要设置密码，首先打开配置文件，要注意的是这两个都是配置文件，记住你改的是哪一个，不放心的可以两个都改。 然后找到#requirepass foobared，改成requirepass 密码。 接着按住shift后右键进入该目录下的命令行，执行redis-server.exe 你改的配置的文件名。 这样启动会有个问题，一旦你把命令行窗口关闭 redis也会被关闭，所以我们需要把它注册成服务

```
命令是： redis-server.exe --service-install redis.windows.conf
```

　成功后就能在服务管理中找到

如果安装后默认已经添加了这个服务项，那就不能再次添加，你可以右键查看属性 　　 可以看到使用的是哪个配置文件，然后按照需要修改就可以了。

最后提醒一下，修改过配置，记得一定要重启redis！