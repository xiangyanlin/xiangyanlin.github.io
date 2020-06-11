---
title: 'windows下升级node.js, 在cmd 运行n stable报错bash不是内部或外部命令，也不是可运行的程序 或批处理文件'
date: 2020-01-08 10:31:27 
categories: node
tags: node
---

windows下升级node.js, 在cmd 运行n stable报错bash不是内部或外部命令，也不是可运行的程序 或批处理文件。

<!--more-->

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108102152449.png)
在GitHub官网，搜索gnvm，下载
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108102414994.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxODg0OTcy,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108102504659.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxODg0OTcy,size_16,color_FFFFFF,t_70)
放在node.js的安装目录下

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108102646281.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxODg0OTcy,size_16,color_FFFFFF,t_70)
然后打开cmd命令行窗口，输入：gnvm update latest，等待更新。
当然也可以直接覆盖.
参考文章：
[https://jingyan.baidu.com/album/9158e000fc556ea2541228e2.html?picindex=1](https://jingyan.baidu.com/album/9158e000fc556ea2541228e2.html?picindex=1).