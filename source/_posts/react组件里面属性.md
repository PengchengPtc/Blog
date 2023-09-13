---
title: React组件里面属性之state
date: 2021-09-22 00:07:28
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

## react中组件实例的属性

### 组件实例的三大核心属性  1.state (类组件)

### 概述

组件实例有几个属性，原型是react里面的component，其中一个是state表示状态，默认为空值。空值是react赋的。

[![4tUvSe.png](https://z3.ax1x.com/2021/09/21/4tUvSe.png)](https://imgtu.com/i/4tUvSe)

### 代码(初写)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <!-- 准备好一个“容器” -->
    <div id="test">

    </div>
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
        // let that = this
        //1.创建类式组件,是继承react里面内置的一个类
        class Weather extends React.Component {
            // 构造器调用了几次？ ——1次
            constructor(props) {
                console.log("constructor");
                super(props)
                this.state = { isHot: false, wind: "微风" }
                // that = this
                // bind是改this指向,this指向改成this,this即实例对象,实例自身会生成一个changeWeather函数,会被优先调用
                this.changeWeather = this.changeWeather.bind(this)
            }
            //构造器可以不用写，直接继承，但render必须写
            //render调用几次？ ---- 1+n次 1是初始化的那次，n是状态跟新的次数
            render() {
                console.log("render");
                //render是放在哪里的？ --- 类的原型对象上，供实例使用。
                //render中的this是谁？---- MyComponent的实例对象。
                console.log("redner中的this", this);
                // 解构赋值
                const { isHot,wind } = this.state
                // react中onclik中c要大写,且函数名不能是字符串，要读出demo得用{}，且吧demo()去掉，demo交给onclick回调，加括号就相当于直接被调用了
                return <h2 onClick={this.changeWeather}>今天天气很{isHot ? "炎热" : "凉爽"},{wind}</h2>
            }
            // changeweather放在哪里?-- weather的原型对象上，供实例使用
            // 通过weather实例调用changeweather时，changelweather中的this就是weather实例
            // changeWeather调用几次？ 点几次调用几次
            changeWeather() {
            console.log('changeWeather');
            // alert("标题被点击了")
            // babel开启了严格模式，this不是window而是undefined，this是拿不到state里面的数据的
            // 类中方法默认开启了局部严格模式，所有changeWeather中的this为undefined，没有通过实例来调用
            // console.log(this.state.isHot);
            // 严重注意，状态(state)不可直接更改，下面这行就是直接更改，要借助一个内置api去更改
            const isHot = this.state.isHot  
            // this.state.isHot = !isHot        这是错误写法
            // 严重注意，状态必须通过setState更改,是一种合并而不是替代
            this.setState({isHot:!isHot})
        }
        }
        //2.渲染组件到页面
        // 上面一个render和下面一个render不是一个东西
        ReactDOM.render(<Weather />, document.getElementById("test"))
     /*
        执行了ReactDOM.render(<Demo/>,document.getElementById("test"))之后会发生什么
    1.react解析组件标签，找到了MyComponent组件。
    2.发现组件的使用类定义的，随后new出来该类的实例，并通过实例调用到原型的render方法。
    3.将render返回的虚拟DOM转为真实dom，随后呈现在页面中。
    */
    </script>
</body>

</html>
```

总结

> 1. 构造器this是没问题的。
> 2. render构造器中this也没问题,因为写成了组件，组件默认会创建一个实例，然后通过实例去调用，this会生效。
> 3. changeWeather中的this有问题，因为不是通过实例来调用的，如果要使用则需要改this指向。

### 简写

1. 初始化状态简写

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <!-- 准备好一个“容器” -->
    <div id="test">

    </div>
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
        // 1.创建类式组件
        class Weather extends React.Component {
            // 为实例添加一个属性
            state = { isHot: false, wind: "微风" }
            render() {
                const { isHot, wind } = this.state
                return <h2 onClick={this.changeWeather}>今天天气很{isHot ? "炎热" : "凉爽"},{wind}</h2>
            }
            // 以赋值形式出现，不需要写在原型对象上，写在示例自身，但this有问题，所以得写成箭头函数
            /*            changeWeather=function() {
                           const isHot = this.state.isHot
                           this.setState({ isHot: !isHot })
                       } */
            // 箭头函数自身没有this指向，写this不会报错，会默认使用他外层是的this指向作为自己的this指向，可以在箭头函数中log一下this的指向
            // 自定义方法——要用赋值语句的形式加箭头函数
            changeWeather = ()=> {
                console.log(this);
                const isHot = this.state.isHot
                this.setState({ isHot: !isHot })
            }

        }
        //2.渲染组件到页面
        ReactDOM.render(<Weather />, document.getElementById("test"))
     /*
                 执行了ReactDOM.render(<Demo/>,document.getElementById("test"))之后会发生什么
             1.react解析组件标签，找到了MyComponent组件。
             2.发现组件的使用类定义的，随后new出来该类的实例，并通过实例调用到原型的render方法。
             3.将render返回的虚拟DOM转为真实dom，随后呈现在页面中。
             */
    </script>
</body>

</html>
```

> 1.  箭头函数自身没有this指向，写this不会报错，会默认使用他外层是的this指向作为自己的this指向，可以在箭头函数中log一下this的指向
> 2.  类中可以直接写赋值语句,不用let，类中不能随便写代码，如下代码的含义是，给car的实例对象添加一个属性，名为a，值为1。但值从外部传，则必须从写构造器接，如果写死则直接写在类里面以赋值语句形式。

### 总结

#### 理解

#### 强烈注意

1. 组件中render方法中的this为组件实例对象。
2. 组件自定义的方法中this为undefined，如何解决？

> a.强制绑定this：通过函数对象的bind()
>
> b.箭头函数

​	3.状态数据，不能直接修改或者跟新。

