---
title: react生命周期(新)
date: 2021-10-25 16:09:17
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

# react生命周期(新)

### 区别

> 即将废弃两个，新加两个
>
> [![5hzAIg.png](https://z3.ax1x.com/2021/10/25/5hzAIg.png)](https://imgtu.com/i/5hzAIg)
>
> 废弃的需要加unsafe才可以使用
>
> [![5hz3oF.png](https://z3.ax1x.com/2021/10/25/5hz3oF.png)](https://imgtu.com/i/5hz3oF)

### 生命周期函数(新)

[![54etE9.png](https://z3.ax1x.com/2021/10/25/54etE9.png)](https://imgtu.com/i/54etE9)

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
    <script type="text/javascript" src="../js/17.1/react.development.js"></script>
    <!-- 引入react-dom，用于支持react操作dom -->
    <script type="text/javascript" src="../js/17.1/react-dom.development.js"></script>
    <!-- 引入babel，用于讲jsx转入为js -->
    <script type="text/javascript" src="../js/17.1/babel.min.js"></script>
    <!-- 引入proptypes,用于对组件标签属性进行限制-->
    <script type="text/javascript" src="../js/prop-types.js"></script>
    <!-- 下面写babel表示写的是jsx，而不是js，而且用babel来翻译，此处必须写babel -->
    <script type="text/babel">
        // 1.创建类式组件
  
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
            //组件跟新完毕的钩子,第三个是参数是快照，在跟新之前获取快照
            componentDidUpdate(preprops,prestate,Snapshot) {
                console.log("count-componentDidUpdate",preprops,prestate,Snapshot);
            }
            //若state的值在任何时候却决于props，那么可以使用getDerivedStateFromProps
            static  getDerivedStateFromProps(props,state) {
                console.log("getDerivedStateFromProps",props,state);
                // 返回状态对象，或者null
                return null
            }

            getSnapshotBeforeUpdate() {
                console.log("getSnapshotBeforeUpdate");
                return "guigu"
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
            UNSAFE_componentWillReceiveProps(props) {
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
        ReactDOM.render(<Count count={199}/>, document.getElementById("test"))
    </script>
</body>

</html>
```

### getSnapshotBeforeUpdate举例

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
    <style>
        .list {
            width: 200px;
            height: 150px;
            background-color: skyblue;
            /* 设置为滑动 */
            overflow: auto;
        }
        .news {
            height: 30px;
        }
    </style>
</head>

<body>
    <!-- 准备好一个容器 -->
    <div id="test"></div>
    <!-- 引入包，注意引入顺序 -->
    <!-- 引入react核心库 -->
    <script type="text/javascript" src="../js/17.1/react.development.js"></script>
    <!-- 引入react-dom，用于支持react操作dom -->
    <script type="text/javascript" src="../js/17.1/react-dom.development.js"></script>
    <!-- 引入babel，用于讲jsx转入为js -->
    <script type="text/javascript" src="../js/17.1/babel.min.js"></script>
    <!-- 引入proptypes,用于对组件标签属性进行限制-->
    <script type="text/javascript" src="../js/prop-types.js"></script>
    <!-- 下面写babel表示写的是jsx，而不是js，而且用babel来翻译，此处必须写babel -->
    <script type="text/babel">
        // 1.创建类式组件

        class NewsList extends React.Component {
           
            state = { newsArr: []}

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
            //组件挂完毕后的勾子
            componentDidMount() {
                console.log("count-componentDidMount");
                setInterval(() => {
                    //获取原状态
                    const {newsArr} = this.state
                    // 模拟一条新闻
                    const news = "新闻" +(newsArr.length+1)
                    // 跟新状态
                    this.setState({newsArr:[news,...newsArr]})
                }, 1000);
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
            //组件跟新完毕的钩子,第三个是参数是快照，在跟新之前获取快照
            componentDidUpdate(preprops, prestate, height) {
                // console.log("count-componentDidUpdate", preprops, prestate, Snapshot);
                this.refs.list.scrollTop += this.refs.list.scrollHeight - height
            }
            //若state的值在任何时候却决于props，那么可以使用getDerivedStateFromProps
            static getDerivedStateFromProps(props, state) {
                console.log("getDerivedStateFromProps", props, state);
                // 返回状态对象，或者null
                return null
            }

            getSnapshotBeforeUpdate() {
                return this.refs.list.scrollHeight
            }

            //初始化渲染、状态跟新之后
            render() {
                // 以下是jsx，后会被转换为html，被babel转
                const { count } = this.state
                console.log("count-render");
                return (
                    <div className="list" ref="list">
                       {
                           this.state.newsArr.map((n,index)=>{
                               return <div key={index} className="news">{n}</div>
                           })
                       }
                    </div>
                )
            }
        }

        class A extends React.Component {
            // 初始化状态
            state = { carName: "奔驰" }
            changeCar = () => {
                this.setState({ carName: "奥托" })
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
            UNSAFE_componentWillReceiveProps(props) {
                console.log("B-componentWillReceiveProps", props);
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
        ReactDOM.render(<NewsList />, document.getElementById("test"))
    </script>
</body>

</html>
```

### 总结

[![54mLee.png](https://z3.ax1x.com/2021/10/25/54mLee.png)](https://imgtu.com/i/54mLee)

[![54nFeg.png](https://z3.ax1x.com/2021/10/25/54nFeg.png)](https://imgtu.com/i/54nFeg)
