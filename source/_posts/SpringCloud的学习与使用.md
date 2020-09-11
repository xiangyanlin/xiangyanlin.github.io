---
title: SpringCloud的学习与使用
date: 2020-08-23 15:17:53
categories: 微服务 - SpringCloud
tags: SpringCloud
---

### SpringCloud

Spring Cloud 是一套完整的微服务解决方案，基于 Spring Boot 框架，准确的说，它不是一个框架，而是一个大的容器，它将市面上较好的微服务框架集成进来，从而简化了开发者的代码量。

<!--more-->

#### 学习的版本说明与记录

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

#### 组件选用

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

