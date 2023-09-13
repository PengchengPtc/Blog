---
title: import函数
date: 2023-03-03 14:46:08
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: es6
tags:
	- es6
---

# import函数

[![ppk2ZOU.png](https://s1.ax1x.com/2023/03/03/ppk2ZOU.png)](https://imgse.com/i/ppk2ZOU)

> 重点：js引擎解析代码的过程：parsing(解析)-》ast-》字节码-》二进制-》执行，解析时候已经确定好了依赖关系

以下写法是错误的

```js
let flag = true;
if (flag) {
    import fomat from "./modules/foo.js"
}
```

>  import fomat from "./modules/foo.js"是解析环境下的代码，无法用在运行环境下，import不是函数是关键字，需要解析，if(flag){}是js到了运行时候，而import fomat from "./modules/foo.js"只是解析阶段，从而报错。

改进方式，改成执行函数,如果是webpack的环境下：es commonJs 用require()

```js
let flag = true;
if (flag) {
    require( "./modules/foo.js");
}
```

或者使用inport函数

```js
let flag = true;
if (flag) {
    import( "./modules/foo.js");
}
```

> 重点：此处的import是一个异步函数，他会等js文件加载成功再去调用(可以先让下面的代码运行)，返回一个promise，一个契约
>
> 类似于发请求和接请求的时候，他会等请求接受到时候再回调做赋值操作(但其他代码可能已经运行)，所以才会有页面数据后出现的情况

最终：

```js
let flag = true;
if (flag) {
    import( "./modules/foo.js").then(res=> {
        console.log("在then中打印");
        console.log(res.name);
        console.log(res.age);
    }).catch(err=>{
        
})
}
```

> .then后执行回调函数,回调就是把一个函数的返回值作为参数传给另外一个函数去调用。
