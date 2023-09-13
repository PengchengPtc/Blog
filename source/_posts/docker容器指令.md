---
title: docker容器指令（上）
date: 2021-05-17 17:35:05
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: DOCKER
tags:
	- DOCKER
---

## docker镜像相关指令

> 有镜像才能创建容器，这是根本前提(下载一个centos镜像演示)
>
> docker 里面的容器其实是一个简化版的linux环境，减去了如打印机等许多不需要的设备。
>
> docker里面跑centos

### 新建并启动容器

```bash
$ docker run [OPTIONS] IMAGE[CAMMAND][ARG...]
```

> options说明(常用)：有些事一个减号，有些是两个减号。
>
> - --name="容器新名字":为容器指定一个新名字
>
> - -d：后台运行容器，并返回容器ID，也即启动守护式容器
>
> - -i：以交互模式运行容器，通常与-t同时使用
>
> - -t: 为容器重新分配一个伪输入终端，通常与-i同时使用
>
> - -P:随机端口映射
>
> - -p：指定端口映射，为以下四种格式
>
>   > ip：hostPort：containerPort
>   >
>   > ip： containerPort
>   >
>   > hostPost:containerPort
>   >
>   > containerPort

示例：

```bash
$ docker run -it 300e315adb2f^C
```

```bash
$ docker run -it --name mycentos01 300e315adb2f^C
```

### 列出当前所有在运行的容器

```bash
$ docker ps
```

> OPTIONS说明(常用)：
>
> - -a：列出当前所有正在运行的容器+历史上运行过的
> - -l：显示最近创建的容器
> - -n：显示最近n个创建的容器
> - -q：静默模式，只显示容器编号
> - --no-trunc：不截断输出。

查看linux的所有进程

```bash
$ ps -ef
```

### 退出容器

> 两种方式：
>
> - exit 容器停止，退出
> - ctrl+P+Q  容器不停止退出

### 启动容器

```bash
$ docker start 容器ID
```

### 重启容器

```bash
$ docker restart 容器ID
```

### 停止容器

```bash
$ docker stop 容器ID
```

### 强制停止容器

```bash
$ docker kill 容器ID
```

### 删除已经停止的容器

```bash
$ docker rm 容器ID
```

### 强制删除容器

```bash
$ docker rm -f 容器ID
```



