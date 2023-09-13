---
title: react高级函数和函数柯里化
date: 2021-10-24 23:15:43
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

# react高级函数_函数柯里化

### 概述

> 高阶函数：如果一个函数符合下面两个规范中的任何一个，那么该函数就是高阶函数。
>
> ​	 1.若A函数，接收到的参数是一个函数，那么A就可以称之为高级函数。
>
> ​	  2.若A函数，调用的返回值依然是一个函数，那么a就可以称之为高阶函数。
>
> ​		常见的高级函数：Promise，settimeout符合第一种，arr.map()
>
> 函数柯里化：通过函数调用继续返回函数的方式，实现多次接受参数最后统一处理的函数编码形式。

### react函数柯里化

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
            saveFormData = (dataType) => {
                return (event)=>{
                this.setState({[dataType]:event.target.value})
                console.log(this.state);
            }
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
                        用户名： <input onChange={this.saveFormData('username')} type="text" name="username" />
                        密码:   <input onChange={this.saveFormData('password')} type="password" name="password" />
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

> 1.onClick(this.saveFormData()),意思是回调this.saveFormData()函数,是onclick调
>
> 2.onClick(this.saveFormData("username")),意思是回调saveFormData("username")自己调用后的返回的结果，其实onClick调用的是saveFormData("username")返回的结果
>
> 3.如果this.saveFormData("username")把定义为上面所写的函数，则表示OnClick调用的是上面的那个箭头函数，所以event要写在箭头函数的形参里面，而saveFormData()接的参数是调用时候写的“username”
>
> 4.相当于闭包

### 不用函数柯里化

> 直接回调一个箭头函数，箭头函数里面调用改变状态函数。

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
            saveFormData = (dataType,event) => {
                this.setState({[dataType]:event.target.value})
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
                        用户名： <input onChange={event => this.saveFormData("username",event)} type="text" name="username" />
                        密码:   <input onChange={event => this.saveFormData("password",event)} type="password" name="password" />
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

