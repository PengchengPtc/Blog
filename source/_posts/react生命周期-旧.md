---
title: react生命周期(旧)
date: 2021-10-25 16:08:59
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

# React生命周期

### 概述

1. 组件从创建到死亡它会经历一些特定的阶段
2. React组件中包含一系列勾子函数(生命周期函数)，会在特定时刻调用。
3. 我们在定义组件时，会在特定的生命周期回调函数中，给特定的工作。

> 生命周期回调函数<=>生命周期钩子函数<=>生命周期函数<=>生命周期钩子。
>
> 生命周期回调就是，react会在不同的生命周期帮你掉生命周期函数，例如react.render()。
>
> 生命周期钩子，就是到合适的生命周期，把他勾出来调用。

### 准备

> 每一次更新状态，render()就会被调一次，加初始化的一次，一共n+1次，n是改变状态的次数。

### 例子

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
            state = { opacity: 1 }
            death = () => {
                // 卸载组件
                ReactDOM.unmountComponentAtNode(document.getElementById("test"))
            }
            action = () => {
                setInterval(() => {
                    // 获取原状态
                    let { opacity } = this.state
                    //减小0.1
                    opacity -= 0.1
                    if (opacity <= 0) opacity = 1
                    //设置新的透明度
                    // this.setState({opacity:opacity})
                    this.setState({ opacity })
                }, 200)
            }
            //组件挂完毕后
            componentDidMount() {
                this.timer =    setInterval(() => {
                    // 获取原状态
                    let { opacity } = this.state
                    //减小0.1
                    opacity -= 0.1
                    if (opacity <= 0) opacity = 1
                    //设置新的透明度
                    // this.setState({opacity:opacity})
                    this.setState({ opacity })
                }, 200)
            }
            //组件将要卸载
            componentWillUnmount() {
                //情空定时器
                clearInterval(this.timer)
            }
            //初始化渲染、状态跟新之后
            render() {
                // 以下是jsx，后会被转换为html，被babel转
                console.log("@");
                return (    
                    <div>
                        <h2 style={{ opacity: this.state.opacity }}>React学不会怎么办？</h2>
                        <button onClick={this.death}>不活了</button>
                        <button onClick={this.action}>开始变化</button>
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

### 常见错误

[![5hBBp6.png](https://z3.ax1x.com/2021/10/25/5hBBp6.png)](https://imgtu.com/i/5hBBp6)

> 1.组件被卸载了，无法跟新状态。
>
> 2.所以上面的例子，得清空定时器。

### 生命周期勾子(旧)

[![5hyUKK.png](https://z3.ax1x.com/2021/10/25/5hyUKK.png)](https://imgtu.com/i/5hyUKK)

#### 演示setState()和forceUpdate()

```js
   class Count extends React.Component {
            // 构造器
            constructor(props) {
                console.log("count-constructor");
                super(props)
                // 初始化状态
                this.state = { count: 0 }
            }
            state = { count: 0 }
            add = () => {
                // 获取原状态
                const { count } = this.state
                //跟新状态
                this.setState({ count: count + 1 })

            }
            death = () => {
                ReactDOM.unmountComponentAtNode(document.getElementById("test"))
            }
            // 强制更新状态
            force = () => {
                this.forceUpdate()
            }
            // 组件将要挂载的勾子
            componentWillMount() {
                console.log("count-componentWillMount");
            }
            //组件挂完毕后的勾子
            componentDidMount() {
                console.log("count-componentDidMount");
            }
            //组件将要卸载的钩子
            componentWillUnmount() {
                console.log("count-componentWillUnmount");
            }
            //控制组件跟新的"阀门",不写react自己生成且返回一个值为真，如果写上，则需要手动写返回值，且为布尔值，true打开，false关闭
            shouldComponentUpdate() {
                console.log("count-shouldComponentUpdate");
                return true
            }
            //组件将要跟新的钩子
            componentWillUpdate() {
                console.log("count-componentWillUpdate");
            }
            //组件跟新完毕的钩子
            componentDidUpdate() {
                console.log("count-componentDidUpdate");
            }
            //初始化渲染、状态跟新之后
            render() {
                // 以下是jsx，后会被转换为html，被babel转
                const { count } = this.state
                console.log("count-render");
                return (
                    <div>
                        <h2>当前求和为{count}</h2>
                        <button onClick={this.add}>点我加一</button>
                        <button onClick={this.death}>点我卸载</button>
                        <button onClick={this.force}>不更改任何状态中的数据，强制更新一下</button>
                    </div>
                )
            }
        }
ReactDOM.render(<Count />, document.getElementById("test"))
```

### 演示父组件

```js
    class A extends React.Component {
            // 初始化状态
            state = {carName:"奔驰"}
            changeCar = () => {
                this.setState({carName:"奥托"})
            }
            render() {
                return (
                    <div>
                        <div>我是a组件</div>
                        <button onClick={this.changeCar}>换车</button>
                        <B carName={this.state.carName} />
                    </div>
                )
            }
        }
        class B extends React.Component {
            //第一次接受的props不调用
            componentWillReceiveProps(props) {
                console.log("B-componentWillReceiveProps",props);
            }
            shouldComponentUpdate() {
                console.log("B-shouldComponentUpdate");
                return true
            }
            //组件将要跟新的钩子
            componentWillUpdate() {
                console.log("B-componentWillUpdate");
            }
            //组件跟新完毕的钩子
            componentDidUpdate() { 
                console.log("B-componentDidUpdate");
            }
            render() {
                console.log("B-render");
                return (
                    <div>我是B组件，接受到的车是：{this.props.carName}</div>
                )
            }
        }
        //2.渲染组件到页面
        ReactDOM.render(<A />, document.getElementById("test"))
```

### 总结(旧)

点击图片查看

> [![5hhIgJ.png](https://z3.ax1x.com/2021/10/25/5hhIgJ.png)](https://imgtu.com/i/5hhIgJ)

