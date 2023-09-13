---
title: Vue最简单的实例
date: 2021-02-02 23:27:13
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:
	- Vue
---

## 声明式编程：

```html
<!-- 声明式渲染 -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- 引入vue，也可以直接下载其文件，引用 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <!--在new vue的过程中，就上面的div交给这个vue管理了，会解析其语法，如{{message}}，它会发现其中有一个变量message,然后去找data里面找该语法有没有被定义，如果被定义，变量的值会直接显示-->
    <div id="app">
        {{ message }}
    </div>
    <script>
    //在vue.js里面肯定定义了一个类名叫vue，所以下面直接创建实例对象
    //es6一般不用var，var有很多缺陷，没有变量的作用域
    //实例中也可以添加组件即：
    //如以下形式：
    // template：
    // <div>
    // <h2>{{message}}</h2>
    // <button @click= "btnClick">按钮</button>
    // <h2>{{name}}</h2>
    // </div>
      const app = new Vue({
    //用于挂载要管理的元素
        el: '#app',//在new vue的过程中，就上面的div交给这个#app管理了，会解析其语法，它会发现其中有一个变量message,交给了vue实例管理
    //它会找这个message在data里面有没有被定义，如果被定义了，他会在div中的{{message}}中予以显示
        data: {//定义数据
          message: 'Hello Vue!'
        }
      })
    </script>
</body>
</html>
```

