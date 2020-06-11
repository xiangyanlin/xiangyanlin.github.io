---
title: ' mysql联合主键'
date: 2020-01-07 11:55:42 
categories: mysql
tags: mysql
---

 mysql联合主键

<!--more-->

把（列名1，列名2）设置联合主键。将其看成一个有序对。这个有序对不能重复！就是不能有两条记录列名1，列名2都是一样的。

添加语法如下：

```
 ALTER TABLE table_name ADD CONSTRAINT 别名 PRIMARY KEY(列名1，列名2)；
```