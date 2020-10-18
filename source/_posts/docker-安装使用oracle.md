---
title: docker 安装使用oracle
date: 2020-10-18 16:27:54
categories: Oracle
tags: docker,oracle
---

####  docker 安装使用oracle

在liunux docker上安装oracle-11g数据库。安装使用非常方便。以下是在centos7上的安装过程

<!--more-->

1拉取镜像

```
docker pull registry.cn-hangzhou.aliyuncs.com/helowin/oracle_11g
```

2启动容器

```
#建立映射目录
mkdir -p -m 755 /Users/lin/Projects/data/oracle_home/oracle_data/{app,dpdump,oraInventory}
#启动
docker run -d -p 1521:1521 --name oracle_11g   -v  /Users/lin/Projects/data/oracle_home/oracle_data/app:/opt/oracle/app     -v  /Users/lin/Projects/data/oracle_home/oracle_data/dpdump:/opt/oracle/dpdump  -v  /Users/lin/Projects/data/oracle_home/oracle_data/oraInventory:/opt/oracle/oraInventory   registry.cn-hangzhou.aliyuncs.com/helowin/oracle_11g
```

3进入容器。设置环境变量

```
#进入容器
docker exec -it oracle_11g bash
#切换root用户
su root
Password: (初始密码：helowin)
#配置环境变量
vi /etc/profile 
  #添加环境变量，加在文件末尾
  export ORACLE_HOME=/home/oracle/app/oracle/product/11.2.0/dbhome_2
  export ORACLE_SID=helowin
  export PATH=$ORACLE_HOME/bin:$PATH
#加载配置文件
source /etc/profile
```

4使用sqlplus连接oracle

```
#建立软连接
ln -sf $ORACLE_HOME/bin/sqlplus /usr/bin
#连接
sqlplus /nolog
conn / as sysdba
#启动服务
sql> startup

```

5设置用户权限

```
#修改system用户账号；
alter user system identified by system;
#修改sys用户账号；
alter user sys identified by system;
#创建内部管理员账号，创建一个用户名为oracle_test的用户，密码为 123456
create user oracle_test identified by 123456;
#将dba权限授权给内部管理员账号；
grant connect,resource,dba to oracle_test;
#修改密码规则策略为密码永不过期；
ALTER PROFILE DEFAULT LIMIT PASSWORD_LIFE_TIME UNLIMITED;
#修改数据库最大连接数据；
alter system set processes=1000 scope=spfile;
修改以上信息后，需要重新启动数据库；
#关闭数据库
shutdown immediate;
#启动
startup;
```

5开放安全组规则和防火墙，使用连接工具连接（Navicat Premium 12连接需要自己给工具下载一个最新的包oci.dill）

服务名和sid都是helowin

