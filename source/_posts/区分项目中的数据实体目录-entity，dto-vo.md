---
title: '区分项目中的数据实体目录 entity，dto,vo'
date: 2020-03-06 10:29:19
categories: java规范
tags: java规范
---

1、entity 里的每一个字段，与数据库相对应，
2、vo 里的每一个字段，是和你前台 html 页面相对应，
3、dto 这是用来转换从 entity 到 vo，或者从 vo 到 entity 的中间的东西 。（DTO中拥有的字段应该是entity中或者是vo中的一个子集）
[参考文章：https://www.cnblogs.com/vegetableDD/p/11732495.html](https://www.cnblogs.com/vegetableDD/p/11732495.html)