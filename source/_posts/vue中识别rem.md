---
title: vue中识别rem
date: 2021-09-01 11:37:00
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:
	- Vue
---

vue中使用rem
vue现在正是火的势头上，作者说明年估计3.0要出来了。那么在vue我们如果做移动端自适应怎么弄呢？

### 安装flexible

在命令行中运行如下安装：

```bash
npm i lib-flexible --save-dev
```

### 引入flexible

在项目入口文件 main.js 里 引入 lib-flexible

```bash
// main.js
import 'lib-flexible'
```


​	对于我们的index.html，最好是不要meta标签，flexible会自动添加上的，因为有一个判断。当然了，懒惰果然是最大的生产力，有的人觉得换算rem太麻烦，就出现了插件px2rem-loader，把px自动转化为对应的rem。但是呢，麻烦的就是如果引入外部的css文件，那么也会把px转化为rem。自己在项目中就是手动计算rem，用上面的方法，直接除以100，这个应该很简单吧，都是程序员，数学这个还是可以吧......

### 大屏自适应
[![hw6ycD.png](https://z3.ax1x.com/2021/09/01/hw6ycD.png)](https://imgtu.com/i/hw6ycD)

