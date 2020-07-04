---
title: '项目启动报错'
date: 2020-05-15 22:12:39
categories: jdk
tags: jdk
---

导入一个web项目，跑起来的时候报”org.xml.sax.SAXNotRecognizedException:Feature:http://apache.org/xml/features/val”。原因：原项目用的是jdk1.7而现在用的是1.8.换成jdk1.7后成功运行