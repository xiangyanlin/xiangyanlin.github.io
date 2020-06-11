---
title: 使用eclipse导入myeclipse项目无法识别为web项目问题的解决
date: 2020-05-15 22:27:55 
categories: eclipse
tags: eclipse
---

原因eclipse默认的web目录为webcontent,而myeclipse的为webRoot,导致无法识别

<!--more-->

解决办法：
在eclipse中右击项目根路径，在弹出的对话框中，选择 Properties：![在这里插入图片描述](https://img-blog.csdnimg.cn/2020051522170285.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxODg0OTcy,size_16,color_FFFFFF,t_70)

选择 Project Facets，点击右边的“Convert to faceted form...”链接：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200515222409927.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxODg0OTcy,size_16,color_FFFFFF,t_70)
勾选 Java 和 Dynamic Web Module ：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200515222615606.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxODg0OTcy,size_16,color_FFFFFF,t_70)

点击“ Further Configuration availabe ” 的链接 ，更改 Content Directory 名字为你的 webRoot 目录名字即可