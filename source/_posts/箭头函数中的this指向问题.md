---
title: 箭头函数中的this指向问题
date: 2021-09-22 18:20:03
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: JS
tags:
	- JS
---

# 箭头函数的this指向问题

> ​	箭头函数自身没有this指向，写this不会报错，会默认使用他外层是的this指向作为自己的this指向，可以在箭头函数中log一下this的指向。

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
            constructor(name, age) {
                this.name = name
                this.age = age
            }
            // 该函数定义在原型对象上,类里面不能直接定义箭头函数。
            study() {
                console.log("定义在原型对象上常规函数的this指向", this);
            }
            profession = "学生"
            study2 = function () {
                console.log("定义在类本身上的this指向", this);
            }
            study3 = ()=> {
                console.log("通过赋值和箭头函数定义在类中的箭头函数的指向",this)
            }
        }
        const p1 = new Person("王小明", "八岁")
        console.log(p1);
        p1.study()
        p1.study()  //通过实例调用,this肯定是找得到的
        x = p1.study2
        x()         //直接调用普通函数则不行
        x2 = p1.study3
        x2()        //直接调用箭头函数this指向任然存在
    </script>
</body>

</html>
```

