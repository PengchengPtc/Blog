---
title: return的实质
date: 2021-03-06 20:50:19
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: JS
tags:
	- JS
---

### Retun的实质:

1. 返回给被赋值的对象的变量，用变量接收

   ```js
   const c = (a,b) => {
       return a+b
   }
   console.log(c(1,1))
   ```

2. 掉请求过程中

   这个err，return给了confirmRestult变量，该变量接收了
   
   ```js
    const confirmResult = await this.$confirm('此操作将永久删除该用户, 是否继续?', '提示', {
             confirmButtonText: '确定',
             cancelButtonText: '取消',
             type: 'warning'
             // catch是捕获错误的
           }).catch(err =>
           err)
   ```
   
   



