---
title: react样式模块化
date: 2021-10-28 16:13:37
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

# react样式模块化

### 为什么要做模块化

> 组件样式的名字如果一样，到app.js里面就会冲突

### 实现样式模块化

一般引入css只能，

```js
import ".index.css"
```

不能用变量接。

[![5qv9Zd.png](https://z3.ax1x.com/2021/10/28/5qv9Zd.png)](https://imgtu.com/i/5qv9Zd)

> 通过改文件名，加module，然后就可以去接这个样式，样式就保存在hello里面。

