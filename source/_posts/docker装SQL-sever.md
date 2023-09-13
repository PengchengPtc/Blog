---
title: docker装SQL sever
date: 2021-06-14 16:29:29
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: DOCKER
tags:
	- DOCKER
---

### 安装环境

> centos7，docker

### 安装指令

```shell
docker run -itd --name sql1 \
    -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=msserver@123456' \
   -p 1433:1433 -m 2000M --memory 2000M \
   -d microsoft/mssql-server-linux:latest
# 登录名 sa  密码 msserver@123456
```

> 注：多次尝试容器并不能跑起来，查明原因才知道是虚拟机内存开小了。

```bash
$ docker logs sql1
```

[![2715OH.png](https://z3.ax1x.com/2021/06/14/2715OH.png)](https://imgtu.com/i/2715OH)

查看发现log，才发现内存开小了，开4g就好了。

<img src="https://sugon666.oss-cn-hangzhou.aliyuncs.com/typora-user-images/image-20210613145508763.png" alt="image-20210613145508763" style="zoom:33%;" />

> 在这里不建议用navicat连接，因为运行SQL sever的sql文件无法显示表格。

### 用ssms连接

[![273GcD.png](https://z3.ax1x.com/2021/06/14/273GcD.png)](https://imgtu.com/i/273GcD)

