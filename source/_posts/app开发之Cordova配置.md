---
title: app开发之Cordova配置
date: 2021-11-16 20:46:07
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Quasar
tags:
	- Quasar
---

# app开发之Cordova配置

## 准备

> 首先要求有java环境。
>
> [下载地址x64](https://www.oracle.com/cn/java/technologies/javase/javase8-archive-downloads.html)
>
> 配置环境变量。
>
> [配环境变量](https://www.runoob.com/java/java-environment-setup.html)

## 配cordova

### 1.第一步是确保安装了Cordova CLI和必要的SDK

```bash
$ npm install -g cordova
```

### 2.添加Cordova Quasar模式

为了开发/构建移动APP，我们需要将Cordova模式添加到我们的Quasar项目中。 它所做的是使用Cordova CLI在`/src-cordova`文件夹中生成一个Cordova项目。 每次构建时会覆盖`/src-cordova/www`文件夹。

```bash
$ quasar mode add cordova
```

### 3. 添加平台

要切换到cordova项目，请键入：

```js
$ cd src-cordova
```

Quasar CLI按需安装目标平台。 但是，如果要手动添加平台，请键入：

```js
$ cordova platform add [android|ios]
```

要验证所有内容是否正常，请键入：

```bash
$ cordova requirements
```

## 下载Android studio

先安装，安装后，下载对应的SDK。

选择所需的SDK。 根据2019年12月的数据，Cordova需要android-28（Android 9.0-Pie），因此请确保将其包括在内。 点击“Apply”安装SDK。

![SDK selection](https://cdn.quasar.dev/img/Android-Studio-SDK-selection.png)

## 运行已有项目

打开Android studio

打开以下路径

[![Ifzkiq.png](https://z3.ax1x.com/2021/11/16/Ifzkiq.png)](https://imgtu.com/i/Ifzkiq)

## 遇到的坑

[配置gradle环境变量](https://www.cnblogs.com/nxjblog/p/12455995.html)

> 检查时候报错可能是没有重启。

以下是可能遇到的坑

gradle打包出错

[Error occurred during initialization of VM Could not reserve enough space for 2097152KB object heap](https://blog.csdn.net/qq_29494055/article/details/111386455)

SDK的build tool版本出错问题

[[Could not determine the dependencies of task ':app:compileDebugJavaWithJavac'. having issue's in Cordova](https://stackoverflow.com/questions/68931751/could-not-determine-the-dependencies-of-task-appcompiledebugjavawithjavac-h)](https://stackoverflow.com/questions/68931751/could-not-determine-the-dependencies-of-task-appcompiledebugjavawithjavac-h)

## 结果

编译成功启动即可

[![IhSvDg.png](https://z3.ax1x.com/2021/11/16/IhSvDg.png)](https://imgtu.com/i/IhSvDg)
