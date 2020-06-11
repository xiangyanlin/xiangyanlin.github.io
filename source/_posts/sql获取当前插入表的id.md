---
title: sql获取当前插入表的id
date: 2019-12-05 22:39:55 
categories: mysql
tags: mysql
---

 sql获取当前插入表的id

<!--more-->

sql语句：

```
select last_insert_id();
```

动态sql:

```
        <selectKey keyProperty="userId" keyColumn="id" resultType="int" order="AFTER">
            select last_insert_id();
        </selectKey>
```