---
title: react一个hello组件
date: 2021-10-28 14:06:18
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

# Hello react

app.js文件

```js
// 创建"外壳"组件App
// {compenent}是单独暴露,而非react的解构赋值
import React,{Component} from "react"

class App extends Component{
  render() {
    return (
      <div>
        hello react
      </div>
    )
  }
}



export default App;

```

> {compenent}是单独暴露,而非react的解构赋值
>
> react用了多种暴露的形式如下所示：
>
> module.js
>
> ```js
> const React = {1,2,3}
> export class Component {
> 
> }
> React.Component = Component
> export default React
> ```
>
> 用分别暴露的形式暴露Component
>
> 其实也可以这样再app.js引入
>
> ```js
> import React from './moudles.js'
> const {Component} = React
> console.log(new Component())
> ```

index.js文件

```js
// 引入react核心库
import React from 'react';
// 引入ReactDom
import ReactDOM from 'react-dom';
import './index.css';
// 引入app组件
import App from './App';
// 引入性能检测的库
import reportWebVitals from './reportWebVitals';

ReactDOM.render(
  //外面的标签能帮我们检查代码
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();

```

### 简化后

目录机构:

[![5qRgl6.png](https://z3.ax1x.com/2021/10/28/5qRgl6.png)](https://imgtu.com/i/5qRgl6)

Hello文件中的index.jsx即是组件

```jsx
import React,{Component} from "react"
import './index.css'
// 创建并暴露App组件
export default class Hello extends Component{
  render() {
    return <h2 className="title">Hello,React!</h2>
  }
}

```

对应样式

```css
.title{
    background-color: orange;
}
```

### 效果

[![5qWeAJ.png](https://z3.ax1x.com/2021/10/28/5qWeAJ.png)](https://imgtu.com/i/5qWeAJ)
