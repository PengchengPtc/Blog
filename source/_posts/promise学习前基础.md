---
title: promise学习前基础
date: 2021-07-08 17:54:21
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:
	- Vue
---

## 区别实例对象和函数对象

```js
// 1.函数对象与实例对象
// 函数对象：讲函数作为对象使用时，简称为函数对象
// 实例对象：new 函数产生的对象，简称为对象
function Fn() { //Fn函数

}
const fn = new Fn() //Fn是构造函数 fn是实例对象(简称为对象)
console.log(Fn.prototype)//Fn是函数对象，用.来体现出来
Fn.bind({})//Fn是函数对象
$('#test')//jQuery是函数($)
$.get('./test')//jQuery函数对象($)
```

> 语法：简单理解：()左边为函数，.左边是函数对象，new的为实例对象，简称为对象。

## 两种类型的回调函数

## **什么是回调函数？**

在 JavaScript 中，函数即对象。我们可以将对象作为参数传递给函数吗？答案是“可以”。

所以，我们可以将函数作为参数传递给其他函数，在外部函数中调用它。听起来有点复杂？我们看一下下面的例子：

```javascript
function print(callback) {  
    callback();
}
```

print( ) 函数将另一个函数作为参数，并在函数体内部调用它。在 JavaScript 里，我们叫它“回调”。所以，被传递给另一个函数作为参数的函数叫作回调函数。

### **为什么需要回调函数？**

JavaScript 按从上到下的顺序运行代码。但是，在有些情况下，必须在某些情况发生之后，代码才能运行（或者说必须运行），这就不是按顺序运行了。这是异步编程。

回调函数确保：函数在某个任务完成之前不运行，在任务完成之后立即运行。它帮助我们编写异步 JavaScript 代码，避免问题和错误。

在 JavaScript 里创建回调函数的方法是将它作为参数传递给另一个函数，然后当某个任务完成之后，立即调用它。

 **如何创建回调函数**

我们通过一个简单的例子来理解上面的内容。我们想在控制台打印一条消息（message），它在 3 秒之后显示。

```javascript
const message = function() {  
    console.log("This message is shown after 3 seconds");
}
 
setTimeout(message, 3000);
```

JavaScript 有一个内建方法叫作 “setTimeout”，它会在给定的时间段（以毫秒为单位）后调用函数或计算表达式。因此，在这里，经过 3 秒后将调用 message 函数（1 秒= 1000 毫秒） 。

换句话说，**message 函数是在发生某事之后（在本示例中为 3 秒之后），而不是在此之前被调用。因此，message 函数就是一个回调函数**

### **什么是匿名函数？**

此外，我们可以直接在另一个函数内定义一个函数，而不是调用它，比如：

```javascript
setTimeout(function() {  
    console.log("This message is shown after 3 seconds");
}, 3000);
```

我们可以看到，这里的回调函数没有名称。在 JavaScript 里，一个没有名称的函数叫作“匿名函数”。这个例子和上面的例子执行的任务一样。

### **用箭头函数写回调函数**

你也可以用 ES6 箭头函数写回调函数。箭头函数是 JavaScript 里的一种新的函数形式。

```javascript
setTimeout(() => { 
    console.log("This message is shown after 3 seconds");
}, 3000);
```

### 同步回调

1. 理解：立即执行，完全执行完后结束，不会放入回调队列当中
2. 例子：数组遍历相关的回调函数      / Promise的excutor函数

```javascript
// 同步回调函数
const arr = [1,3,5]
arr.forEach(item => {  //遍历回调，同步回调函数，执行完了再执行下一条语句，不会放入队列，一上来就要执行完
    console.log(item)
})
console.log("foreach()之后")
```

> 分析：首先假如我们不知道forEach是遍历，但通过上面函数对象的理解，则arr.forEach是一个函数，arr是函数对象。
>
> arr.forEach调用里面的箭头函数，箭头函数作为参数。arr.forEach自己携带三个参数，1，3，5，里面的回调函数，同样有这三个参数。里面的箭头函数是回调函数，是函数执行后，它才作含参数被执行。

### 异步回调

1. 理解：不会立即执行，会放入回调队列将来执行
2. 例子：定时器回调 / ajax回调 /Promise的成功|失败的回调

```javascript
// 异步回调函数
setTimeout(()=>{
    console.log("timout callback()") //异步回调函数，会放入队列中将来执行，先开始，再等待完成再执行
},0)
console.log("setTimeout()之后")
console.log("setTimeout()之后2")
```

## JS的error处理

> promise里面有错误回调，故要理解js的错误处理

1.错误的类型

-   Error：所有错误的父类型
-   ReferenceError：引用的变量不存在

```js
console.log(a) //ReferenceError:  a is not defined
console.log('-----')//没有捕获error，下面的代码不会执行
```

-   TypeError：数据类型不确定的错误

```js
let bconsole.log(b.xxx)b = {}b.xxx()//TypeError：b.xxx is not a function
```

-   RangeError：数据值不在其所允许的范围内

```js
//递归调用fn，自己调用自己function fn() {    fn()}fn()//RangeError: Maximum call stack size exceeded,递归调用有次数限制
```

-   SyntaxError：语法错误。

```js
const c = """//SyntaxError: Unexpected string
```

2.错误处理

-   捕获错误：try ...catch

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <script>
        //捕获错误：try ... catch
        try {
            let d
            console.log(d.xxx)
        } catch (error) {
            console.log(error.message)
            console.log(error.stack)
        }
        console.log("出错之后")
        //抛出错误：throw error
        
    </script>
</body>

</html>
```

-   抛出错误：throw error

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        function something() {
            // Date.now()是获取当前数字和
            if (Date.now()%2===1) {
                console.log("当前时间为奇数，可以执行任务")
            }else {//如果时间是偶数抛出异常，由调用来处理
                throw new Error("当前时间为偶数,无法执行任务")
            }
        }
    //捕获处理异常
    try {
        something()
    } catch (error) {
        alert(error.message)
        // alert(Date.now)
    }
    </script>
</body>
</html>
```

3.错误对象

-   message属性：错误相关信息
-   stack属性： 函数调用栈记录信息
