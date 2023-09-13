---
title: docker容器指令(下)
date: 2021-05-17 17:36:31
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: DOCKER
tags:
	- DOCKER
---

## 常用容器指令下

### 启动守护式容器

```bash
$ docker run -d 容器名
```

> 只启动不进入交互式终端

每两秒打印一次

```bash
$ docker run -d centos /bin/sh -c "while true;do echo hello zzyy;sleep 2;done"
```

### 查看容器日志

```bash
docker logs -f -t --tail 容器ID
```

> -t 是加入时间戳
>
> -f 跟随最新的日志打印
>
> ---tail 数字显示最后多少条

每两秒打印一次

```bash
$ docker run -d centos /bin/sh -c "while true;do echo hello zzyy;sleep 2;done"
```

查看日志

```bash
$ docker logs -t  容器ID
```

持续查看日志

```bash
$ docker docker logs -t -f 容器ID
```

查看最后三条

```bash
$ docker docker logs -t -f -tail 3 容器ID
```

### 查看容器内运行的进程

```bash
$ docker top 容器ID
```

### 查看容器内部的细节

```bash
$ docker inspect 容器ID
```

### 进入正在运行的容器并以命令行交互

```bash
$ docker exec -it 容器ID bashShell
```

示例：

```bash
$ docker exec -t 0e76db4c4106 ls  -l /tmp
```

> 进入容器执行了ls -ls -l  /tmp命令，直接把结果返回到宿主机，相当于没有进入容器，远程操作。

重新进入

```bash
$ docker attach 容器ID
```

> 重新进入容器，可以执行命令

等价于

```bash
$ docker exec -it 0e76db4c4106 /bin/bash
```

两者区别

> attach 
>
> 直接进入容器启动命令的终端，不会启动新的进程
>
> exec
>
> 是在容器内打开新的终端，并且苦于启动新的进程

### 从容器内拷贝文件到主机上

示例：

```bash
$ docker cp 容器ID: /tmp/yum.log /root
```

把容器里面的yum.log文件拷贝到宿主机的/root目录

