---
title: ' 阿里云centos7 运行tomcat 之后远程无法访问的解决'
date: 2020-01-17 15:05:57 
categories: 
	- linux
		- centos
tags: 阿里云服务器
---

在安装好 jdk tomcat,并且配好环境变量之后返现远程通过8080无法访问
解决方法如下：

<!--more-->

#### 1 查看在服务器本地是否能够访问

```
 curl -i http://localhost:8080
```
看一下有没有数据返回，比较慢可能需要等待几分钟时间
#### 2 添加安全组规则
在阿里云的控制添加安全组规则：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200117145259792.png)
### 3在服务器放开放防火墙firewall端口
查看8080在firewall是否开启。发现没有开启
```
 firewall-cmd --query-port=8080/tcp
no
```
添加8080

```
 firewall-cmd --add-port=8080/tcp --permanent
```
重新载入防火墙

```
firewall-cmd --reload
```
查询8080端口是否开启成功：

```
firewall-cmd --query-port=8080/tcp
```
参考文章：
[Linux下Centos7对外开放端口：](https://blog.csdn.net/realjh/article/details/82048492)
[https://blog.csdn.net/realjh/article/details/82048492](https://blog.csdn.net/realjh/article/details/82048492)