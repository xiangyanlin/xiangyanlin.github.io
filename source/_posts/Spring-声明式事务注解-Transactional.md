---
title: Spring 声明式事务注解@Transactional
date: 2019-11-21 15:30:59 
categories: Spring
tags: Spring
---

 Spring 声明式事务注解@Transactional使用的两种方式：1 结合xml配置使用； 2纯注解使用

<!--more-->

## 1 结合xml配置使用

#### xml配置文件中加入

```
    <!-- 配置事务管理器 -->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <!--自己配置的dataSource-->
        <property name="dataSource" ref="dataSource"></property>
    </bean>

    <!-- 开启spring对注解事务的支持-->
    <tx:annotation-driven transaction-manager="transactionManager"></tx:annotation-driven>
```
##### 在serivce层或者serice层的方法加@Transactional注解
参数：
propagation：事务传播行为
timeout：事务超时设置
isolation：事务隔离级别


## 2 纯注解使用
### 事务管理器配置类

```
/**
 * 和事务相关的配置类
 */
public class TransactionConfig {

    /**
     * 用于创建事务管理器对象
     * @param dataSource
     * @return
     */
    @Bean(name="transactionManager")
    public PlatformTransactionManager createTransactionManager(DataSource dataSource){
        return new DataSourceTransactionManager(dataSource);
    }
}
```
##### service中的配置和1一样