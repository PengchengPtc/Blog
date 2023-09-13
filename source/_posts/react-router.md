---
title: react-router
date: 2021-10-31 22:26:20
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

# react-router

### Router原理

1. 历史
2. 跳转
3. 事件

### 常见的Router

1. 页面Router

   > 页面跳转，页面重新加载，回退也是页面重新加载。
   >
   > ```js
   > window.location.herf = "http://www.baidu.com"
   > history.back()
   > ```

2. Hash Router

   > 只有路由的哈希值在变化，只是状态改变，页面不会刷新。
   >
   > ```js
   > window.location.herf = "#hash"
   > window.hashchange = function() {
   > 	console.log("current hash",window.location.hash)
   > }
   > ```
   >
   > 

3. H5 Router

   > 功能路由和hash路由是一样的，只是hash路由只能操作hash，h5路由既能操作hash，又能操作路径，只是兼容性差。
   >
   > ```js
   > history.pushState("name","title","/path");
   > history.replaceState('name','title','path')
   > window.onpopstate = function() {
   >  console.log(window.loaction.href)
   >  console.log(window.location.pathname)
   >  console.log(window.location.hash)
   >  console.log(window.loaction.search)
   > }
   > ```

### React-Router

> react提供的路由，只用使用api。
>
> 动态路由，可以和组件用在一起。

#### 一些组件

- <BrowerRouter></HashRouter>,路由方式，页面路由和哈希路由
- <Route>,路由规则
- <Switch>,路由选项
- <Link/>/<NavLink>,跳转导航
- <Redirect>,自动跳转

### 安装

> 只需要安装react-router-dom

```bash
yarn add react-router-dom@4.2.2
```

### react-router的基本使用

```js
// 创建"外壳"组件App
// {compenent}是单独暴露,而非react的解构赋值
import React, { Component } from "react"
import { HashRouter as Router, Route,Link } from 'react-router-dom'



class A extends Component {
  render() {
    return (
      <div>
        Component A
      </div>
    )
  }
}


class B extends Component {
  render() {
    return (
      <div>
        Component B
      </div>
    )
  }
}



class Wrapper extends Component {
  render() {
    return (
      <div>
        <Link to="/a">组件A</Link>
        <br/>
        <Link to="/b">组件B</Link>
        {this.props.children}
      </div>
    )
  }
}




// import Welcome from "./components/Welcome"
// 创建并暴露App组件
export default class App extends Component {
  render() {
    return (
      <div>
        <Router>
          <Wrapper>
            <Route path="/a" component={A}>
              <A />
            </Route>
            <Route path="/b" component={B}>
              <B />
            </Route>
          </Wrapper>
        </Router>
      </div>
    )
  }
}

```

[![Ipi8J0.png](https://z3.ax1x.com/2021/10/31/Ipi8J0.png)](https://imgtu.com/i/Ipi8J0)

[![IpisW6.md.png](https://z3.ax1x.com/2021/10/31/IpisW6.md.png)](https://imgtu.com/i/IpisW6)

### 传参

```js
// 创建"外壳"组件App
// {compenent}是单独暴露,而非react的解构赋值
import React, { Component } from "react"
import { BrowserRouter as Router, Switch, Route, Link } from 'react-router-dom'



class A extends Component {
  render() {
    return (
      <div>
        Component A
        <Switch>
          {/* /a/123他会提取a，识别到a就跳转   exact是精准匹配，path是不完全匹配，所以带参数他也匹配到第一条，一般统配的放在后面 */}
          <Route exact path={`${this.props.match.path}`} render={(route) => {
            return <div>当前组件是不带参数的A</div>
          }} />
          {/* 真子路径 */}
          <Route path={`${this.props.match.path}/sub`} render={(route) => {
            return <div>当前组件是带参数的Sub</div>
          }} />
          {/* 传参 */}
          <Route path={`${this.props.match.path}/:id`} render={(route) => {
            return <div>当前组件是带参数的A,参数是{route.match.params.id}</div>
          }} />

        </Switch>
      </div>
    )
  }
}


class B extends Component {
  render() {
    return (
      <div>
        Component B
      </div>
    )
  }
}



class Wrapper extends Component {
  render() {
    return (
      <div>
        <Link to="/a">组件A</Link>
        <br />
        <Link to="/a/123">带参数的组件A</Link>
        <br />
        <Link to="/b">组件B</Link>
        <br />
        <Link to="/a/sub">子组件Asub</Link>
        {this.props.children}
      </div>
    )
  }
}




// import Welcome from "./components/Welcome"
// 创建并暴露App组件
export default class App extends Component {
  render() {
    return (
      <div>
        <Router>
          <Wrapper>
            <Route path="/a" component={A}>
              <A />
            </Route>
            <Route path="/b" component={B}>
              <B />
            </Route>
          </Wrapper>
        </Router>
      </div>
    )
  }
}




```

[![Ipk7qg.png](https://z3.ax1x.com/2021/10/31/Ipk7qg.png)](https://imgtu.com/i/Ipk7qg)

[![IpkXin.png](https://z3.ax1x.com/2021/10/31/IpkXin.png)](https://imgtu.com/i/IpkXin)

