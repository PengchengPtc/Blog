---
title: vue中直接将对象的值赋给自定义的变量，但操作后者时，原对象的值会被修改
date: 2021-12-13 15:36:56
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:
	- Vue
---

### 存在问题

[![oODD2t.png](https://s4.ax1x.com/2021/12/13/oODD2t.png)](https://imgtu.com/i/oODD2t)

如上图为解决办法，其中，this.params4就是定义的一个空对象（this.params4={}），当点击时间触发时将一行记录传到方法openEditBlocCarWind（）中，直接赋值给this.params4，然后修改时就会修改obj的值，加上上面的Json处理后就不会啦。

下图贴出对应的对象打印到控制台的结构：


[![oODIx0.png](https://s4.ax1x.com/2021/12/13/oODIx0.png)](https://imgtu.com/i/oODIx0)

### 解决办法

```js
//this.saleList本地变量
//res.data.data后端请求过来的变量
this.saleList = JSON.parse(JSON.stringify(res.data.data后端请求过来的变量))
```



