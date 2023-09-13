---
title: express路由的使用
date: 2023-03-07 03:02:04
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: express
tags:
	- express
---

# express路由的使用

## 1.路由

![h0Obk.png](https://i.328888.xyz/2023/03/07/h0Obk.png)

> 相对教重复，全放app不方便管理

![h0bzL.png](https://i.328888.xyz/2023/03/07/h0bzL.png)

> 一个minni-app就封装所有的user接口

## 2创建路由文件

![h0ICU.png](https://i.328888.xyz/2023/03/07/h0ICU.png)

```js
/*
举个例子
 请求所有的用户信息: get/users
 请求所有的某个用户信息:get/users/:id
 请求所有的某个用户信息:post/users body:{username:password}
 请求所有的某个用户信息:delete/users/:id
 请求所有的某个用户信息:post/users/:id{nickname}
 */

const express = require('express');

const router = express.Router();

router.get('/',(req,res,next)=>{
    res.json(["why","kobe","lilei"]);
})

router.get('/:id',(req,res,next)=>{
    res.json(`${req.params.id}用户的信息`);
})

router.post('/',(req,res,next)=>{
    res.json("create user success");
})

module.exports = router;
```

## 3使用路由

```js
const express = require('express');

const userRouter = require('./routers/user');

const productRouter = require("./routers/products")

const app = express();

app.use("/users",userRouter);

app.use('/products',userRouter);

app.listen(8000,()=>{
    console.log("路由服务启动成功~");
})
```

## 4结果自测
