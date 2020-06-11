---
title: 解决程序中执行插入语句，mysql数据库表插入的中文变成问号的问题
date: 2019-12-08 13:50:04
categories: mysql
tags: mysql
---

解决程序中执行插入语句，mysql数据库表插入的中文变成问号的问题

<!--more-->

执行保存操作，执行插入语句
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191208134343121.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxODg0OTcy,size_16,color_FFFFFF,t_70)
发现插入的数据，中文在数据库中变成了问号
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191208134506604.png)
在数据库中执行以下插入语句：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191208134633703.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxODg0OTcy,size_16,color_FFFFFF,t_70)
发现没问题：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191208134717513.png)
于是检查一下自己的连接配置，发现url中没有加utf-8，于是加上：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191208134847707.png)
再次执行程序保存操作，发现问题解决：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191208134937709.png)