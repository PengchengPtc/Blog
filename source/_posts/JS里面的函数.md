---
title: JS里面的函数
date: 2023-09-21 10:51:43
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: JS
tags:	
	 - JS
---

# JS里面的函数

## 1.前言

​	直接上代码！

## 2.代码

```js
// Path: function.js
// 一、函数的定义
// 1.通过函数声明的方式定义(命名函数)
function max(a, b) {
  return a > b ? a : b;
}
console.log(max(2, 3)); // 3
// 2.通过函数表达式的方式定义(匿名函数)
let max = function (a, b) {
  return a > b ? a : b;
};
console.log(max(2, 3)); // 3
// 3.通过Function构造函数实例化的方式来定义函数
let max = new Function("a", "b", "return a > b ? a : b");
console.log(max(2, 3)); // 3
// 函数的调用
// 1.直接调用
function test() {
  console.log("this is", this);
}
test(); // window
// 2.作为对象的方法调用
let obj = {
  name: "obj",
  test: function () {
    console.log("this is", this);
  },
};
obj.test(); // obj
// 3.通过call()和apply()间接调用
let obj2 = {
  name: "obj",
  test: function () {
    console.log("this is", this);
  },
};
let obj3 = { name: "obj3" };
obj.test.call(obj2); // obj3
obj.test.apply(obj2); // obj3
// 4.作为构造函数调用
function Person(name) {
  this.name = name;
}
let obj4 = new Person("obj4");
console.log(obj4.name); // obj4
// 5.作为函数方法调用
function test() {
  console.log("this is", this);
}
test.call(null); // window

// 二、函数的参数
// 1.函数的参数数量
function test(a, b, c) {
  console.log(arguments); // [1, 2, 3]
}
test(1, 2, 3);
// 2.函数的参数类型
function test(a, b, c) {
  console.log(typeof a); // number
  console.log(typeof b); // string
  console.log(typeof c); // object
}
test(1, "2", { name: "obj" });
// 3.函数的参数传递
function addTen(num) {
  num += 10;
  return num;
}
let count = 20;
let result2 = addTen(count);
console.log(count); // 20
console.log(result2); // 30
// 4.检测参数数量
function doAdd(num1, num2) {
  if (arguments.length === 1) {
    console.log(num1 + 10);
  } else if (arguments.length === 2) {
    console.log(arguments[0] + num2);
  }
}
doAdd(10); // 20
doAdd(30, 20); // 50
// 5.没有重载,后面的会覆盖前面的
function addSomeNumber(num) {
  return num + 100;
}
function addSomeNumber(num) {
  return num + 200;
}
let result1 = addSomeNumber(100); // 300
console.log(result1);

// 三、函数的属性和方法
// 1.length属性
function test1(a, b, c) {
  console.log(test1.length); // 3
}
test1(1, 2, 3);
// 2.prototype属性
function test2() {
  console.log("this is", this);
}
test2.prototype.name = "obj";
let obj5 = new test2();
console.log(obj5.name); // obj
// 3.call()方法
function test3(a, b, c) {
  console.log(a, b, c); // 1 2 3
}
test3.call(null, 1, 2, 3);
// 4.apply()方法
function test4(a, b, c) {
  console.log(a, b, c); // 1 2 3
}
test4.apply(null, [1, 2, 3]);
// 5.bind()方法
function test5(a, b, c) {
  console.log(a, b, c); // 1 2 3
}
test5.bind(null, 1, 2, 3)();

// 四、函数的内部属性
// 1.arguments属性
function test6(a, b, c) {
  console.log(arguments); // [1, 2, 3]
}
test6(1, 2, 3);
// 2.callee属性
function test7() {
  console.log(arguments.callee); // ƒ test7()
}
test7();
// 3.caller属性
function outer() {
  inner();
}
function inner() {
  console.log(inner.caller); // ƒ outer() { inner(); }
}
outer();

// 五、函数的属性和方法
// 1.函数的属性
function test8() {
  console.log("this is", this);
}
test8.name; // test8
test8.length; // 0
// 2.函数的方法
function test9() {
  console.log("this is", this);
}
test9.call(null); // window
test9.apply(null); // window
test9.bind(null)(); // window

// 六、函数的高级特性
// 1.函数的递归
function factorial(num) {
  if (num <= 1) {
    return 1;
  } else {
    return num * factorial(num - 1);
  }
}
console.log(factorial(5)); // 120
// 2.闭包,闭包是指有权访问另一个函数作用域中的变量的函数
function createComparisonFunction(propertyName) {
  return function (object1, object2) {
    let value1 = object1[propertyName];
    let value2 = object2[propertyName];
    if (value1 < value2) {
      return -1;
    } else if (value1 > value2) {
      return 1;
    } else {
      return 0;
    }
  };
}
function sortData() {
  let data = [
    { name: "Zachary", age: 28 },
    { name: "Nicholas", age: 29 },
  ];

  data.sort(createComparisonFunction("name"));
  console.log(data[0].name); // Nicholas

  data.sort(createComparisonFunction("age"));
  console.log(data[0].name); // Zachary
}

sortData(); // 调用函数以执行排序和打印操作

// 3.闭包与变量
function createFunctions() {
  let result = new Array();
  for (var i = 0; i < 10; i++) {
    result[i] = function () {
      return i;
    };
  }
  return result;
}
let result = createFunctions();
console.log(result[0]()); // 10
console.log(result[1]()); // 10
console.log(result[2]()); // 10
// 4.模仿块级作用域
function outputNumbers(count) {
  for (var i = 0; i < count; i++) {
    console.log(i);
  }
  console.log(i); // 10
}
outputNumbers(10);
// 5.私有变量
function MyObject() {
  // 私有变量和私有函数
  let privateVariable = 10;
  function privateFunction() {
    return false;
  }
  // 特权方法
  this.publicMethod = function () {
    privateVariable++;
    return privateFunction();
  };
}
let obj10 = new MyObject();
console.log(obj10.publicMethod()); // false
// 6.静态私有变量
(function () {
  // 私有变量和私有函数
  let privateVariable = 10;
  function privateFunction() {
    return false;
  }
  // 构造函数
  MyObject = function () {};
  // 公有/特权方法
  MyObject.prototype.publicMethod = function () {
    privateVariable++;
    return privateFunction();
  };
})();
let obj11 = new MyObject();
console.log(obj11.publicMethod()); // false
// 7.模块模式
let singleton = (function () {
  // 私有变量和私有函数
  let privateVariable = 10;
  function privateFunction() {
    return false;
  }
  // 特权/公有方法和属性
  return {
    publicProperty: true,
    publicMethod: function () {
      privateVariable++;
      return privateFunction();
    },
  };
})();
console.log(singleton.publicMethod()); // false
// 8.增强的模块模式
let singleton2 = (function () {
  // 私有变量和私有函数
  let privateVariable = 10;
  function privateFunction() {
    return false;
  }
  // 创建对象
  let object = new CustomType();
  // 添加特权/公有属性和方法
  object.publicProperty = true;
  object.publicMethod = function () {
    privateVariable++;
    return privateFunction();
  };
  // 返回这个对象
  return object;
})();
console.log(singleton2.publicMethod()); // false
// 9.封装变量
function Person(name) {
  this.getName = function () {
    return name;
  };
  this.setName = function (value) {
    name = value;
  };
}
let person = new Person("Nicholas");
console.log(person.getName()); // Nicholas
person.setName("Greg");
console.log(person.getName()); // Greg
// 10.静态私有变量
(function () {
  // 私有变量和私有函数
  let privateVariable = 10;
  function privateFunction() {
    return false;
  }
  // 构造函数
  MyObject = function () {};
  // 公有/特权方法
  MyObject.prototype.publicMethod = function () {
    privateVariable++;
    return privateFunction();
  };
})();
let obj12 = new MyObject();
console.log(obj12.publicMethod()); // false
// 11.模块模式
let singleton3 = (function () {
  // 私有变量和私有函数
  let privateVariable = 10;
  function privateFunction() {
    return false;
  }
  // 特权/公有方法和属性
  return {
    publicProperty: true,
    publicMethod: function () {
      privateVariable++;
      return privateFunction();
    },
  };
})();
console.log(singleton3.publicMethod()); // false
// 12.增强的模块模式
let singleton4 = (function () {
  // 私有变量和私有函数
  let privateVariable = 10;
  function privateFunction() {
    return false;
  }
  // 创建对象
  let object = new CustomType();
  // 添加特权/公有属性和方法
  object.publicProperty = true;
  object.publicMethod = function () {
    privateVariable++;
    return privateFunction();
  };
  // 返回这个对象
  return object;
})();
console.log(singleton4.publicMethod()); // false
// 13.封装变量
function Person(name) {
  this.getName = function () {
    return name;
  };
  this.setName = function (value) {
    name = value;
  };
}
let person2 = new Person("Nicholas");
console.log(person2.getName()); // Nicholas
person.setName("Greg");
console.log(person2.getName()); // Greg
// 14.静态私有变量
(function () {
  // 私有变量和私有函数
  let privateVariable = 10;
  function privateFunction() {
    return false;
  }
  // 构造函数
  MyObject = function () {};
  // 公有/特权方法
  MyObject.prototype.publicMethod = function () {
    privateVariable++;
    return privateFunction();
  };
})();
let obj13 = new MyObject();
console.log(obj13.publicMethod()); // false

```

## 3.小结

​	复盘！！！！

