---
title: flex布局
date: 2021-07-28 08:57:01
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: CSS
tags:
	- CSS
---

## flex布局

### 布局原理

flex是flexible box的缩写，意为”弹性布局“，用来为盒状模型提供的灵活性，任何一个容器都可以指定为flex布局。

- 当我们为父盒子设为felx布局以后，子元素的float，clear和vertical-align属性将失效
- 伸缩布局=弹性布局=伸缩盒布局=弹性盒布=flex布局

> margin: atuo可以实现水平居中，flex布局不仅可实现水平居中且能垂直居中。

采用felx布局的元素，称为felx容器，简称容器。它的所用子元素自动成为容器成员，称为felx项目，简称“项目”。

- 体验中div就是flex父容器
- 体验中span就是子容器flex项目
- 子容器可以横向排列也可以纵向排列

总结flex布局原理:

就是通过给父盒子添加flex属性，来控制子盒子的位置和排列方式。

### 常用父项属性

以下由6个属性对父元素设置的

- flex-direction：设置主轴的方向

[![WhgRX9.png](https://z3.ax1x.com/2021/07/27/WhgRX9.png)](https://imgtu.com/i/WhgRX9)

- justify-content： 设置主轴上的子元素排列方式

[![WhfIDH.png](https://z3.ax1x.com/2021/07/27/WhfIDH.png)](https://imgtu.com/i/WhfIDH)

- flex-wrap：设置子元素是否换行

[![WhoKOO.png](https://z3.ax1x.com/2021/07/27/WhoKOO.png)](https://imgtu.com/i/WhoKOO)

- align-content： 设置侧轴上的子元素 的排列方式(多行)

[![WhLGtg.png](https://z3.ax1x.com/2021/07/27/WhLGtg.png)](https://imgtu.com/i/WhLGtg)

- aligin-items： 设置侧轴上的子元素排列方式(单行)

[![WhTcUH.png](https://z3.ax1x.com/2021/07/27/WhTcUH.png)](https://imgtu.com/i/WhTcUH)

- flex-flow：复合属性，相当于同时设置了felx-direction和flex-wrap

[![WhXyl9.png](https://z3.ax1x.com/2021/07/27/WhXyl9.png)](https://imgtu.com/i/WhXyl9)

> align-content和align-items区别
>
> [![WhO3K1.png](https://z3.ax1x.com/2021/07/27/WhO3K1.png)](https://imgtu.com/i/WhO3K1)

### flex布局子项常见属性

- flex子项目占的分数
- align-self控制子项自己再侧轴的排列方式
- order属性定义子项的排列顺序I(前后顺序)

####　flex属性

[![W4ZoaF.png](https://z3.ax1x.com/2021/07/27/W4ZoaF.png)](https://imgtu.com/i/W4ZoaF)

 #### align-self

[![W4m9mV.png](https://z3.ax1x.com/2021/07/27/W4m9mV.png)](https://imgtu.com/i/W4m9mV)

#### order

![W4mVp9.png](https://z3.ax1x.com/2021/07/27/W4mVp9.png)
