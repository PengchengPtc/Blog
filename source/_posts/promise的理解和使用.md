---
title: promise的理解和使用
date: 2021-07-09 11:58:31
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:	
	 - Vue
---

## promise是什么？

### 理解

1.抽象表达

​	Promise是JS中进行异步编程的新的解决方案(旧的是谁？)

> 旧的是纯回掉形式

2.具体表达

1. 从语法上来说：Promise是一个构造函数。
2. 从功能上来说，promise对象用来封装一个异步操作并可以获得其结果。

###　promise的状态改变

1. pending(未确定)变成resolved(成功)
2. pending变为rejected(失败)

最开始new的时候，状态为pending，只有两种，且一个promise对象只能改变一次，无论变为成功还是失败，都会有一个结果数据，成功的结果数据一般称为value，失败的结果数据一般称为reason。

[![RLTUXV.png](https://z3.ax1x.com/2021/07/08/RLTUXV.png)](https://imgtu.com/i/RLTUXV)

### promise的基本使用

```js
// 1.创建一个新的promise对象
const p = new Promise((resolve,reject) => {//执行器函数  同步回调
     console.log("执行执行器 excutor")
    //2.执行异步操作任务
    setTimeout(
        ()=>{
        const time = Date.now() //如果当前时间为偶数就代表成功，否则代表失败
        if (time %2 == 0){
            resolve("成功的数据,time="+ time)
        }else {
            //3.2 如果失败了，调用reject(reason)
            reject("成功的数据,time="+ time)
        }
    },1000);
    //3.1.如果成功了，调用resolve(value)
    //3.1.如果失败了，调用reject(reason
})
console.log
p.then(
    value => {//接收得到成功的value的数据    onResolved 当为resolved状态执行
        console.log("成功的回调",value)
    },
    reason => {//接收得到失败的value数据     onRejected 当为onRejected状态执行
        console.log("失败的回调",reason) 
    }
)
```

### 为什么要用promise？

相比于纯回调函数：

1.promise相比于纯回调函数，指定回调函数比较灵活。

```js
// 使用纯回调函数的方式
// 成功的回调函数
function successCallback(result) {
    console.log("声音文件创建成功"+result)
}
// 失败的回调函数
function failureCallback(error) {
    console.log("声音文件创建失败"+error)
}

// 使用纯回调函数
// 先指定回调函数(即在参数中携带两个回调函数)，即先指定了回调函数，才执行的异步任务，在执行异步操作，否则
// 创建音频文件肯定得花时间，audioSettings是创建文件的配置文件
createAudioFileAsync(audioSettings,successCallback,failureCallback)
// 不能先执行异步操作再指定回调函数，它完都完成了，你指定回调函数已经得不到数据了



// 使用promise的方式
//再执行异步操作
    const promise = createAudioFileAsync(audioSettings);         /*创建音频文件，返回一个promise，异步操作在createAudioFileAsync里面执行。
    这个异步操作就是上面写的promise的基本使用*/
    // 上面一行执行完了，异步操作就完了，得到promise对象的时候，异步对象已经启动了。
    // 再指定回调操作
    setTimeout(()=>{
        promise.then(successCallback,failureCallback);
    },3000);



/*
由上面的比较得知:
1.纯回调的方式，回调函数必须在异步操作前面指定
2.promise方式，则可以在异步操作完后指定异步操作，然后得到返回的成功或者失败的数据
比较知道:promise指定回调函数较为灵活。
*/
```

2.纯回调可能存在回调地狱。

promise支持链式调用，可以解决回调地狱问题。

回调函数嵌套调用时候，上一层函数的结果作为下一层函数参数的条件。

回调地狱实例：

```js
doSomething(function (result) {
    doSomethingElse(result, function (newResult) {
        doThirdThing(newResult, function (finalResult) {
            console.log("Got the final result:" + finalResult)
        }, failureCallback)
    }, failureCallback)
}, failureCallback)
```

使用promise的链式调用解决回调地狱：非嵌套关系，只写了成功的回调，没有写失败的回调处理，但失败的回调都会找到最后一个catch(failureCallback)

```js
doSomething().then(function (result) {
    return doSomethingElse(result)
})
    .then(function (newResult) {
        return doThirdThing(newResult)
    })
    .then(function (finalResult) {
        console.log("Got the final result", +finalResult)
    }
        .catch(failureCallback))
```

> doSomething()就是一个promise
>
> 每一个then前面都是一个promise
>
> newResult=doSomethingElse(result)以此类推

回调地狱的终极解决方式，promise并非解决回调地狱的终极解决方案，因为他还有回调函数，但他没有嵌套。

async/await:回调地狱的终极解决方案

```js
async function request() {
    try {
        //result是doSomething这个promise返回的成功的结果，下面以此类推
        const result = await doSomething()
        const newResult = await doSomethingElse(result)
        const finalResult = await doThirdThing(newResult)
        console.log("Got the final result" + finalResult)
    } catch (error) {
        failureCallback(error)
    }
}
```



