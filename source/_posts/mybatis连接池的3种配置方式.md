---
title: mybatis连接池的3种配置方式
date: 2019-12-11 22:40:49 
categories: mybatis
tags: mybatis
---

 mybatis连接池的3种配置方式:1,POOLED; 2,UNPOOLED 3,JNDI

<!--more-->

#### 1,POOLED
采用传统的javax. sql. DataSource规范中的连接池.一旦数据库操作完成，mybaties会将此连接返回给连接池。mybatis有实现规范。
SqlMapConfig.xml中的配置：

```
  <dataSource type="POOLED">
                <property name="driver" value=""></property>
                <property name="url" value=""></property>
                <property name="username" value=""></property>
                <property name="password" value=""></property>
            </dataSource>
```

#### 2,UNPOOLED
采用传统的获取连接的方式，同样实现Javax. sql. DataSourcel，不过没有使用池的思想。也就是说mybaties会为每一个数据库操作创建一个新的连接，使用完就关闭它。
SqlMapConfig.xml中的配置：

```
  <dataSource type="UNPOOLED">
                <property name="driver" value=""></property>
                <property name="url" value=""></property>
                <property name="username" value=""></property>
                <property name="password" value=""></property>
            </dataSource>
```

#### 3,JNDI

  是SUN公司推出的一套规范，属于JavaEE技术之一。目的是模仿windows系统中的注册表。采用服务器提供的JNDI技术实现，来获取DataSource对 象，不同的服务器所能拿到DataSource是不一样。
  mybaties会从在应用服务器向配置好的JNDI数据源DataSource获取数据库连接。一般在生产环境中使用。
  SqlMapConfig.xml中的配置：

```
<environments default= "mysql">
<environment id= "mysql">
<transact ionManager type =”JDBC">< / transact ionManager>
<dataSource type= ”JNDI" >
< property name= ”data_ source" value= "java : comp/ env/ jdbc/数据库名
</dataSource>
< /environment>
< / environments>
```

```
 
<?xml version="1.0" encoding="UTF-8"?>
<Context>

<Resource 
name="jdbc/test"                  数据源的名称
type="javax.sql.DataSource"                   数据源类型
auth="Container"                        数据源提供者
maxActive="20"                         最大活动数
maxWait="10000"                            最大等待时间
maxIdle="5"                               最大空闲数
username="root"                            用户名
password="1234"                            密码
driverClassName="com.mysql.jdbc.Driver"          驱动类
url="jdbc:mysql://localhost:3306/eesy_mybatis" 连接url字符串
/>



```
在resouce的目录下：
写一个配置文件：context.xml

```
<Resource 
name="jdbc/test"
type="javax.sql.DataSource"
auth="Container"
maxActive=
maxWait=
maxIdle=
username=
password=
driverClassName="com.mysql.jdbc.Driver"
url=
/>
</Context>
```