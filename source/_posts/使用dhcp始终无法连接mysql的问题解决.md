---
title: 使用dhcp始终无法连接mysql的问题解决
date: 2019-11-21 16:22:03
categories: mysql
tags: mysql
---

把mysql的时区加8

<!--more-->

把mysql的时区加8

```
     set global time_zone = '+8:00';
```

参考链接：
[https://blog.csdn.net/zqb765720343/article/details/80076020:](https://blog.csdn.net/zqb765720343/article/details/80076020)