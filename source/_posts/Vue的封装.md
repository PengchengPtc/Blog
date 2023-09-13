---
title: .Vue的封装
date: 2021-02-02 23:27:53
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
mathjax: false
tags:
	- Vue
---

## .vue的文件的封装：

### 1.首先，创建的实例对象：

main.js文件里面创建如下实例：

```js
const app new Vue({
    
})
```

app没有什么实质性的用处，其实可以省略const app，简写为以下：

```js
new Vue({
    
})
```

html文件里面的script标签里面的内容，直接放到新建的对象里面。

```js
new Vue({
    el:'#app',
    data: {
        message:'Hello Webpack',
        name:'coderwhy'
    },
    methods:{
        btnClick(){
            
        }
    } 
})
```

index.html剩余的内容：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div id="app">
        <h2>{{message}}</h2>
        <button @click= "btnClick">按钮</button>
        <h2>{{name}}</h2>
     </div>
</body>
</html>
```

接下来，public文件夹中的index.html文件中的div里面的东西不需要动，前提是要做一个.vue的封装。

index.html只保存如下代码：**一般是不会改的。**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <!--和Vue对应-->
    <div id="app">
        
    </div>
</body>
</html>
```

### 2.定义一个template属性：Vue内部会把template里面的内容和index.html里面的div替换，即template会替换el。

```js
new Vue({
    el:'#app',
        template:`
        <div>
        <h2>{{message}}</h2>
        <button @click= "btnClick">按钮</button>
        <h2>{{name}}</h2>
        </div>
`
    ,
    data: {
        message:'Hello Webpack',
        name:'coderwhy'
    },
    methods:{
        btnClick(){
            
        }
    } 
})
```

第一，Vue实例中写太多template,会显得臃肿,需单独创建一个对象：后面这个对象会演变为一个组件，即.vue文件。

```js
const App = {
    template:`
        <div>
        <h2>{{message}}</h2>
        <button @click= "btnClick">按钮</button>
        <h2>{{name}}</h2>
        </div>
`
    ,
}
```

删减上面template内容后的mian.js文件的创建实例剩余部分：

```js
new Vue({
    el:'#app',
    template:``,
    data: {
        message:'Hello Webpack',
        name:'coderwhy'
    },
    methods:{
        btnClick(){
            
        }
    } 
})
```

同理，data的里面内容也可以转到组件template当中,全部抽取到新建立的一个App对象当中

```js
const App = {
    template:`
        <div>
        <h2>{{message}}</h2>
        <button @click= "btnClick">按钮</button>
        <h2>{{name}}</h2>
        </div>
`
,
    data(){
 //转换过来多了个return，因为是data()函数
    return {
         message:'Hello Webpack',
         name:'coderwhy 
    }           
}
}
```

同理methods也可以抽取到App对象当中：

```js
const App = {
    template:`
        <div>
        <h2>{{message}}</h2>
        <button @click= "btnClick">按钮</button>
        <h2>{{name}}</h2>
        </div>,
`
,
        data(){
        //转换过来多了个return，因为是data()函数
         return {
                message:'Hello Webpack',
                 name:'coderwhy'
                 }
 ,
         methods:{
                 btnClick(){
            
         }
    } 
}
}
```

以上App对象实则是个组件，只需在Vue实例里面去注册这个App，在Vue里面注册组件，在template里面使用组件。在Vue实例里面找到

这个组件，然后解析template。

```js
new Vue({
    el:'#app',
//在这个了用app，就在template中用了一个组件，先注册一个组件，再在template用了这个组件
    template:'<App/>',//这个<App/>就代替了那个index.html中的<div></div>
//在components注册App,这就把整个组件封装进来了
    components:{
        App
    }
})
```

创建一个app.js文件，放入刚刚创立的App对象：

把App常量的东西剪掉，复制到app.js中,相当于把组件放到了app.js中

```js
export default{
   //以下为模板代码
    template:`
        <div>
        <h2>{{message}}</h2>
        <button @click= "btnClick">按钮</button>
        <h2>{{name}}</h2>
        </div>,
`,
//以下为js代码
        data(){
        //转换过来多了个return，因为是data()函数
         return {
                 message:'Hello Webpack',
                 name:'coderwhy'
                 }   
        },
        methods:{
                 btnClick(){
            
        }
    } 

}
```

main.js中的直接引入新键的app.js就行

```js
const App =变成以下引入：
//default导入不需要大括号x，因为只有一个变量
import App from "./vue/app"
//因为默认是default，App其实是新命名的变量名，而App其实就是一个对象赋值得来的，
//export default 直接{}
//省略了变量名App
```

但改实例对象赋值的变量的，里面的模板和js代码没有分离。

### 3.创建App.vue文件，把template和js代码分离。

新建app.vue组件，把app.js里面的东西分离，效果如下。

```js
<template>
       <div>
        <h2 class = "title">{{message}}</h2>
        <button @click= "btnClick">按钮</button>
        <h2>{{name}}</h2>
        </div>
</template>
<script>
        //export default一个对象
        export default {
//这是自带的
		name:"App"，
         data(){
        //转换过来多了个return，因为是data()函数
         return {
                 message:'Hello Webpack',
                 name:'coderwhy'
                 }   
         }，
        methods:{
                 btnClick(){
            
        }
    } 
 }
</script>
<style scoped>
    .title{
        color:green;
    }
</style>
```

在main.js中导导入：

```js
import App from './vue/App.vue'
```

创建的App.vue无法加载，要配置node。在在webpack.config.js里面配置。node_modules里面的东西。

### 以上就是.vue文件封装的全过程，实现组件化开发。