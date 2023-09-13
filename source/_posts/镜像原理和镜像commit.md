---
title: docker镜像原理和镜像commit
date: 2021-05-17 21:47:14
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: DOCKER
tags:
     - DOCKER
---

# Docker镜像

## 镜像原理

### 什么是镜像？

> 镜像是一种轻量级的，可执行的独立软件包，用来打包软件运行环境和基于运行环境开发的软件，它包含运行某个软件所需要的所有内容，包括代码、运行时、库、环境变量和配置文件。
>
> docker镜像实质是UnionFS(联合文件系统)。

### Docker镜像加载原理

> Docker的镜像实际上由一层一层的文件系统，这种层级的文件系统UnionFS
>
> bootfs(boot file system)主要包含bootloader和kernel,bootloader主要是引导加载kernel,Linux刚启动时回加载bootf文件系统，在Docker镜像的最底层是bootfs，这一层与我们典型的Linux/Unix系统是一样的，包含boot加载器和内核。当boot加载完成之后整个内核就都在内存中，此时内存的使用权已由bootfs转交给内核，此时系统也会卸载bootfs。
>
> rootfs(root file system),在bootfs之上，包含的就是典型的Linux系统中的/dev,/proc,/bin,/etc等标准目录和文件。rootfs就是各种不同的操作系统发行版，比如Ubuntu，Centos等等。

平时我们安装的虚拟机的Centos都是好几g，为什么docker这里才200m

对于应该精简的OS，rootfs可以很小，只需要包括最基本的命令、工具和程序库就可以了，以为底层直接用Host的kernel，自己只需要提供rootfs就行了。因此可见对于不同 的linux发行版，bootf基本是一致的，rootfs会有差别，因此不同的发行版可以公用bootfs。

> Docker镜像都是只读的，当容器启动时，应该新的可写层被加载到镜像的顶部。这一层通常被称作“容器层”，“容器层”之下的都叫“镜像层”。

### 镜像分层

以tomcat为例：

[![gRTafP.png](https://z3.ax1x.com/2021/05/17/gRTafP.png)](https://imgtu.com/i/gRTafP)

## Docker镜像commit操作补充

**Docker commit**

docker commit 提交容器副本是之成为一个新的镜像。

**指令**

```bash
$ docker commit -m="提交的描述信息" -a="作者" 容器ID要创建的目标镜像名：[标签名]
```

**示例演示**

- docker hub上下载tomcat镜像到本地并成功运行

  ```bash
  $ docker run -it -p 8889:8080 tomcat
  ```

  只查看容器id

  ```bash
  $ docker run -itd -p 8889:8080 tomcat
  ```

  [![gW9eJS.png](https://z3.ax1x.com/2021/05/17/gW9eJS.png)](https://imgtu.com/i/gW9eJS)
  [参考博客解决](https://blog.csdn.net/qq_40891009/article/details/103898876)

  [![gWFGnJ.png](https://z3.ax1x.com/2021/05/17/gWFGnJ.png)](https://imgtu.com/i/gWFGnJ)

  > ls -l，详细该目录下的目录

  > -p 主机端口：docker容器端口 第一个8080是docker对外暴露的端口，第二个8080是tomcat的默认端口
  >
  > -P 随机分配端口
  >
  > i 交互
  >
  > t 终端

- 故意删除上一步镜像生产的tomcat容器文档

  操作步骤：

  [![gWkWZ9.png](https://z3.ax1x.com/2021/05/17/gWkWZ9.png)](https://imgtu.com/i/gWkWZ9)

  点击导航的document：

  [![gWkcMF.png](https://z3.ax1x.com/2021/05/17/gWkcMF.png)](https://imgtu.com/i/gWkcMF)

- 也即当前的tomcat运行实例是一个没有文档内容的容器，以它为模板commit一个没有doc的tomcat新镜像atguigu/tomcat02

  提交

  ```bash
  $ docker commit -a="ptc" -m="tomcat without docs" 1102bbfc7dea guigu/newtomcat:1.1
  ```

  [![gWEe7d.png](https://z3.ax1x.com/2021/05/17/gWEe7d.png)](https://imgtu.com/i/gWEe7d)

  run

  ```bash
  $ docker run -it -p 7777:8080 guigu/newtomcat:1.1
  ```

  ![image-20210517213720445](C:\Users\29833\AppData\Roaming\Typora\typora-user-images\image-20210517213720445.png)

- 启动我们的新镜像并和原来的对比。

> 1.启动guigu/newtomcat，它没有docs。
>
> 2.新启动原来的tomcat，它有docs。

run-d:后台式启动，没加-d是前台式启动。

```bash
$ docker run -d -p 6666:8080 guigu/newtomcat:1.1
```

[![gWZO6f.png](https://z3.ax1x.com/2021/05/17/gWZO6f.png)](https://imgtu.com/i/gWZO6f)

> 服务器输入地址启动效果是一样的。

