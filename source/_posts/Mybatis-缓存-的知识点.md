---
title: Mybatis 缓存 的知识点
date: 2020-02-22 11:26:59 
categories: mybatis
tags: mybatis
---

像大多数的持久化框架一样，Mybatis 也提供了缓存策略，通过缓存策略来减少数据库的查询次数，从而提 高性能。 

<!--more-->

##### Mybatis 中缓存分为一级缓存，二级缓存。
![一级和二级缓存](https://img-blog.csdnimg.cn/20200222111725745.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxODg0OTcy,size_16,color_FFFFFF,t_70)
##### 一级缓存
一级缓存是 SqlSession 级别的缓存，只要 SqlSession 没有 flush 或 close，它就存在。 
一级缓存是 SqlSession 范围的缓存，当调用 SqlSession 的修改，添加，删除，commit()，close()等
###### 二级缓存
二级缓存是 mapper 映射级别的缓存，多个 SqlSession 去操作同一个 Mapper 映射的 sql 语句，多个 SqlSession 可以共用二级缓存，二级缓存是跨 SqlSession 的
######  二级缓存的开启与关闭 
2.2.2.1 第一步：在 SqlMapConfig.xml 文件开启二级缓存 

```
<settings> 
 <!-- 开启二级缓存的支持 --> 
  <setting name="cacheEnabled" value="true"/>
</settings> 
```

因为 cacheEnabled 的取值默认就为 true，所以这一步可以省略不配置。为 true 代表开启二级缓存；为 false 代表不开启二级缓存。 
######  第二步：配置相关的 Mapper 映射文件 
<cache>标签表示当前这个 mapper 映射将使用二级缓存，区分的标准就看 mapper 的 namespace 值。

```
 <?xml version="1.0" encoding="UTF-8"?>
	 <!DOCTYPE mapper     PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"     "http://mybatis.org/dtd/mybatis-3-mapper.dtd"> 
	<mapper namespace="com.itheima.dao.IUserDao">
  <!-- 开启二级缓存的支持 -->  
  <cache></cache> 
  </mapper> 
```

###### 第三步：配置 statement 上面的 useCache 属性 

```
<!-- 根据 id 查询 --> 
<select id="findById" resultType="user" parameterType="int" useCache="true">
  select * from user where id = #{uid} 
  </select> 
```

将 UserDao.xml 映射文件中的<select>标签中设置 useCache=”true”代表当前这个 statement 要使用 二级缓存，如果不使用二级缓存可以设置为 false。 注意：针对每次查询都需要最新的数据 sql，要设置成 useCache=false，禁用二级缓存