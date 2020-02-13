---
layout:     post
title:      如何免费激活Windows10 只需要Copy&Paste
subtitle:   学习笔记
date:       2019-09-07
author:     chenyeshen
header-img: img/mg13.jpg
catalog: true
tags:
    - 免费激活Windows10
    - 激活Windows10
---

### 在cmd 中 或者powershell输入以下是激活分别需要用的指令

-  slmgr.vbs /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX
-  slmgr.vbs /skms kms.lotro.cc
-  slmgr.vbs /ato
-  slmgr.vbs -xpr   查询到期时间


**成功了**



**如果是win10家庭版请把第一个指令换成以下这个**

```
 slmgr.vbs /ipk TX9XD-98N7V-6WMQ6-BX7FG-H8Q99
```

**win10企业版则是这个**

```
 slmgr.vbs /ipk nppr9-fwdcx-d2c8j-h872k-2yt43
```



# 牛逼！一行命令激活系统和Office

```
slmgr /skms kms.v0v.bid && slmgr /ato 
```

