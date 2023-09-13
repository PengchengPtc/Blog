---
title: react的事件处理
date: 2021-10-24 23:15:14
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

# react的事件处理

### 概述

> 1)通过onXxxx属性指定事件处理函数(注意大小写)。
>
> ​	a.React使用的是自定义(合成)事件，而不是使用原生DOM事件。    ——为了更好的兼容性
>
> ​	b.React中的事件是通过事件委托方式处理的(委托给组件最外层的元素)。    ——为了高效
>
> 2)通过event.target得到发生事件的DOM元素对象。     ————不要过度使用ref

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
            //创建ref容器
            myRef = React.createRef()
            myRef2 = React.createRef()

            //展示左侧输入框的内容
            showData = () => {
                alert(this.myRef.current.value);
            }

            //展示右侧输入框的数据
            showData2 = (event) => {
                alert(event.target.value);
            }

            render() {
                // 以下是jsx，后会被转换为html，被babel转
                return (
                    <div>
                        <input ref={this.myRef} type="text" placeholder="点击按钮提示数据" /> &nbsp;
                        <button onClick={this.showData}>点我提示左侧的数据</button> &nbsp;
                        <input  onBlur={this.showData2} type="text" placeholder="点击按钮提示数据" />
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

