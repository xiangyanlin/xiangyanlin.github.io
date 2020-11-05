---
title: 消息队列和rabbitMQ
date: 2020-08-02 13:50:19
categories: 消息队列	
tags: rabbitMQ

---

#### 消息中间件概述

消息队列已经逐渐成为企业IT系统内部通信的核心手段。它具有低耦合、可靠投递、广播、流量控制、最终一致性等一系列功能，成为异步RPC的主要手段之一。当今市面上有很多主流的消息中间件，如老牌的ActiveMQ、RabbitMQ，炙手可热的Kafka，阿里巴巴自主开发RocketMQ等。

<!--more-->

##### 协议

MQ是消息通信的模型。实现MQ的大致有两种主流方式:AMQP,JMS.

AMQP:AMQP（Advanced Message Queuing Protocol，高级消息队列协议）是一个进程间传递**异步消息**的**网络协议**。

**JMS**:　JMS即[Java消息服务](http://baike.baidu.com/view/3292569.htm)（Java Message Service）应用程序接口，是一个[Java平台](http://baike.baidu.com/view/209634.htm)中关于面向[消息中间件](http://baike.baidu.com/view/3118541.htm)（MOM）的[API](http://baike.baidu.com/subview/16068/5889234.htm)，用于在两个应用程序之间，或[分布式系统](http://baike.baidu.com/view/991489.htm)中发送消息，进行异步通信。Java消息服务是一个与具体平台无关的API，绝大多数MOM提供商都对JMS提供支持（百度百科给出的概述）。我们可以简单的理解：两个应用程序之间需要进行通信，我们使用一个JMS服务，进行中间的转发，通过JMS 的使用，我们可以解除两个程序之间的耦合。（如ActiveMQ,RocketMQ）

**RbbitMQ**：基于AMQP协议。使用erlang语言开发，稳定性好。它是应用程序之间的通信方法，消息队列在分布式系统中应用十分广泛。（生产者，消费者）

**RbbitMQ的六种工作模式**

简单模式，work模式，Publish/Subscribe发布与订阅模式，Routing路由模式，Topics主题模式，RPC远程调用模式。



#### 消息自动确认机制

默认情况下，生产者生产的消息平均分配给每一个消费者。



##### 2work模式

平均的吧消息分发给每一个消费者

某个消费者宕机的情况下：

关闭自动确认。在业务代码执行完成时手动确认。



##### 3Publish/Subscribe发布与订阅模式

广播。通过指定交换机发给 所有与此交换机绑定的队列（交换机类型fanout）



##### 4Routing路由模式

通过指定交换机 发给所有与此交换机下指定的路由键绑定的队列(交换机类型direct)



##### 5Topics主题模式(动态路由)

通过指定交换机 发给所有与此交换机下指定的(路由键通配符，如a.*)绑定的队列(交换机类型topic)



