---
title: react组件实例里面属性之props
date: 2021-09-22 23:18:57
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: React
tags:
	- React
---

# 组件实例的三大核心属性  1.props (类组件)

### 概述：

state只能在组件内部传值，修改，是一个统一修改，而在想从一个个传值对每个实例进行修改就要用 到props。

### 基本使用

代码：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <!-- 准备好一个“容器” -->
    <div id="test1">

    </div>
    <div id="test2">

    </div>
    <div id="test3">

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
        // 1.创建类式组件
        class Person extends React.Component {
            render() {
                console.log(this);
                // const { isHot, wind } = this.state
                const {name,sex,age} = this.props
                return (
                    <ul>
                        <li>姓名:{name}</li>
                        <li>性别:{sex}</li>
                        <li>年龄:{age}</li>
                    </ul>
                )
            }
        }
        //2.渲染组件到页面
        ReactDOM.render(<Person name = 'tom' age = '18' sex= '女'/>, document.getElementById("test1"))
        ReactDOM.render(<Person name = 'sarara' age = '17' sex= '女'/>, document.getElementById("test2"))
        ReactDOM.render(<Person name = 'jom' age = '16' sex= '男'/>, document.getElementById("test3"))
    </script>
</body>

</html>
```

### 组合传值和限制传值规则

> 1. 原生js虽然不能展开运算符不能展开对象，但babel加react下，能展开对象，且只针对组件传值，{}是为了显示表达式。
> 2. Person.propTypes限制类型和必要性，Person.defaultPorps限制默认值。
> 3. props是只读，不能修改。

代码：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <!-- 准备好一个“容器” -->
    <div id="test1">

    </div>
    <div id="test2">

    </div>
    <div id="test3">

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
        class Person extends React.Component {
            render() {
                console.log(this);
                // const { isHot, wind } = this.state
                const {name,sex,age} = this.props
                //props是只读的
                //this.props.name = 'jack' //此行代码会报错，因为props是只读的
                return (
                    <ul>
                        <li>姓名:{name}</li>
                        <li>性别:{sex}</li>
                        <li>年龄:{age}</li>
                    </ul>
                )
            }
        }
        // 对props传的值做限制,对标签属性进行类型、必要性的限制
        Person.propTypes = {
            name:PropTypes.string.isRequired ,  //限制name必填，且为字符串
            sex: PropTypes.string,              //限制sex为字符串
            age: PropTypes.number,              //限制age为数值
            speak: PropTypes.func               //限制speak为函数
        }
        // 如果不传，则默认传值如下，指定默认标签属性值
        Person.defaultProps = {
            sex:"不男不女",
            age:18
        }
        //2.渲染组件到页面
        ReactDOM.render(<Person name = 'tom' age = {18} sex= '女' speak = {speak}/>, document.getElementById("test1"))
        ReactDOM.render(<Person name = 'sarara' age = {17} sex= '女'/>, document.getElementById("test2"))

        const p = {name:"老刘",age:18,sex:'女'}

        // ReactDOM.render(<Person name = 'jom' age = '16' sex= '男'/>, document.getElementById("test3"))
        // 此处注意，原生js虽然不能展开运算符不能展开对象，但babel加react下，能展开对象，且只针对组件传值
        ReactDOM.render(<Person {...p} />, document.getElementById("test3"))

        function speak() {
            console.log("我说话了");
        }
    </script>
</body>

</html>
```

### props简写方式

> person的属性可以放到类里面，作为类自身的属性。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <!-- 准备好一个“容器” -->
    <div id="test1">

    </div>
    <div id="test2">

    </div>
    <div id="test3">

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
        class Person extends React.Component {
            // static是给类自身加属性
            // 对props传的值做限制,对标签属性进行类型、必要性的限制
            static propTypes = {
                name: PropTypes.string.isRequired,  //限制name必填，且为字符串
                sex: PropTypes.string,              //限制sex为字符串
                age: PropTypes.number,              //限制age为数值
                speak: PropTypes.func               //限制speak为函数
            }
            // 如果不传，则默认传值如下，指定默认标签属性值
            static defaultProps = {
                sex: "不男不女",
                age: 18
            }
            render() {
                // this指向react的实例对象，下面创建了三个实例对象，所以打印三遍this。
                console.log(this);
                // const { isHot, wind } = this.state
                const { name, sex, age } = this.props
                return (
                    <ul>
                        <li>姓名:{name}</li>
                        <li>性别:{sex}</li>
                        <li>年龄:{age}</li>
                    </ul>
                )
            }
        }

        //2.渲染组件到页面
        ReactDOM.render(<Person name='tom' age={18} sex='女' speak={speak} />, document.getElementById("test1"))
        ReactDOM.render(<Person name='sarara' age={17} sex='女' />, document.getElementById("test2"))

        const p = { name: "老刘", age: 18, sex: '女' }

        // ReactDOM.render(<Person name = 'jom' age = '16' sex= '男'/>, document.getElementById("test3"))
        // 此处注意，原生js虽然不能展开运算符不能展开对象，但babel加react下，能展开对象，且只针对组件传值
        ReactDOM.render(<Person {...p} />, document.getElementById("test3"))

        function speak() {
            console.log("我说话了");
        }
    </script>
</body>

</html>
```

### 类式组件中的构造器与props

> 构造器是否接受props，是否传递super，取决于：是否希望在构造器中通过this访问props。
>
> 构造器一般可省略。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <!-- 准备好一个“容器” -->
    <div id="test1">
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
        class Person extends React.Component {
            //构造器是否接受props，是否传递super，取决于：是否希望在构造器中通过this访问props
            constructor(props) {
                // console.log(props);
                super(props)
                console.log("constructor",this.props);
            }
            // static是给类自身加属性
            // 对props传的值做限制,对标签属性进行类型、必要性的限制
            static propTypes = {
                name: PropTypes.string.isRequired,  //限制name必填，且为字符串
                sex: PropTypes.string,              //限制sex为字符串
                age: PropTypes.number,              //限制age为数值
                speak: PropTypes.func               //限制speak为函数
            }
            // 如果不传，则默认传值如下，指定默认标签属性值
            static defaultProps = {
                sex: "男",
                age: 18
            }
            render() {
                // this指向react的实例对象，下面创建了三个实例对象，所以打印三遍this。
                console.log(this);
                // const { isHot, wind } = this.state
                const { name, sex, age } = this.props
                return (
                    <ul>
                        <li>姓名:{name}</li>
                        <li>性别:{sex}</li>
                        <li>年龄:{age}</li>
                    </ul>
                )
            }
        }

        //2.渲染组件到页面
        ReactDOM.render(<Person name='jerry'/>, document.getElementById("test1"))
    </script>
</body>

</html>

```

### 函数式组件使用props

> 1.之前说的组件的三大属性针对的是实例，函数没有实例，没有this，故不能使用stata，refs
>
> 2.但函数可以传递参数，可以使用props

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <!-- 准备好一个“容器” -->
    <div id="test1">
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
        // class Person extends React.Component {
        //     // static是给类自身加属性
        //     // 对props传的值做限制,对标签属性进行类型、必要性的限制
        //     static propTypes = {
        //         name: PropTypes.string.isRequired,  //限制name必填，且为字符串
        //         sex: PropTypes.string,              //限制sex为字符串
        //         age: PropTypes.number,              //限制age为数值
        //         speak: PropTypes.func               //限制speak为函数
        //     }
        //     // 如果不传，则默认传值如下，指定默认标签属性值
        //     static defaultProps = {
        //         sex: "男",
        //         age: 18
        //     }
        //     render() {
        //         // this指向react的实例对象，下面创建了三个实例对象，所以打印三遍this。
        //         console.log(this);
        //         // const { isHot, wind } = this.state
        //         const { name, sex, age } = this.props
        //         return (
        //             <ul>
        //                 <li>姓名:{name}</li>
        //                 <li>性别:{sex}</li>
        //                 <li>年龄:{age}</li>
        //             </ul>
        //         )
        //     }
        // }
        // 创建函数式组件,函数组件没有this
        function Person(props) {
            console.log(props);
            const {name,sex,age} = props
            return (
                <ul>
                        <li>姓名:{name}</li>
                        <li>性别:{sex}</li>
                        <li>年龄:{age}</li>
                    </ul>
            )
        }
         // 对props传的值做限制,对标签属性进行类型、必要性的限制
         Person.propTypes = {
            name:PropTypes.string.isRequired ,  //限制name必填，且为字符串
            sex: PropTypes.string,              //限制sex为字符串
            age: PropTypes.number,              //限制age为数值
            speak: PropTypes.func               //限制speak为函数
        }
        // 如果不传，则默认传值如下，指定默认标签属性值
        Person.defaultProps = {
            sex:"不男不女",
            age:18
        }
        //2.渲染组件到页面
        ReactDOM.render(<Person name='jerry'/>, document.getElementById("test1"))
    </script>
</body>
</html>
```

### 总结

> 1.限制
>
> 2.默认值
>
> 3.简写是从类的外侧移到类的里侧
>
> 4.作用
>
> 1）通过标签属性从组件外向组件传递变化值。
>
> 2）注意组件内部不要修改props数据。

