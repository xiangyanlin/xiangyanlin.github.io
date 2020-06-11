---
title: mybatis 延迟加载和立即加载的实现
date: 2020-01-08 22:06:49 
categories: mybatis
tags: mybatis
---

mybatis 延迟加载和立即加载的实现

<!--more-->

 延迟加载：   就是在需要用到数据时才进行加载，不需要用到数据时就不加载数据。延迟加载也称懒加载.
 好处：先从单表查询，需要时再从关联表去关联查询，大大提高数据库性能，因为查询单表要比关联查询多张表速 度要快。  
 坏处：   因为只有当需要用到数据时，才会进行数据库查询，这样在大批量数据查询时，因为查询工作也要消耗 时间，所以可能造成用户等待时间变长，造成用户体验下降
 在我们使用多表查询时（一对一，一对多或者多对多），mybatis默认使用立即加载。如果我们想使用延迟加载需要做两件事

 ### 1设置多表查询返回的resultMap


```
    <resultMap id="entity1tEntity2" type="entity1">
        <id property="entity1_id" column="entity1_id"></id>
        <result property="entity2_id" column="entity2_id"></result><!--关联字段-->
        <result property="file" column="file"></result>
            <!--在这里完成这个配置后只要select * from table_entity1就可以了-->
        <!-- 一对一的关系映射：配置封装entity2的内容
        select属性指定的内容：查询entity2的唯一标识：
        column属性指定的内容：entity2根据id查询时，所需要的参数的值
        -->
        <association property="entity2" column="entity2_id" javaType="entity2" select="namespce+查询语句的id"></association>
            <!--在这里完成这个配置后只要select * from table_entity1 where entity2_id=?就可以了-->
    </resultMap>

```
配置映射文件config.xml

```
<configuration>
    <settings>
        <!--开启Mybatis支持延迟加载-->
        <setting name="lazyLoadingEnabled" value="true"/>
    </settings>
</configuration>
```
官方文档：[https://mybatis.org/mybatis-3/zh/configuration.html#settings](https://mybatis.org/mybatis-3/zh/configuration.html#settings).
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200108220513576.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxODg0OTcy,size_16,color_FFFFFF,t_70)