---
title: request参数解析-params与query
date: 2023-03-06 23:20:22
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: express
tags:
	- express
---

# request参数解析-params与query

## 1.客户端发送请求的方式

![hnPZN.png](https://i.328888.xyz/2023/03/06/hnPZN.png)

> 此节主要讲params和query

params：路径后面拼接路径

> http://localhost:8000/products/1/ptc

query：路径拼接参数

> http://localhost:8000/login?username=why&password=123

## 2.代码

```js
const express = require('express'); //express是个函数


const app = express();

// params方式  http://localhost:8000/products/1/ptc
app.get('/products/:id/:name',(req,res,next)=>{
    console.log(req.params);
    // req.params=>在数据库种查询真实的商品数据,再返回商品数据
    res.end('商品的详情数据');
})
// query方式  http://localhost:8000/login?username=why&password=123
app.get('/login',(req,res,next)=>{
    console.log(req.query);
    // req.params=>在数据库种匹配用户名和密码,再返回token
    res.end('用户登录成功');
})

app.listen(8000,()=>{
    console.log("客户端请求的方式");
})
```

## 3.结果

![hnYkq.png](https://i.328888.xyz/2023/03/06/hnYkq.png)

![htAOp.png](https://i.328888.xyz/2023/03/06/htAOp.png)

[![htf5k.png](https://i.328888.xyz/2023/03/06/htf5k.png)](https://imgloc.com/i/htf5k)

[![htUav.png](https://i.328888.xyz/2023/03/06/htUav.png)](https://imgloc.com/i/htUav)
