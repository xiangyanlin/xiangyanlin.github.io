---
title: Docker Compose的使用
date: 2020-07-07 10:50:16
categories: docker
tags: Docker Compose
---

####  Docker Compose

<!--more-->

##### 安装

centos安装（使用root用户或者sudo）：

从 [官方 GitHub Release](https://github.com/docker/compose/releases) 处直接下载编译好的二进制文件：

```
curl -L https://github.com/docker/compose/releases/download/1.26.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
```



给予执行权限：

```
 chmod +x /usr/local/bin/docker-compose
```



### docker-compose.yml

编写 `docker-compose.yml` 文件，这个是 Compose 使用的主模板文件。

```yaml
version: '3'

services:
  tomcat:
    restart: always
    image: tomcat
    container_name: tomcat
    ports:
     - 8080:8080

```





对于 Compose 来说，大部分命令的对象既可以是项目本身，也可以指定为项目中的服务或者容器。如果没有特别的说明，命令对象将是项目，这意味着项目中所有的服务都会受到命令影响。

执行 `docker-compose [COMMAND] --help` 或者 `docker-compose help [COMMAND]` 可以查看具体某个命令的使用格式。

`docker-compose` 命令的基本的使用格式是

```bash
docker-compose [-f=<arg>...] [options] [COMMAND] [ARGS...]
```



## [#](https://www.funtl.com/zh/docs-docker/Docker-Compose-命令说明.html#命令选项)命令选项

- `-f, --file FILE` 指定使用的 Compose 模板文件，默认为 `docker-compose.yml`，可以多次指定。
- `-p, --project-name NAME` 指定项目名称，默认将使用所在目录名称作为项目名。
- `--x-networking` 使用 Docker 的可拔插网络后端特性
- `--x-network-driver DRIVER` 指定网络后端的驱动，默认为 `bridge`
- `--verbose` 输出更多调试信息。
- `-v, --version` 打印版本并退出。



