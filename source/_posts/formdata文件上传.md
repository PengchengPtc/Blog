---
title: formdata文件上传
date: 2023-03-07 03:00:35
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: express
tags:
	- express
---

# formdata文件上传

### 1.formdata

> formdata可以选择文件类型，可以是文件，也可以是text，文件可以是图片

![hV3l8.png](https://i.328888.xyz/2023/03/06/hV3l8.png)

## 2.代码

```js
const path = require('path');

const express = require('express'); //express是个函数
const multer = require('multer');   // 用于express框解析，但在epress内，需要手动安装


// 自定义文件名
const storage = multer.diskStorage({
    destination: (req,file,cb)=>{
        // cb是回调函数
        cb(null,'./uploads');
    },
    filename:(res,file,cb)=>{
        cb(null,Date.now()+path.extname(file.originalname));
    }
})

const app = express();  //函数就有返回值，这里取express()的返回值
const upload = multer({
    // dest: './uploads'    // 文件存储位置，storage方式是可以自定义文件名的方式
    storage
}
); //multer也是一个函数

app.use(express.json());    // json数据格式解析
app.use(express.urlencoded({extended:true})); // urlencoded数据格式解析
// app.use(upload.any());      // formdata数据格式解析,其实是解析非文件的任何内容,不能当全局使用会和后面upload里面的single或者fields冲突!!!!!!!!!!!!!!!!!!!

app.post('/login',upload.any(),(req,res,next)=>{
    console.log(req.body); // 拿到req里面的内容，body是在解析过程新设置的变量，赋的值是解析后的值
    res.end('用户登录成功');
})

// 还差个中间件,即upload.single(file)，用于上传文件，并且进行保存操作,用upload.array也可以,用fields也是可以的
app.post('/upload',upload.fields([{name:"file",maxCount:2}]),(req,res,next)=>{
      console.log(req.files);  //打印文件内容
       res.end("文件上传成功");
})

app.listen(8000,()=>{
    console.log("form-data解析");
})
```

## 3.结果

![h0CDz.png](https://i.328888.xyz/2023/03/07/h0CDz.png)
