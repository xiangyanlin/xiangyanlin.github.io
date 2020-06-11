---
title: Spring 编程式事务
date: 2019-11-21 21:55:45
categories: Spring
tags: Spring
---

Spring 编程式事务:1 配置文件bean.xml; 2在自己的业务层方法加编程式事务

<!--more-->

#### 1 配置文件bean.xml

导入相关依赖后，在配置文件bean.xml文件中配置

```

    <!-- 配置事务管理器-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <!--这里是自己配置的数据源-->
        <property name="dataSource" ref="dataSource"></property>
    </bean>

    <!--配置事务模板对象-->
    <bean id="transactionTemplate" class="org.springframework.transaction.support.TransactionTemplate">
        <property name="transactionManager" ref="transactionManager"></property>
    </bean>
```
#### 2在自己的业务层方法加编程式事务
在需要加事务的方法method中书写：
```
public void method() {
        transactionTemplate.execute(new TransactionCallback<Object>() {
            @Override
            public Object doInTransaction(TransactionStatus status) {
                ......
                自己的方法逻辑
            }
        });

    }
```