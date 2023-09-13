---
title: react组件实例的属性ref
date: 2021-10-24 23:13:30
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

# 组件实例的三大核心属性  1.ref(类组件)

### 概述

> 1.组件内的标签可以定义ref属性来标识自己。
>
> 2.标识用ref，生成的属性是ref。

### 原生的id到ref

原生id:

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
    <!-- 引入proptypes,用于对组件标签属性进行限制-->
    <script type="text/javascript" src="../js/prop-types.js"></script>
    <!-- 下面写babel表示写的是jsx，而不是js，而且用babel来翻译，此处必须写babel -->
    <script type="text/babel">
        // 1.创建类式组件
        class Demo extends React.Component {
            //展示左侧输入框的内容
            showData = () =>{
                const input = document.getElementById("input1")
                alert(input.value)
            }
            render() {
                return (
                   <div>
                    <input id= "input1" type="text" placeholder ="点击按钮提示数据" /> &nbsp;
                    <button onClick={this.showData}>点我提示左侧的数据</button> &nbsp;
                    <input type="text" placeholder ="点击按钮提示数据" />
                    </div>
                )
            }
        }

        //2.渲染组件到页面
        ReactDOM.render(<Demo/>, document.getElementById("test"))
    </script>
</body>

</html>

```

> 字符串形式的ref，ref是针对react设计的，id则是原生的。

### 字符串形式ref

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
    <!-- 引入proptypes,用于对组件标签属性进行限制-->
    <script type="text/javascript" src="../js/prop-types.js"></script>
    <!-- 下面写babel表示写的是jsx，而不是js，而且用babel来翻译，此处必须写babel -->
    <script type="text/babel">
        // 1.创建类式组件
        class Demo extends React.Component {
            //展示左侧输入框的内容
            showData = () => {
                //  this的指向是Demo的实例对象，因为组件创建的函数只能供实例对象调用，this是谁调用指向谁
                const { input1 } = this.refs
                alert(input1.value)
                console.log(this)
            }
            showData2 = () => {
                const { input2 } = this.refs
                alert(input2.value)
            }
            render() {
                // 以下是jsx，后会被转换为html，被babel转
                return (
                    <div>
                        <input ref="input1" type="text" placeholder="点击按钮提示数据" /> &nbsp;
                        <button onClick={this.showData}>点我提示左侧的数据</button> &nbsp;
                        <input ref="input2" onBlur={this.showData2} type="text" placeholder="点击按钮提示数据" />
                    </div>
                )
            }
        }
        //2.渲染组件到页面
        ReactDOM.render(<Demo />, document.getElementById("test"))
    </script>
</body>
</html>
```

> 1.ref去标识标签，在属性中以refs形式显示
>
> 2.onClik和onBulr是react自己封装的一套

### 回调形式的ref

> 1.字符串的ref存在一些效率上的问题，可能会在未来的版本移除。
>
> 2.所谓回调函数，就是自己定义的函数，自己没调用，被其他调用。
>
> 3.注意回调函数，你只需要定义在那，至于调用，不用管，react会帮你调用。
>
> 4.不仅仅调用了，还把当前节点传进回调函数里面。

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
    <!-- 引入proptypes,用于对组件标签属性进行限制-->
    <script type="text/javascript" src="../js/prop-types.js"></script>
    <!-- 下面写babel表示写的是jsx，而不是js，而且用babel来翻译，此处必须写babel -->
    <script type="text/babel">
        // 1.创建类式组件
        class Demo extends React.Component {
            //展示左侧输入框的内容
            showData = () => {
                //  this的指向是Demo的实例对象，因为组件创建的函数只能供实例对象调用，this是谁调用指向谁
                const { input1 } = this
                alert(input1.value)
                console.log(this)
            }
            showData2 = () => {
                const { input2 } = this
                alert(input2.value)
            }
            render() {
                // 以下是jsx，后会被转换为html，被babel转
                return (
                    <div>
                        <input ref={(c) =>{console.log(c);this.input1 = c}} type="text" placeholder="点击按钮提示数据" /> &nbsp;
                        <button onClick={this.showData}>点我提示左侧的数据</button> &nbsp;
                        <input ref={(c) => this.input2 = c} onBlur={this.showData2} type="text" placeholder="点击按钮提示数据" />
                    </div>
                )
            }
        }
        //2.渲染组件到页面
        ReactDOM.render(<Demo />, document.getElementById("test"))
    </script>
</body>
</html>
```

### 回调ref中调用次数的问题

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
    <!-- 引入proptypes,用于对组件标签属性进行限制-->
    <script type="text/javascript" src="../js/prop-types.js"></script>
    <!-- 下面写babel表示写的是jsx，而不是js，而且用babel来翻译，此处必须写babel -->
    <script type="text/babel">
        // 1.创建类式组件
        class Demo extends React.Component {
            state = {isHot:false}
            showData = () => {
                const {input1} = this
                alert(input1.value)
            }
            //展示左侧输入框的内容
            changeWeather = () => {
                // 获取原来的状态
                const {isHot} = this.state
                // 更新状态
                this.setState({isHot:!isHot})
            }
            saveInput = (c) => {
               this.input1 = c;
               console.log("@",c);
            }
            render() {
                const {isHot} = this.state
                // 以下是jsx，后会被转换为html，被babel转
                return (
                    <div>
                        <h2>今天天气很热{isHot ?"炎热":"凉快"}</h2>
                        {/*jsx里面的注释要先加{}，{}里面可以写js，再用js的注释方法注释*/}
                        {/*<input ref={(c) =>{console.log(c);this.input1 = c}} type="text" placeholder="点击按钮提示数据" /> &nbsp;*/}
                        <input ref={this.saveInput}  type="text" placeholder="点击按钮提示数据" /><br/><br/>
                        <button onClick={this.showData}>点我提示左侧的数据</button> 
                        <button onClick={this.changeWeather}>点我切换天气</button>
                    </div>
                )
            }
        }
        //2.渲染组件到页面
        ReactDOM.render(<Demo />, document.getElementById("test"))
    </script>
</body>
</html>
```

> 关于回调refs的说明
> 1.如果ref回调函数是以内联函数的方式定义的，在更新过程中它会被执行两次，第一次传入参数null，然后第二次会传入参数DOM元素。这是因为在每次渲染时会创建一个新的函数实例，所以React清空旧的ref并且设置新的。
>
> 2.通过将ref 的回调函数定义class的绑定函数的方式可以避免上述问颗,但是大多数情况下它是无关紧要的。
>
> 3.更新过程，相当于更新状态，如果用内联的方式写，跟新状态后，reder()会被调两次，因为有第一次初始化，因为跟新后react任务他是新函数，古返回为null，而通过绑定函数形式写，因为是挂在实例对象上的，所以他知道之前调用过，不打印null。
>
> 4.jsx注释，不能直接注释，需要{}，{}里面可以用js注释，用js的注释方法，{/**/}。

### createRef的使用

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
    <!-- 引入proptypes,用于对组件标签属性进行限制-->
    <script type="text/javascript" src="../js/prop-types.js"></script>
    <!-- 下面写babel表示写的是jsx，而不是js，而且用babel来翻译，此处必须写babel -->
    <script type="text/babel">
        // 1.创建类式组件
        class Demo extends React.Component {
            /*
                React.createRef调用后可以返回一个容器，该容器可以存储ref所标识的节点，该容器是“专人专用”
            */
           myRef = React.createRef()
           myRef2 = React.createRef()
            //展示左侧输入框的内容
            showData = () => {
                //  this的指向是Demo的实例对象，因为组件创建的函数只能供实例对象调用，this是谁调用指向谁
                alert(this.myRef.current.value);
            }
            showData2 = () => {
                alert(this.myRef2.current.value);
            }
            render() {
                // 以下是jsx，后会被转换为html，被babel转
                return (
                    <div>
                        <input ref={this.myRef} type="text" placeholder="点击按钮提示数据" /> &nbsp;
                        <button onClick={this.showData}>点我提示左侧的数据</button> &nbsp;
                        <input ref={this.myRef2} onBlur={this.showData2} type="text" placeholder="点击按钮提示数据" />
                    </div>
                )
            }
        }
        //2.渲染组件到页面
        ReactDOM.render(<Demo />, document.getElementById("test"))
    </script>
</body>
</html>
```

>  React.createRef调用后可以返回一个容器,然而每返回一个容器，只能装一个refs。

### 总结

> 开发一般使用内联的写法，出问题也无关紧要。
>
> 推荐使用最麻烦的reateRef的写法。

