---
title: 个人对promise的理解
date: 2021-07-30 12:26:15
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags: 	
	- Vue
---

### 个人对promise的理解

> 学promise之前，要理解回掉的概念。

#### 回调

回调函数就是作为参数被另外一个参数调用，但必须是外面的函数先执行，里面的函数再执行才能成回调。

回调分为同步回掉和异步回调。

##### 同步回调

外面函数执行后，里面执行里面的回调函数。

##### 异步回调

外面的函数执行需要一定时间，执行完之后才调用里面的回调函数。

###　promise过程

promise就是一个异步回调，每一个异步操作(请求)执行完之后都有两个状态，成功执行resolve，失败执行reject，此操作封装到promise对象里面，此时promise的值为捕获的成功的数据或者失败的数据。

然后通过then方法获取成功回掉的数据和失败回调的数据，然后得到了一个新的promise对象。

#### 为什么使用promise

1.解决了使用纯回调必须将异步操作和成功回调和失败的 回调函数一起调用，不然异步操作执行完就拿不到数据。

2.解决了回调地狱问题。

### 解决回调地狱最优方法其实是async/await

async/await其实是是对promise的一个简化操作

```js
async function request() {
     const result = await doSomething()
}
```

> doSomething()即异步操作
>
> result返回的成功的数据

