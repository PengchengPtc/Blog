---
title: Vue项目部署
date: 2021-07-09 11:44:27
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: DOCKER
tags:
	- DOCKER
---

## Vue项目部署

### 1.创建vue项目

```bash
yarn build / npm run build
```

此时工程根目录下多出一个`dist`文件夹

> 如果将该dist目录整个传到服务器上，部署成静态资源站点就能直接访问到该项目。

接下来就来构建一个这样的静态资源站点。

### 2.构建vue应用镜像

> nginx 是一个高性能的HTTP和反向代理服务器，此处我们选用 nginx 镜像作为基础来构建我们的vue应用镜像。

### 3. 获取 nginx 镜像

```bash
docker pull nginx
```

> - `docker`镜像（Image）一个特殊的文件系统。Docker镜像是一个特殊的文件系统，除了提供容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。 镜像不包含任何动态数据，其内容在构建之后也不会被改变。
> - docker 镜像相关操作有: 搜索镜像`docker search [REPOSITORY[:TAG]]`、拉取镜像`docker pull [REPOSITORY[:TAG]]` 、查看镜像列表`docker image ls`、删除镜像：`docker image rm [REPOSITORY[:TAG]] / docker rmi [REPOSITORY[:TAG]]` 等等。
> - docker 镜像名称由REPOSITORY和TAG组成 `[REPOSITORY[:TAG]]`，TAG默认为latest

### 4.创建 nginx config配置文件

先把dist文件上传到centos本地目录，此处做演示。上传到centos本地机的root文件夹里面

在项目根目录下创建`nginx`文件夹，该文件夹下新建文件`default.conf`

```bash
server {
    listen       80;
    server_name  localhost;

    #charset koi8-r;
    access_log  /var/log/nginx/host.access.log  main;
    error_log  /var/log/nginx/error.log  error;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```

该配置文件定义了首页的指向为 `/usr/share/nginx/html/index.html`, 所以我们可以一会把构建出来的index.html文件和相关的静态资源放到`/usr/share/nginx/html`目录下。

[![RjcWOe.png](https://z3.ax1x.com/2021/07/09/RjcWOe.png)](https://imgtu.com/i/RjcWOe)

[![Rjgnt1.png](https://z3.ax1x.com/2021/07/09/Rjgnt1.png)](https://imgtu.com/i/Rjgnt1)

### 5.创建 Dockerfile 文件(在项目根目录)、

写入以下内容：前提是在dist目录下

```bash
FROM nginx
COPY / /usr/share/nginx/html/
COPY nginx/default.conf /etc/nginx/conf.d/default.conf
```

[![Rjg0c8.png](https://z3.ax1x.com/2021/07/09/Rjg0c8.png)](https://imgtu.com/i/Rjg0c8)

### 6.基于该Dockerfile构建vue应用镜像

运行命令（注意不要少了最后的 “.” ）

```bash
docker build -t vuenginxcontainer .
复制代码
```

> `-t` 是给镜像命名 `.` 是基于当前目录的Dockerfile来构建镜像

查看本地镜像，运行命令

```bash
docker images
```

[![Rj2MUs.png](https://z3.ax1x.com/2021/07/09/Rj2MUs.png)](https://imgtu.com/i/Rj2MUs)

### 7.启动 vue app 容器

> Docker 容器Container： 镜像运行时的实体。镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等 。

基于 vuenginxcontainer 镜像启动容器，运行命令：

```
docker run \
-p 3000:80 \
-d --name vueApp \
vuenginxcontainer
复制代码
```

> - `docker run` 基于镜像启动一个容器
> - `-p 3000:80` 端口映射，将宿主的3000端口映射到容器的80端口
> - `-d` 后台方式运行
> - `--name` 容器名 查看 docker 进程

```
docker ps
复制代码
```

[![Rj2bqg.png](https://z3.ax1x.com/2021/07/09/Rj2bqg.png)](https://imgtu.com/i/Rj2bqg)

可以发现名为 vueApp的容器已经运行起来。此时访问 [http://localhost:3000](https://link.juejin.cn/?target=http%3A%2F%2Flocalhost%3A3000) 或者服务器ip：3000就能访问到该vue应用:

[![RjR4w4.png](https://z3.ax1x.com/2021/07/09/RjR4w4.png)](https://imgtu.com/i/RjR4w4)

