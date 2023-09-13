---
title: react非受控组件和受控组件
date: 2021-10-24 23:14:10
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

# react非受控组件和受控组件

### 非受控组件

> 现用现取

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
            handleSubmit = (event) => {
                event.preventDefault() //组织表单提交
                const {username,password} = this
                alert(`你输入的用户名：${username.value},你输入的密码：${password.value}`)
            }
            render() {
                // 以下是jsx，后会被转换为html，被babel转
                return (
                    <form onSubmit={this.handleSubmit}>
                        用户名：<input ref={c =>{this.username = c}} type="text" name="username" />
                        密码:  <input ref={c =>{this.password = c}} type="password" name="password" />
                        <button>登录</button>
                    </form>
                )
            }
        }
        //2.渲染组件到页面
        ReactDOM.render(<Demo />, document.getElementById("test"))
    </script>
</body>

</html>
```



### 受控组件

> 先存在状态里面，用的时候再取，类似于双向绑定。
>
> react里面没有双向绑定。
>
> 提交时候再取state里面的用户名和密码。

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
            state = {
                username:"",
                password:""
            }
            
            // 保存用户名到状态中
            saveUsername = (event) => {
                this.setState({username:event.target.value})
                console.log(this.state);
            }
            savePassword = (event) => {
                this.setState({password:event.target.value})
                console.log(this.state);
            }
            // 保存密码到状态中
            handleSubmit = (event) => {
                event.preventDefault() //组织表单提交
                const {username,password} = this.state
                alert(`你输入的用户名：${username.value},你输入的密码：${password.value}`)
            }
            render() {
                // 以下是jsx，后会被转换为html，被babel转
                return (
                    <form onSubmit={this.handleSubmit}>
                        用户名： <input onChange={this.saveUsername} type="text" name="username" />
                        密码:   <input onChange={this.savePassword} type="password" name="password" />
                        <button>登录</button>
                    </form>
                )
            }
        }
        //2.渲染组件到页面
        ReactDOM.render(<Demo />, document.getElementById("test"))
    </script>
</body>
</html>
```

