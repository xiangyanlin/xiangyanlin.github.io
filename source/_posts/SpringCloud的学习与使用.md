---
title: SpringCloud的学习与使用
date: 2020-08-23 15:17:53
categories: 微服务 - SpringCloud
tags: SpringCloud
---

### SpringCloud

Spring Cloud 是一套完整的微服务解决方案，基于 Spring Boot 框架，准确的说，它不是一个框架，而是一个大的容器，它将市面上较好的微服务框架集成进来，从而简化了开发者的代码量。

<!--more-->

#### 项目构建

##### 学习的版本说明与记录

springBoot2.x版和springcloud H版

springcloud与springboot版本对应：
https://start.spring.io/actuator/info

```json
"spring-cloud": {
      "Finchley.M2": "Spring Boot >=2.0.0.M3 and <2.0.0.M5",
      "Finchley.M3": "Spring Boot >=2.0.0.M5 and <=2.0.0.M5",
      "Finchley.M4": "Spring Boot >=2.0.0.M6 and <=2.0.0.M6",
      "Finchley.M5": "Spring Boot >=2.0.0.M7 and <=2.0.0.M7",
      "Finchley.M6": "Spring Boot >=2.0.0.RC1 and <=2.0.0.RC1",
      "Finchley.M7": "Spring Boot >=2.0.0.RC2 and <=2.0.0.RC2",
      "Finchley.M9": "Spring Boot >=2.0.0.RELEASE and <=2.0.0.RELEASE",
      "Finchley.RC1": "Spring Boot >=2.0.1.RELEASE and <2.0.2.RELEASE",
      "Finchley.RC2": "Spring Boot >=2.0.2.RELEASE and <2.0.3.RELEASE",
      "Finchley.SR4": "Spring Boot >=2.0.3.RELEASE and <2.0.999.BUILD-SNAPSHOT",
      "Finchley.BUILD-SNAPSHOT": "Spring Boot >=2.0.999.BUILD-SNAPSHOT and <2.1.0.M3",
      "Greenwich.M1": "Spring Boot >=2.1.0.M3 and <2.1.0.RELEASE",
      "Greenwich.SR6": "Spring Boot >=2.1.0.RELEASE and <2.1.17.BUILD-SNAPSHOT",
      "Greenwich.BUILD-SNAPSHOT": "Spring Boot >=2.1.17.BUILD-SNAPSHOT and <2.2.0.M4",
      "Hoxton.SR7": "Spring Boot >=2.2.0.M4 and <2.3.4.BUILD-SNAPSHOT",
      "Hoxton.BUILD-SNAPSHOT": "Spring Boot >=2.3.4.BUILD-SNAPSHOT and <2.4.0.M1",
      "2020.0.0-SNAPSHOT": "Spring Boot >=2.4.0.M1"
    },
    "spring-cloud-alibaba": {
      "2.2.1.RELEASE": "Spring Boot >=2.2.0.RELEASE and <2.3.0.M1"
    },
    "spring-cloud-services": {
      "2.0.3.RELEASE": "Spring Boot >=2.0.0.RELEASE and <2.1.0.RELEASE",
      "2.1.7.RELEASE": "Spring Boot >=2.1.0.RELEASE and <2.2.0.RELEASE",
      "2.2.3.RELEASE": "Spring Boot >=2.2.0.RELEASE and <2.3.0.M1"
    },
```

spring cloud:Hoxton.SR1

springboot:2.2.2RELEASE

spring cloud alibaba 2.1.0RELEASE



##### 组件选用

服务于注册中心：

Eureka(停更)  ZooKeeper 	Consul   Nacos(主要使用)

服务调用：

Ribbon（维护） LoadBalancer

服务调用2：

Feign(停更)  OpenFeign

服务熔断与降级：Hystrix(停更)  resilience4j  sentienal(alibaba 国内主要使用)

服务网关：

Zuul(停更)   gateWay(主要使用)

服务配置：

config（停更） Nacos

服务总线：Nacos



##### 微服务模块的建立

1建module

2改pom

3写yml

4主启动

5业务类



##### 服务与注册中心

###### Eureka

​	Spring Cloud封装了Netflix公司开发的Eureka模块来实现服务治理

​	在传统的rpc远程调用框架中，管理每个服务与服务之间依赖关系比较复杂，管理比较复杂，所以需要使用服务治理，管理服务于服务之间依赖关系，可以实现服务调用、负载均衡、容错等，实现服务发现与注册。

  Eureka包含两个组件:Eureka Server和Eureka Client。 Eureka 采用cs结构Eureka Server维持心跳连接

  服务注册:将服务信息注册进注册中心

  服务发现:从注册中心上获取服务信息

   实质:存key服务命取value调用地址

![image-20201018205756145](E:\code\myBlog\source\_posts\SpringCloud的学习与使用\image-20201018205756145.png)

1先启动eureka注册中心
2启动服务提供者payment支付服务
3支付服务启动后会把自身信息(k服务地址以别名方主
册进eureka)
4消费者order服务在需要调用接口时，使用服务别名去注册
中心获取实际的RPC远程调用地址
5消费者获是调用地址后，底层实际是利用HttpClient支术



设计思想

分布式CAP理论里面的AP





###### Zookeeper

###### Consul

###### Nacos











##### 一些小知识点

pom:<dependencyManagement></dependencyManagement>

```
-- 子模块继承之后，提供作用：锁定版本+子modlue不用写groupId和version 
```



idea热部署： ctrl+f9重启服务
健康路径：/actuator/health