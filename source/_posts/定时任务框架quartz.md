---
title: 定时任务框架quartz
date: 2020-09-04 14:02:22
categories: 中间件
tags: quartz

---

###  定时任务框架quartz

#### 什么是 quartz ？

Quartz是OpenSymphony开源组织在Job scheduling领域又一个开源项目，完全由Java开发，可以用来执行定时任务，类似于java.util.Timer。但是相较于Timer， Quartz增加了很多功能：

- 持久性作业 - 就是保持调度定时的状态;
- 作业管理 - 对调度作业进行有效的管理;

#### Quartz的三个组成部分

- 调度器：Scheduler
- 任务：JobDetail
- 触发器：Trigger，包括SimpleTrigger和CronTrigger

