---
title: react脚手架
date: 2021-10-28 14:05:53
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

# react脚手架

### 概述

> 之前的代码不是开发环境，编码慢，用脚手架可以快速编码。
>
> react脚手架是用webpack搭建的。
>
> 但不需要手动配置，facebook已经为我们做好了一个脚手架。
>
> 前端三大框架Angular,React,Vue都有自己的脚手架。

### react脚手架

1. xxx脚手架用来帮助程序员快速搭建一个基于xxx库的模板项目。
   - 包含了所有需要的配置(语法检查、jsx编译、devSever)。
   - 下载好所有的相关依赖。
   - 可以直接运一个简单效果
2. react提供了一个用于创建react项目的脚手架库(create-react-app)，基于react脚手架的项目，一般直接叫搭建react脚手架。
3. 项目的整体技术架构：react+webpack+es6+eslint
4. 使用脚手架开发项目的特点：模块化，组件化，工程化。

> 工程化，就是用 webpack搭建项目，到编译，语法检查，编译，一条龙服务，全自动的项目，就是一个工程化的项目，类似于生产线。

### 创建项目并启动

***\*第一步\****，全局安装：npm i -g create-react-app

***\*第二步\****，切换到想创项目的目录，使用命令：create-react-app hello-react

***\*第三步\****，进入项目文件夹：cd hello-react

***\*第四步\****，启动项目：npm start

> npm与yarn一样的功能，只不过推荐使用yarn，因为react和yarn都是facebook开发的。

[![5qaZut.md.png](https://z3.ax1x.com/2021/10/28/5qaZut.md.png)](https://imgtu.com/i/5qaZut)

> npm run eject是把webpack本隐藏的文件暴露出来，不可逆。
>
> npm test 用于测试。

### 脚手架文件介绍

```#
	public ---- 静态资源文件夹
		favicon.icon ------ 网站页签图标
		index.html -------- 主页面
		logo192.png ------- logo图
		logo512.png ------- logo图
		manifest.json ----- 应用加壳的配置文件
		robots.txt -------- 爬虫协议文件
src ---- 源码文件夹
		App.css -------- App组件的样式
		App.js --------- App组件
		App.test.js ---- 用于给App做测试
		index.css ------ 样式，通用性
		index.js ------- 入口文件
		logo.svg ------- logo图
		reportWebVitals.js
			--- 页面性能分析文件(需要web-vitals库的支持)
		setupTests.js
			---- 组件单元测试的文件(需要jest-dom库的支持)
```

html文件：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <!-- 引入图标，%PUBLIC_URL%代表public文件夹路径 -->
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <!-- 开启理想视口，用做移动端网页适配 -->
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <!-- 用于配置浏览器页签+地址栏的颜色(仅仅支持安卓手机浏览器，且兼容性不好) -->
    <meta name="theme-color" content="#000000" />
    <!-- 用于描述网页，用于搜索爬虫 -->
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <!-- 用于指定网页添加到手机屏幕后的图标，仅仅支持苹果手机 -->
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <!-- 用于应用加壳，应用加壳时候的配置文件 -->
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />

    <title>React App</title>
  </head>
  <body>
    <!-- 若浏览器不支持js,则展示标签中的内容 -->
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <!-- 容器 -->
    <div id="root"></div>
  </body>
</html>

```

用客户端开发，安卓和ios应用呀学java

> Android  java
>
> ios     oc swift

我们现在是web端开发，开发的是spa项目，s大一，p页面，a应用。写的是网页。要转换为客户端应用，有一种实现方式，就是先用框架生成html项目，通过应用加壳可以实现转换为apk和ios应用，壳里面是html即是网页，要么就用Java直接开发

