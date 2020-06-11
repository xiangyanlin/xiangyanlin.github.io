---
title: 在学Spring Aop 发现的注意点
date: 2019-11-18 21:16:33 
categories: Spring
tags: Spring
---

## 基于xml
有两种方式可以实现：1环绕通知; 2前置通知，后置通知，最终通知，异常通知

<!--more-->

### 1环绕通知
配置环绕通知
### 2前置通知，后置通知，最终通知，异常通知



<!--配置aop-->
    <aop:config>
        <!--切入点表达式-->
        <aop:pointcut id="pr" expression="execution(作用范围)"></aop:pointcut>
        <aop:aspect id="txAdvice" ref="txManager">
            <!--前置通知-->
            <aop:before method="beginTransaction" pointcut-ref="pr"></aop:before>
            <!--后置通知-->
            <aop:after-returning method="commit" pointcut-ref="pr"></aop:after-returning>
            <!--异常通知-->
            <aop:after-throwing method="rollback" pointcut-ref="pr"></aop:after-throwing>
            <!--最终通知-->
            <aop:after method="release" pointcut-ref="pr"></aop:after>
        </aop:aspect>

    </aop:config>
### 基于注解
只能使用环绕通知
如果使用前置通知，后置通知，最终通知，异常通知会因为执行顺序问题导致错误
```
 @Around("pt1()")
    public Object aroundAdvice(ProceedingJoinPoint pjp){
        Object rtValue = null;
        try {
            //1.获取参数
            Object[] params = pjp.getParams();
            //2.开启事务
            this.beginTransaction();
            //3.执行方法
            rtValue = pjp.proceed(params);
            //4.提交事务
            this.commit();
            //返回结果
            return  rtValue;
        }catch (Throwable e){
            //5.回滚事务
            this.rollback();
            throw new RuntimeException(e);
        }finally {
            //6.释放资源
            this.release();
        }
    }
```