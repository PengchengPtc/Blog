---
title: hello react
date: 2021-09-21 20:29:49
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

# React

## 认识React

### 是什么？

用于构建用户界面的javascript的库。

是一个将数据渲染为html视图的开源javascript库。

### 怎么展示数据

[![hLa1ZF.png](https://z3.ax1x.com/2021/09/09/hLa1ZF.png)](https://imgtu.com/i/hLa1ZF)

> react负责最后最后一步，只负责数据的呈现。

### 谁开发的？

> 由Facebook开发，且开源。现被腾讯阿里广泛使用。

###　为什么要学？

[![hLw9HS.md.png](https://z3.ax1x.com/2021/09/09/hLw9HS.md.png)](https://imgtu.com/i/hLw9HS)

### react的特点

[![hLwWVS.png](https://z3.ax1x.com/2021/09/09/hLwWVS.png)](https://imgtu.com/i/hLwWVS)

### 原生js和react操作数据的区别

[![hL01Z8.png](https://z3.ax1x.com/2021/09/09/hL01Z8.png)](https://imgtu.com/i/hL01Z8)

[![hL0roF.png](https://z3.ax1x.com/2021/09/09/hL0roF.png)](https://imgtu.com/i/hL0roF)

> react会比较虚拟dom，已经有的dom不会重新操作，只会操作新的。

### jQuery与react的区别

首先来看jQuery

> jQuery 是一个 JavaScript 库。
>
> jQuery 极大地简化了 JavaScript 编程。
>
> jQuery 很容易学习。

jQuery只是简化了操作dom的代码，用$来简化代码，但是并没有简化过程，而react是简化过程。

## hello react

### 首先引入babel，react核心库，react操作dom库

babel可以

> 1.es6 =》 es5  以前
>
> 2.jsx  =》 js 现在

代码区域：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- 准备好一个容器 -->
    <div id="test"></div>
    <!-- 引入包，注意引入顺序 -->
    <!-- 引入react核心库 -->
    <script type="text/javascript" src="../js/react.development.js"></script>
    <!-- 引入react-dom，用于支持react操作dom -->
    <script type="text/javascript" src="../js/react-dom.development.js"></script>
    <!-- 引入babel，用于讲jsx转入为js -->
    <script type="text/javascript" src="../js/babel.min.js"></script>
    <!-- 下面写babel表示写的是jsx，而不是js，而且用babel来翻译，此处必须写babel -->
    <script type="text/babel">
        // 1.创建虚拟dom
        const VDOM = <h1>Hello,React</h1>  //此处一定不要写引号，因为不是字符串
        // 2.渲染虚拟dom到页面,ReactDom是上面引入的react-dom
        // ReactDom.render(虚拟dom,容器)
        ReactDOM.render(VDOM,document.getElementById("test"))
    </script>
</body>
</html>
```

效果：

[![hL4Qa9.png](https://z3.ax1x.com/2021/09/09/hL4Qa9.png)](https://imgtu.com/i/hL4Qa9)

> jsx比纯js写法简单，jsx可以比较简洁的创建虚拟dom

### 虚拟dom与真实dom

```js
  const TDOM = document.getElementById("test")
        console.log("虚拟dom",VDOM);
        console.log("真实dom",TDOM);
        debugger;
        // console.log(typeof VDOM);
        // console.log(VDOM instanceof Object);
        // 关于虚拟dom
        // 1.本质是Object类型的对象(一般对象)
        // 2.虚拟dom比较"轻",真实dom比较重，因为虚拟dom是react内部在用，无需真实dom上那么的多属性
        // 3.虚拟dom最终会被React转化为真实dom,呈现在页面上
```

### jsx语法规则

>  	   	   1.定义虚拟dom时候，不要写引号。
>
>  	      2.标签中混入js表达式要用{}。
>  	      3.样式的类名不要用class，要用className。
>  	      4.内联样式，要用style={{key:value}}的形式去写
>  	      5.只有一个根标签
>  	      6.标签必须闭合
>  	      7.标签首字母
>  	      	(1).若小写字母开头，则将改标签转为html中同名元素，若htm1中无该标签对应的同名元素，则报错。
>  	    	  (2).若大写字母开头，react就去渲染对应的组件，若组件没有定义，则报错。|

#### xml

> xml早期用于存储和传输数据

```html
<student>
    <name>Tom</name>
    <age>19</age>
</student>
```

====》

```js
"{"name":"Tom","age":19}"
```

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .title {
            background-color: orange;
            width: 200px;
        }
    </style>
</head>

<body>
    <!-- 准备好一个容器 -->
    <div id="test"></div>
    <!-- 引入包，注意引入顺序 -->
    <!-- 引入react核心库 -->
    <script type="text/javascript" src="../js/react.development.js"></script>
    <!-- 引入react-dom，用于支持react操作dom -->
    <script type="text/javascript" src="../js/react-dom.development.js"></script>
    <!-- 引入babel，用于讲jsx转入为js -->
    <script type="text/javascript" src="../js/babel.min.js"></script>
    <!-- 下面写babel表示写的是jsx，而不是js，而且用babel来翻译，此处必须写babel -->
    <script type="text/babel">
        const myId = "aTgUiGu"
        const myData = "Hello,rEaCt"
        // 1.创建虚拟dom 
        const VDOM = (
            <div>
                <h2 className="title" id={myId.toLowerCase()}>
                    <span style={{ color: "white", fontSize: "29px" }}>{myData.toLocaleLowerCase()}</span>
                </h2>
                <h2 className="title" id={myId.toUpperCase()}>
                    <span style={{ color: "white", fontSize: "29px" }}>{myData.toLocaleLowerCase()}</span>
                </h2>
                <input type="text" />
            </div>
        )
        //渲染虚拟dom到页面
        ReactDOM.render(VDOM, document.getElementById("test"))
        /*
            jsx语法规则:
                1.定义虚拟dom时候，不要写引号。
                2.标签中混入js表达式要用{}。
                3.样式的类名不要用class，要用className。
                4.内联样式，要用style={{key:value}}的形式去写
                5.只有一个根标签
                6.标签必须闭合
                7.标签首字母
                (1).若小写字母开头，则将改标签转为html中同名元素，若htm1中无该标签对应的同名元素，则报错。
                (2).若大写字母开头，react就去渲染对应的组件，若组件没有定义，则报错。|
            */
    </script>
</body>

</html>
```

###　表达式和代码(语句)的区别

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <!-- 准备好一个容器 -->
    <div id="test"></div>
    <!-- 引入包，注意引入顺序 -->
    <!-- 引入react核心库 -->
    <script type="text/javascript" src="../js/react.development.js"></script>
    <!-- 引入react-dom，用于支持react操作dom -->
    <script type="text/javascript" src="../js/react-dom.development.js"></script>
    <!-- 引入babel，用于讲jsx转入为js -->
    <script type="text/javascript" src="../js/babel.min.js"></script>
    <!-- 下面写babel表示写的是jsx，而不是js，而且用babel来翻译，此处必须写babel -->
    <script type="text/babel">
        /*一定注意区分:【js语句(代码)】与【js表达式】
                用const可以接，就是表达式，不能接就是代码
                1.表达式：一个表达式会表示一个值，可以放在任何一个需要值的地方下面这这些都是表达式
                (1). a
                (2). a + b
                (3). demo(1)
                (4).arr.map()
                2.语句(代码)
                下面这些都是语句(代码)：
                    (1).if() {}
                    (2).for() {}
                    (3).switch(){case:xxxxx}
        */
        const data = ['Angular', 'react', 'Vue']
        // 1.创建虚拟dom
        const VDOM = (
            <div>
                <h1>前端js框架列表</h1>
                <ul>
                    {
                        data.map((item,index)=>{
                            return <li key={index}>{item}</li>
                        })
                    }
                </ul>
            </div>
        ) //此处一定不要写引号，因为不是字符串
        // 2.渲染虚拟dom到页面,ReactDom是上面引入的react-dom
        // ReactDom.render(虚拟dom,容器)
        ReactDOM.render(VDOM, document.getElementById("test"))
    </script>
</body>

</html>
```

## react中的组件

### 函数组件

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <!-- 准备好一个容器 -->
    <div id="test"></div>
    <!-- 引入包，注意引入顺序 -->
    <!-- 引入react核心库 -->
    <script type="text/javascript" src="../js/react.development.js"></script>
    <!-- 引入react-dom，用于支持react操作dom -->
    <script type="text/javascript" src="../js/react-dom.development.js"></script>
    <!-- 引入babel，用于讲jsx转入为js -->
    <script type="text/javascript" src="../js/babel.min.js"></script>
    <!-- 下面写babel表示写的是jsx，而不是js，而且用babel来翻译，此处必须写babel -->
    <script type="text/babel">
      //1.创建函数式组件
       function MyComponent() {
           console.log(this); //此处的this是undefined，因为babel编译后开启了严格模式
           return <h2>我是用函数定义的组件(适用于【简单组件】的定义)</h2>
       }
       //2.渲染组件到页面
       ReactDOM.render(<MyComponent/>,document.getElementById("test"))
       /*
        执行了ReactDOM.render(<Demo/>,document.getElementById("test"))之后会发生什么
            1.react解析组件标签，找到
            2.发现组件是使用函数定义的，随后调用函数，将返回的虚拟dom转为真实dom，随后呈现再页面中。
       */
    </script>
</body>
</html>
```



