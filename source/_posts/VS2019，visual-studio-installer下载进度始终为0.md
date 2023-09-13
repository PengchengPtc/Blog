---
title: VS2019，visual studio installer下载进度始终为0
date: 2021-04-11 23:52:33
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: 软件安装
tags:
	- 软件安装
---

### VS2019，visual studio installer下载进度始终为0

## 4 解决

### 4.1 在本机对域名进行IP解析

在如下路径：C:\Windows\System32\drivers\etc找到hosts文件

加入如下内容

```
23.205.239.104 aka.ms
```

注：

> 网上许多教程是改了dns就可以了，我是改了也不行，如果你也是，可以试试这个。
>
> 改dns我也说一下，分别是两个
>
> 114.114.114.114
>
> 8.8.8.8
>
> 一个是国内的，一个是谷歌的
>
> 具体可以参照https://my.oschina.net/u/4302800/blog/4733832

还有我修改的dns是阿里的

[![c058mV.png](https://z3.ax1x.com/2021/04/12/c058mV.png)](https://imgtu.com/i/c058mV)

###　产品激活

参考：https://blog.csdn.net/cai20142932/article/details/89010514

[![c0o6RH.png](https://z3.ax1x.com/2021/04/12/c0o6RH.png)](https://imgtu.com/i/c0o6RH)