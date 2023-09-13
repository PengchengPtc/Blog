---
title: 类中的this指向问题
date: 2021-09-22 18:18:49
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: JS
tags:
     - JS
---

# 类中this指向问题

### 代码

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
    <script>
        class Person {
             constructor(name,age) {
                this.name = name
                this.age = age
             }
             study() {
            // study放在哪里?-- weather的原型对象上，供实例使用
            // 通过student实例调用study时，study中的this就是student实例
                 console.log(this);
             }
        }
        const p1 = new Person("tom",18)
        p1.study()   //通过实例调用speak方法,是可以拿到this的
        const x = p1.study
        x()          //此处函数属于直接调用,this按理说指向window，但类局部开了严格模式，让他不敢指向window


        // 实例一
        // 没有开启严格模式之前
        function demo() {
            console.log(this);
        }
        demo()
        // 开启严格模式后
        function demo2() {
            'use strict'
            console.log(this);
        }
        demo2()


        // 修改this指向
        function demo3() {
            console.log(this);
        }
        demo()
        const x = demo.bind({a:1,b:2})
        x()
    </script>
</body>
</html>
```

### 有明确调用者时，this指向调用者

看这个例子：

```javascript
var obj = {
  myName: "小小飞",
  func: function() {
    console.log(this.myName);
  }
}

obj.func();    // 小小飞
```

上述例子很好理解，因为调用者是obj，所以func里面的this就指向obj，`this.myName`就是`obj.myName`。其实这一条和上一条可以合在一起，没有明确调用者时其实隐含的调用者就是window，所以经常有人说**this总是指向调用者**。

### 总结

1. 只有通过实例调用原型中的函数,this才能生效。
2. 类局部开启了严格模式，让this不敢指向windows。
