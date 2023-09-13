---
title: '对export { }的理解'
date: 2023-03-03 14:45:51
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: es6
tags: 	
	- es6
---

# 对export { }的理解

> export后面的{}不是对象！！！

[![ppk2ZOU.png](https://s1.ax1x.com/2023/03/03/ppk2ZOU.png)](https://imgse.com/i/ppk2ZOU)

> 重点理解：如果把let name = "why"变成et name = { }变成对象，后面的const name =0x1相当于引用了地址，在index.js里面再改name同样foo.js里面的值也得更着改，因为是改的是地址。

## 一个小实例

```js
const a = 18;
a = 19; //语法错误，变量不能改
```

```js
const a = {
    name:'ptc',
    age: 18
};
a.name = 'why'; //可以改因为改的是地址
console.log(a.name); // 'why'
```

