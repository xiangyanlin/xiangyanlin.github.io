---
title: mybatis表间关系，多表联查如何定义实体和返回类型
date: 2019-12-17 23:40:21
categories: mybatis
tags: mybatis
---

 mybatis表间关系，多表联查如何定义实体和返回类型

<!--more-->

### 1，一对一关系在实体加入关联实体属性(Entity1 和Entity2一对一,通过field关联)

```
public class Entity1 implements Serializable {
private Integer id;
private String field;
private String field1;
private Entity2 entity2;
(getter,setter,toString方法)
...
}
public class Entity2 implements Serializable {
private Integer id;
private String field;
private String field2;
private Entity2 entity1;
(getter,setter,toString方法)
...
}
```
 Entity1对应的mapper中加入相应的resultMap

```
    <resultMap id="entity1Entity2Map" type="Entity1 ">
        <id property="id" column="aid"></id>
        <result property="field" column="field"></result>
        <result property="field1" column="field1"></result>
        <!-- 一对一的关系映射：配置封装Entity2的内容-->
        <association property="field" column="field" javaType="Entity2">
            <id property="id" column="id"></id>
            <result column="field" property="field"></result>
            <result column="field2" property="field2"></result>
        </association>
    </resultMap>
```
2，一对多关系在实体加入关联实体属性(Entity3 和Entity4一对多,通过field关联)
```
public class Entity3 implements Serializable {
private Integer id;
private String field;
private String field3;
private List<Entity4> entity4;
(getter,setter,toString方法)
...
}
public class Entity2 implements Serializable {
private Integer id;
private String field;
private String field4;
private Entity2 entity3;
(getter,setter,toString方法)
...
}
```
 Entity3对应的mapper中加入相应的resultMap

```
    <resultMap id="entity3Entity4Map" type="Entity3 ">
        <id property="id" column="aid"></id>
        <result property="field" column="field"></result>
        <result property="field3" column="field3"></result>
        <!-- 配置Entity3对象中Entity4集合的映射 -->
        <collection property="Entity4" ofType="Entity4">
            <id column="id" property="id"></id>
            <result column="field" property="field"></result>
            <result column="field4" property="field4"></result>
        </collection>
    </resultMap>
```
### 3，多对多关系
多对多关系就类似了，实体（Entity5，Entity6关联）中都是加对方的List<T>
ReultMap关对方联集合的映射