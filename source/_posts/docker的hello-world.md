---
title: docker的hello-world
date: 2021-05-04 21:36:16
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: DOCKER
tags:
	- DOCKER
---

### 安装docker引擎

列出并排序您存储库中可用的版本

```bash
$ yum list docker-ce --showduplicates | sort -r
```

然后安装指定的版本的docker-ce,写法如下

```bash
$ sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io
```

以上肯定存在报错，原因是没有没有docker的epel源

> root用户可以不加sudo，sudu的用处是获取最高权限。

### 解决方案

设置存储库

安装`yum-utils`软件包（提供`yum-config-manager` 实用程序）并设置**稳定的**存储库。

```bash
$ sudo yum install -y yum-utils

$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

可以不指定版本直接安*最新版本*的Docker Engine和容器

```bash
$ sudo yum install docker-ce docker-ce-cli containerd.io
```

启动Docker。

```bash
$ sudo systemctl start docker
```

### 一个指令安装docker

> 以上安装方法来源于官网，中规中矩。

一键安装docker的指令如下：

```bash
$ curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

### Docker的helloworld

> 实现过程：我们需要从仓库（docker hub）上抓一个helloworld镜像到，然后以这个helloworld镜像为模板，运行一个helloworld的容器实例。
>
> 1.拉镜像到本地
>
> 2.运行
>
> 3.看效果

阿里云镜像加速配置

```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://ruf8jhn0.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

运行helloworld生成helloworld容器

```bash
docker run hello-world
```

> 由于本地没有hello-world这个镜像，所以会下载一个hello-world的镜像，并在内运行。

查看容器：

```bash
$ docker images
```

[![guNai6.png](https://z3.ax1x.com/2021/05/04/guNai6.png)](https://imgtu.com/i/guNai6)