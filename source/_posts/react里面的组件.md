---
title: react里面的组件
date: 2021-09-22 00:05:02
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

# 类式组件

## react中的组件

### 函数组件

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
      //1.创建函数式组件
       function MyComponent() {
           console.log(this); //此处的this是undefined，因为babel编译后开启了严格模式
           return <h2>我是用函数定义的组件(适用于【简单组件】的定义)</h2>
       }
       //2.渲染组件到页面
       ReactDOM.render(<MyComponent/>,document.getElementById("test"))
       /*
        执行了ReactDOM.render(<Demo/>,document.getElementById("test"))之后会发生什么
            1.react解析组件标签，找到了MyComponent组件。
            2.发现组件是使用函数定义的，随后调用函数，将返回的虚拟dom转为真实dom，随后呈现再页面中。
       */
    </script>
</body>

</html>
```

### 类式组件

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
        class MyComponent extends React.Component {
            //构造器不用写，直接继承，但render必须写
            render() {
                //render是放在哪里的？ --- 类的原型对象上，供实例使用。
                //render中的this是谁？---- MyComponent的实例对象。
                console.log("redner中的this",this);
                return <h2>我是用类定义的组件(适用于【复杂组件】的定义</h2>
            }
        }
        //2.渲染组件到页面
        // 上面一个render和下面一个render不是一个东西
        ReactDOM.render(<MyComponent/>,document.getElementById("test"))
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

