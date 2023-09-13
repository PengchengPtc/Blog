---
title: JavaScript高级原型链
date: 2021-07-29 17:55:25
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: JavaScript
tags:
	- JavaScript
---

## 构造函数(ES5)和原型

###　概述

在典型的ＯＯＰ的语言中（如Java），都存在类的概念，类就是对象的模板，对象就是类的实例，但在ES6之前，JS中并密钥引入类的概念。

ES6，全称ECMAScript6.0，2015.0.6发版。但是目前浏览器JavaScript是ES5版本，大多数高版本的浏览器也支持ES6，不过只实现了ES6的部分特性和功能。

在ES6之前，对象不是基于类创建的，而是用一种称为**构造函数**的特殊函数来定义对象和他们的特征。

创建对象可以通过以下三种方式

1. 对象自变量

   ```js
   var obj1 = {};
   ```

2. new Object()

   ```js
   var obj2 = new Object();
   ```

3. 自定义构造函数

   ```js
   //利用构造函数创建类
   function Star(uname,age) {
       this.uname = uname;
       this.age = age;
       this.sing = function() {
           console.log('I can dance')
       }
   }
   //创建对象
   var dlz = new Star('带篮子'，18);
   var zxy = new star('张学友'，19);
   console.log(dlz);
   dlz.sing()
   zxy.sing()
   ```

   ### 构造函数

   构造函数是一中特殊的函数，主要用来初始化对象，即为对象成员变量赋值始值，它总与new一起使用。我们可以把对象中的一些公共的属性和方法抽取出来，然后封装到这个函数里面。

   #### new在执行时会做四件事情

   1. 在内存中创建一个新的空对象
   2. 让this指向这个新的对象
   3. **执行构造函数里面的代码**（记住只是定义，在new之前没有调用），给这个新对象添加属性和方法
   4. 返回这个新对象(所以构造函数里面不需要return)

   #### 实例成员和静态成员

   ##### 实例成员 

   > 实例成员就说构造函数内部通过this添加的成员，uname，age，sing就是实例成员
   >
   > 实例对象只能通过实例化的对象访问

   ```js
   console.log(dlz.uname);   //对
   dlz.sing();               //对
   console.log(Star.uname);  //undefined，不可以通过构造函数来访问实例对象
   ```

   ##### 静态成员

   > 在构造函数本身上添加的成员 

   ```js
   Star.sex = '男'
   console.log(Star.sex);
   console.log(dlz.sex);     //undefined,不能可以通过实例对象访问静态成员
   ```

   #### 构造函数存在的问题

   > 构造函数方法很好用，但是存在浪费内存的问题。
   >
   > 每创建一个对象，里面的函数都要开辟新的内存空间。

   ```js
   console.log(dlz.sing === zxy.sing)     //false，false比较的是内存地址，虽然是同一个函数，但用不同地址存。
   ```

[![WTKB38.png](https://z3.ax1x.com/2021/07/28/WTKB38.png)](https://imgtu.com/i/WTKB38)

### 构造函数原型prototype

> prototype是一个对象，prototype是原型的意思，故称之为原型对象。

```js
console.dir(Star)
```

[![WTlIv8.png](https://z3.ax1x.com/2021/07/28/WTlIv8.png)](https://imgtu.com/i/WTlIv8)

构造函数通过原型分配的函数是所有对象所**共享的**。

JavaScript规定，**每一个构造函数都有一个prototype属性**，指向另一个对象。注意这个prototype就是一个对象，这个对象的所有属性和方法，都会呗构造函数所拥有。

**我们可以把那些不变的方法，直接定义在prototype对象上，这样所有对象的实例可以共享这些方法。**

```js
  Star.prototype.sing= function() {
            console.log('i can dance')
        }
  dlz.sing()                           // i can dance
  zxy.sing()                           // i can dance
```

```js
console.log(dlz.sing === zxy.sing)     //true，实现了共享
```

一般情况下，我们的公共属性定义到构造函数里面，公关的方法我们放到原型对象上。

#### 对象原型(__proto__)

> 对象都会有一个属性_proto_指向构造函数的prototype原型对象，之所以我们对象可以使用构造函数prototype原型对象的属性和方法，就是因为对象有_proto_原型的存在

```js
console.log(dlz); //对象身上系统自己添加一个_proto_指向我们构造函数的原型对象
console.log(dlz.__proto__ === Star.prototype); //true
//方法的查找规则：首先先看dlz对象上是否有sing方法，如果有就执行这个对象上的sing
//如果没有sing这个方法，因为有_proto_的存在，就取构造函数原型对象prototype身上取查找sing这个方法。
```

#####　constructor构造函数

对象原型(_proto_)和构造函数原型对象里面都有一个属性contructor属性，constructor我们称为构造函数，因为它指回到构造函数本身。

constructor主要记录该对象引用于哪个构造函数，它可以让原型对象重新指向原来的构造函数。

很多情况下，我们需要手动的利用constructor这个属性指回原来的构造函数

```js
Star.prototype = {
    constructor: Star,
    sing: function() {
        console.log('i can sing')
        
    }
    movie: function() {
        console.log('i can act')
    }
}
```

### 构造函数、实例、原型对象三者之间的关系

[![WHeL6g.png](https://z3.ax1x.com/2021/07/29/WHeL6g.png)](https://imgtu.com/i/WHeL6g)

### 原型链

[![WH8MC9.png](https://z3.ax1x.com/2021/07/29/WH8MC9.png)](https://imgtu.com/i/WH8MC9)

```js
1.是个对象就有__proto__，为对象原型，对应类的原型对象，即prototype。
2.对象是根据类创建的，类里面是prototype，对象里面是__prototype__，二者相等。
3.constructor是原型对象里面的一个属性，录该对象引用于哪个构造函数。
4.prototype是对象，__proto__也是对象。
```

学了原型链，更方便我们查找对象的原型对象所对应的构造函数，一层递一层。

### JavaScript成员查找机制

[![WH03Jf.png](https://z3.ax1x.com/2021/07/29/WH03Jf.png)](https://imgtu.com/i/WH03Jf)

> 1.只要原型链上有一个原型对象有实例对象想使用的方法或者属性，实例对象都能调用成功。
>
> 2.实例对象自身没有定义那个方法或者属性，它会就近使用。

### 原型对象中this指向

> 1.只有你调用了这个函数，才能知道的这个this指向谁。
>
> 2.一般情况下，this指的是函数的调用者。

```js
var that;
Star.prototype.sing = function() {
    console.log('i can sing')
    that = this
}
var ldh = new Star('刘德华'，18)
//1.在构造函数中，里面this指向的是实例对象ldh
ldh.sing();
console.log(that = ldh);
//2.原型对象函数里面的this指向实例对象ldh
```

### 原型对象的应用

#### 扩展内置对象方法

```js
   //array是一个内置对象，里面有一些固定的方法。
        console.log(Array.prototype)
        Array.prototype.sum  = function() {
            var sum = 0;
            for (var i = 0;i < this.length; i++) {    //this指向调用者
                sum += this[i];
            }
            return sum;
        }
        var arr1 = new Array(11,22,33)
        //arr1调用了sum函数，故this指向arr1
        console.log(arr1.sum())
        //此处相当于实例对象
        var arr = [1,2,3]
        console.log(arr.sum());
        // 可以检验arr是否为Array的实例对象
        console.log(arr.__proto__ === Array.prototype);  //true
        console.log(Array.prototype) //查看原型对象是否存在这个新加的sum函数
```

[![WHOpXF.png](https://z3.ax1x.com/2021/07/29/WHOpXF.png)](https://imgtu.com/i/WHOpXF)

### 继承

ES6之前并没有给我们提供extend继承。我们可以通过构造函数+原型对象模拟实现继承，被称为组合继承。

#### call()

调用这个函数，并且修改函数运行时的this指向。

```js
  //call方法
        function fn(x,y) {
            console.log('我想喝手磨咖啡');
            //查看函数内部this的指向
            console.log(this);
            console.log(x+y);
        }
        // this.fn()//this是调用者，这个是window，可以省略this
        // fn()
        // fn.call()
        var o = {
            name: 'andy'
        };
        fn.call(o,1,2)
```

#### 借用构造函数继承父类型属性

> 核心原理：通过call()把父类型的this指向子类型的this，这样就可以实现子类型继承父类型的属性。

```js
  //借用父构造函数继承属性
        //1.父构造函数
        function Father (uname,age) {
            // this指向父构造函数的对象实例
            this.uname = uname;
            this.age =age;
        }
        //2.子构造函数
        function Son(uname,age,score) {
            // this指向子构造函数的对象实例,把父函数的this改为子函数的this
            Father.call(this,uname,age)
            this.score = score
        }
        var son = new Son('刘德华',18)
        console.log(son)
```

####　借用原型对象继承方法

```js
   //借用父构造函数继承属性
        //1.父构造函数
        function Father (uname,age) {
            // this指向父构造函数的对象实例
            this.uname = uname;
            this.age =age;
        }
        Father.prototype.money = function() {
            console.log(100000)
        }
        //2.子构造函数
        function Son(uname,age,score) {
            // this指向子构造函数的对象实例,把父函数的this改为子函数的this
            Father.call(this,uname,age)
            this.score = score
        }
        // son.prototype= Father.prototype //有问题，如果修改了子原型对象，父原型对象也会一起变化
        Son.prototype = new Father();
        //如果利用对象形式修改了原型对象，别忘了利用constructor指回原来的原型对象
        Son.prototype.constructor = Son;
        Son.prototype.exam = function() {
            console.log('孩子要考试')
        }
        var son = new Son('刘德华',18)
        console.log(son)
        console.log(Son.prototype.constructor);
```

### ES5新增方法概述

ES5中给我们新增了一些方法，可以很方便的操作数组或者字符串，这些方法包括：

- 数组方法
- 字符串方法
- 对象方法

####　数组方法

迭代（遍历）方法：forEach(),map(),filter(),some(),every();

##### forEach(里面有一个回调函数)

[![WbfZvR.png](https://z3.ax1x.com/2021/07/29/WbfZvR.png)](https://imgtu.com/i/WbfZvR)

```js
        var arr = [1,2,3]
        var sum = 0
        arr.forEach(function(value,index,array){
            console.log('每个数组元素'+value);
            console.log('每个元素的索引号'+index);
            console.log('数组本身'+array);
            sum += value
        })
        console.log(sum)
    
```

##### filter

[![WbfWZV.png](https://z3.ax1x.com/2021/07/29/WbfWZV.png)](https://imgtu.com/i/WbfWZV)

```js
     //filter 筛选数组
        var arr = [12,66,4,88,1,3]
        var newArr = arr.filter(function(value,index) {
            // return value >=20;
            return value%2 === 0
        })
        console.log(newArr)
```

##### some

[![Wb4Vn1.png](https://z3.ax1x.com/2021/07/29/Wb4Vn1.png)](https://imgtu.com/i/Wb4Vn1)

```js
  var arr = [10, 20, 4]
        var flag = arr.some(function (value) {
            return value >= 20
        })
        console.log(flag);  //true，返回布尔值
```

> 只要查到一个满足条件，即跳出循环。

#### 字符串方法

trim()方法会从一个字符串的两端删除空白字符。

```js
str.trim()
```

trim()方法并不影响字符串本身，它返回的是一个新的字符串，只去掉两侧的。

```js
  var str = '   andy    '
        console.log(str);
        var str1 =str.trim();
        console.log(str1)
```

#### 对象方法

##### keys

[![Wb7Awn.png](https://z3.ax1x.com/2021/07/29/Wb7Awn.png)](https://imgtu.com/i/Wb7Awn)

```JS
  var obj = {
            id: 1,
            pname: 'xiaomi',
            price: 19999,
            num:2000
        }
        var arr = Object.keys(obj)
        console.log(arr);
```

##### defineProperty

[![WbbprQ.png](https://z3.ax1x.com/2021/07/29/WbbprQ.png)](https://imgtu.com/i/WbbprQ)

```js
    var obj = {
            id: 1,
            pname: 'xiaomi',
            price: 19999,
            num:2000
        }
        // var arr = Object.keys(obj)
        // console.log(arr);
        // 新增或者修改以前
        obj.num = 1000;
        obj.price =99;
        console.log(obj);
        //es5新增
        Object.defineProperties(Obj,'num',{
            value:1000
        });
        console.log(obj)
        Object.defineProperties(Obj,'price',{
            value:9.9
        });
        console.log(obj)

```

