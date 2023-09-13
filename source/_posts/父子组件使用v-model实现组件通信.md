---
title: 父子组件使用v-model实现组件通信
date: 2021-11-05 21:19:59
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags: 	
	- Vue
---

##  父子组件使用v-model实现组件通信

我们在使用别人的组件库的时候，经常是通过v-model来控制一个组件显示和隐藏的效果，例如：弹框，下面一步一步的解开v-model的什么面纱
提到v-model首先想到的就是我们对于表单用户数据的双向数据绑定，操作起来很简洁很粗暴，例如:

```haskell
<input type="text" v-model="msg">

data () {            
    return {                
        msg: ''            
    }        
}
```

其实v-model是个语法糖，上面这一段代码和下面这一段代码是一样的效果：

```kotlin
<input type="text" :value="msg" @input="msg = $event.target.value">
data () {
    return {
        msg: '' 
    }        
}
```

由此可以看出，v-model="msg"实则是 :value="msg" @input="msg = $event.target.value"的语法糖。这里其实就是监听了表单的input事件，然后修改:value对应的值。除了在输入表单上面可以使用v-model外，在组件上也是可以使用的，[这点官网有提到](https://link.segmentfault.com/?enc=5qWW0RYXGz16gm%2Bs3FJCMA%3D%3D.rv24FGszaC%2F43nRa3BkeG4iPiEcS%2BdzlqWAS6pwMUetPNUrOTOXtZqFaMUmaBYP25V%2FoQ78jWF7nxDf9AS3SlVlt2dgbCX6XfSlQkUzOFjh%2BKBztRQFu7UkYGXceDUbZLGvbRfYK4xiXn9ofo7V9%2FO3eB41zVc8At0KRUowdoME%3D)，但是介绍的不是很详细，导致刚接触的小伙伴会有一种云里雾里不知所云的感觉。既然了解了v-model语法糖本质的用法，那么我们就可以这样实现父子组件的双向数据绑定：

**以上原理实现方法，写法1：**

父组件用法：

```xml
<empty v-model="msg"></empty>
```

子组件写法：

```awk
// 点击该按钮触发父子组件的数据同步
<div class="share-btn" @click="confirm">确定</div>

// 接收父组件传递的value值
// 注意，这种实现方法，这里只能使用value属性名
props: {            
    value: {                
        type: Boolean,                
        default: false            
    }        
},
methods: {            
    confirm () {                
        // 双向数据绑定父组件:value对应的值 
        // 通过$emit触发父组件input事件，第二个参数为传递给父组件的值，这里传递了一个false值 
        // 可以理解为最上面展示的@input="msg = $event.target.value"这个事件
        // 即触发父组件的input事件，并将传递的值‘false’赋值给msg             
        this.$emit('input', false)            
    }        
}
```

这种方式实现了父子组件见v-model双向数据绑定的操作，例如你可以试一下实现一个全局弹窗组件的操作，通过v-model控制弹窗的显示隐藏，因为你要在页面内进行某些操作将他显示出来，控制其隐藏的代码是写在组件里面的，当组件隐藏了对应的也要父组件对应的值改变。

