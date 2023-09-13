---
title: docker镜像的相关指令
date: 2021-05-16 17:05:17
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: DOCKER
tags:
	- DOCKER
---

## Docker镜像相关指令



### 帮助命令

1.查看版本

```bash
$ docker version
```

2.查看相关信息

```bash
$ docker info
```

3.帮助命令

```bash
$ docker --help
```

> 可以查看相关指令，提代盲目查询

### 镜像命令

关系理解

> 鲸鱼背上有集装箱
>
> 蓝色的大海里面------宿主机系统window10
>
> 鲸鱼 -----docker
>
> 集装箱-----容器实例------from-----来自我们的镜像模板

**1.docker images**

- 列出本地主机上的镜像

- options说明：

  > -a：列出本地所有的镜像（含中间映像层）
  >
  > -q：只显示镜像ID
  >
  > --digests：显示镜像的摘要信息
  >
  > --no-trunc：显示完整的镜像信息

```bash
$ docker images 【+ options】
```

**2.docker search** 某个镜像的名字

- 到dockerhub查询镜像

- options说明：

  > --no-trunc：显示完整的镜像描述；
  >
  > -s：列出收藏数不小于指定值的镜像；
  >
  > --automated：只列出auto_mate build类型的镜像；

示例：

``` bash
$ docker search tomcat
```

筛选条件：点赞数超过30

```bash
$ docker search -s 30 tomcat
```

不省略

```bash
x $ docker search -s 30 --no-trunc  tomcat
```

**3.docker pull 某个镜像的名字**

- 下载镜像
- docker pull 镜像名字[:TAG]

```bash
$ docker pull tomcat
```

等价于

```bash
$ docker pull tomcat:latest
```

可以添加参数：示例如下，为3.2的版本

```bash
$ docker pull tomcat:3.2
```

4.docker rmi 某个镜像的名字ID,加-f是强制删除。

- 删除镜像

- 删除单个

- > ```bash
  > $ docker rmi -f 镜像ID
  > ```

- 删除多个

> ```bash
> $ docker rmi -f 镜像名1：TAG 镜像名2：TAG
> ```

- 删除全部:q查询，a全部id

> ```bash
> $ docker rmi -f $(docker images -qa)
> ```

示例：

```bash
$ docker rmi -f hello-world nginx
```



