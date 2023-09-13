---
title: 原生js的点击事件及react点击事件
date: 2021-09-22 00:01:15
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: JS
tags:
	- JS
---

### 原生js点击事件

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

    <button id='btn1'>按钮1</button>
    <button id='btn2'>按钮2</button>
    <button onclick="demo()">按钮3</button>

    <script type="text/javascript">
    // 方法一
        // 拿到dom
        const btn1 = document.getElementById('btn1')
        console.log(btn1);
        // 操作dom
        btn1.addEventListener('click', () => {
            alert("按钮1被点击了")
        })
    
    //方法二
        // 拿到dom
        const btn2 = document.getElementById('btn2')
        // 操作dom
        btn2.onclick = () => {
            alert('按钮2被点击了')
        }
    
    // 方法三,react推荐方法
        function demo() {
            alert("按钮3被点击了")
        }
    </script>
</body>

</html>
```



### react点击事件

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
        //1.创建类式组件,是继承react里面内置的一个类
        class Weather extends React.Component {
            constructor(props) {
                super(props)
                this.state = { isHot: false, wind: "微风" }
            }
            //构造器可以不用写，直接继承，但render必须写
            render() {
                //render是放在哪里的？ --- 类的原型对象上，供实例使用。
                //render中的this是谁？---- MyComponent的实例对象。
                console.log("redner中的this", this);
                // 解构赋值
                const { isHot } = this.state
                // react中onclik中c要大写,且函数名不能是字符串，要读出demo得用{}，且吧demo()去掉，demo交给onclick回调，加括号就相当于直接被调用了
                return <h2 onClick={demo}>今天天气很{isHot ? "炎热" : "凉爽"}</h2>
            }
        }
        //2.渲染组件到页面
        // 上面一个render和下面一个render不是一个东西
        ReactDOM.render(<Weather />, document.getElementById("test"))

        function demo() {
            alert("标题被点击了")
        }

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

