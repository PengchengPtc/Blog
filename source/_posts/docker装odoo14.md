---
title: docker装odoo14
date: 2021-07-05 16:47:21
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: DOCKER
tags:
	- DOCKER
---

创建数据库容器服务

```bash
docker run -d -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -e POSTGRES_DB=postgres --name db1 postgres:10.0
```

输入cmd后 需要等待一部分时间，原因是此刻 正在拉取postgres的镜像[![R5ksYD.png](https://z3.ax1x.com/2021/07/05/R5ksYD.png)](https://imgtu.com/i/R5ksYD)

等待片刻会返回一串ID，这个ID为新建的postgres容器ID，同时记住：创建数据库容器服务时 有一个 -name 选项，后面跟着的是这个容器的名称（示范中写的是 db1），后面我们会用到。

接下来创建 odoo容器服务

我们创建odoo容器，注意 -p 8888:8069这个参数，8888是宿主机的端口（也就是我们ubuntu的端口，可以任意设定），8069是容器内的odoo端口，访问odoo容器的地址是 宿主机（ubuntu）的 ip:8888

```bash
docker run -v /opt/addons/:/mnt/extra-addons -p 8888:8069 --name test_odoo1 --link db1:db -t odoo:14
```

![image-20210705175739835](C:\Users\29833\AppData\Roaming\Typora\typora-user-images\image-20210705175739835.png)此刻一样会等待

等待片刻看到这样的情况就是 odoo启动了，即可访问。

为了让odoo一直运行，我们需要 快捷键control + c 退出。然后输入 docker ps -a 查看容器，并找到 odoo14对应的容器id。

然后输入 docker start 容器ID，即可让odoo容器一直运行了。

[![RI9tiQ.png](https://z3.ax1x.com/2021/07/05/RI9tiQ.png)](https://imgtu.com/i/RI9tiQ)

[![RICBpd.png](https://z3.ax1x.com/2021/07/05/RICBpd.png)](https://imgtu.com/i/RICBpd)

