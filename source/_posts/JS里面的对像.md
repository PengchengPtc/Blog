---
title: JS里面的对象
date: 2023-09-21 10:51:34
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: JS
tags:	
	 - JS
---

# JS里面的对象

## 1.前言

​	对象的话往往和数组，字符串结合起来使用。

## 2.代码

```js
// Path: object.js
// 创建对象
// 1.通过字面量创建对象
let obj1 = {
    name: "zhangsan",
    age: 18,
}
console.log(obj1); // {name: "zhangsan", age: 18}
// 2.通过构造函数创建对象
function Person(name, age) {
    this.name = name;
    this.age = age;
}
let obj2 = new Person("zhangsan", 18);
console.log(obj2); // Person {name: "zhangsan", age: 18}
// 3.通过Object.create()创建对象
let obj3 = Object.create(null);
obj3.name = "zhangsan";
obj3.age = 18;
console.log(obj3); // {name: "zhangsan", age: 18}
// 4.通过工厂函数创建对象
function createPerson(name, age) {
    let obj = new Object();
    obj.name = name;
    obj.age = age;
    return obj;
}
let obj4 = createPerson("zhangsan", 18);
console.log(obj4); // {name: "zhangsan", age: 18}
// 5.通过原型链创建对象
function Person1() {}
Person1.prototype.name = "zhangsan";
Person1.prototype.age = 18;
let obj5 = new Person1();
console.log(obj5); // Person1 {}
// 6.通过Object.assign()创建对象
let obj6 = Object.assign({}, {
    name: "zhangsan",
    age: 18,
});

// 对象的增删改查
// 1.增
let obj7 = {
    name: "zhangsan",
    age: 18,
}
// 1.1.通过.的方式增加属性
obj7.height = 180;
console.log(obj7); // {name: "zhangsan", age: 18, height: 180}
// 1.2.通过[]的方式增加属性
obj7["weight"] = 70;
console.log(obj7); // {name: "zhangsan", age: 18, height: 180, weight: 70}
// 2.删
let obj8 = {
    name: "zhangsan",
    age: 18,
}
// 2.1.通过.的方式删除属性
delete obj8.name;
console.log(obj8); // {age: 18}
// 2.2.通过[]的方式删除属性
delete obj8["age"];
console.log(obj8); // {}
// 3.改
let obj9 = {
    name: "zhangsan",
    age: 18,
}
// 3.1.通过.的方式修改属性
obj9.name = "lisi";
console.log(obj9); // {name: "lisi", age: 18}
// 3.2.通过[]的方式修改属性
obj9["age"] = 20;
console.log(obj9); // {name: "lisi", age: 20}
// 4.查
let obj10 = {
    name: "zhangsan",
    age: 18,
}
// 4.1.通过.的方式查找属性
console.log(obj10.name); // zhangsan
// 4.2.通过[]的方式查找属性
console.log(obj10["age"]); // 18

// 对象的遍历
// 1.for...in循环遍历对象
let obj11 = {
    name: "zhangsan",
    age: 18,
}
for (let key in obj11) {
    console.log(key); // name age
    console.log(obj11[key]); // zhangsan 18
}
// 2.Object.keys()遍历对象
let obj12 = {
    name: "zhangsan",
    age: 18,
}
console.log(Object.keys(obj12)); // ["name", "age"]
// 3.Object.values()遍历对象
let obj13 = {
    name: "zhangsan",
    age: 18,
}
console.log(Object.values(obj13)); // ["zhangsan", 18]
// 4.Object.entries()遍历对象
let obj14 = {
    name: "zhangsan",
    age: 18,
}
console.log(Object.entries(obj14)); // [["name", "zhangsan"], ["age", 18]]
// 5.Object.getOwnPropertyNames()遍历对象
let obj15 = {
    name: "zhangsan",
    age: 18,
}
console.log(Object.getOwnPropertyNames(obj15)); // ["name", "age"]
// 6.Object.getOwnPropertySymbols()遍历对象
let obj16 = {
    name: "zhangsan",
    age: 18,
}   
console.log(Object.getOwnPropertySymbols(obj16)); // []
// 7.Reflect.ownKeys()遍历对象
let obj17 = {
    name: "zhangsan",
    age: 18,
}
console.log(Reflect.ownKeys(obj17)); // ["name", "age"]

// 对象的合并
// 1.通过Object.assign()合并对象
let obj18 = {
    name: "zhangsan",
    age: 18,
}
let obj19 = {
    height: 180,
    weight: 70,
}

let obj20 = Object.assign(obj18, obj19);
console.log(obj20); // {name: "zhangsan", age: 18, height: 180, weight: 70}
// 2.通过...合并对象
let obj21 = {
    name: "zhangsan",
    age: 18,

}
let obj22 = {
    height: 180,
    weight: 70,
}
let obj23 = {
    ...obj21,
    ...obj22,
}
console.log(obj23); // {name: "zhangsan", age: 18, height: 180, weight: 70}

// 对象的拷贝
// 1.通过Object.assign()拷贝对象
let obj24 = {
    name: "zhangsan",
    age: 18,
}
let obj25 = Object.assign({}, obj24);
console.log(obj25); // {name: "zhangsan", age: 18}
// 2.通过...拷贝对象
let obj26 = {
    name: "zhangsan",
    age: 18,
}

let obj27 = {
    ...obj26,
}
console.log(obj27); // {name: "zhangsan", age: 18}

// 对象的比较
// 1.通过===比较对象
let obj28 = {
    name: "zhangsan",
    age: 18,
}
let obj29 = {
    name: "zhangsan",
    age: 18,
}
console.log(obj28 === obj29); // false
// 2.通过JSON.stringify()比较对象
let obj30 = {
    name: "zhangsan",
    age: 18,
}
let obj31 = {
    name: "zhangsan",
    age: 18,
}
console.log(JSON.stringify(obj30) === JSON.stringify(obj31)); // true
// 3.通过Reflect.ownKeys()比较对象
let obj32 = {
    name: "zhangsan",
    age: 18,
}
let obj33 = {
    name: "zhangsan",
    age: 18,
}
console.log(Reflect.ownKeys(obj32).toString() === Reflect.ownKeys(obj33).toString()); // true

// 对象的转换
// 1.对象转换为字符串
let obj34 = {
    name: "zhangsan",
    age: 18,
}
console.log(obj34.toString()); // [object Object]
console.log(JSON.stringify(obj34)); // {"name":"zhangsan","age":18}
// 2.对象转换为数字
let obj35 = {
    name: "zhangsan",
    age: 18,
}
console.log(Number(obj35)); // NaN
// 3.对象转换为布尔值
let obj36 = {
    name: "zhangsan",
    age: 18,
}
console.log(Boolean(obj36)); // true
// 4.对象转换为日期
let obj37 = {
    name: "zhangsan",
    age: 18,
}
console.log(new Date(obj37)); // Invalid Date
// 5.对象转换为JSON
let obj38 = {
    name: "zhangsan",
    age: 18,
}
console.log(JSON.parse(obj38)); // Uncaught SyntaxError: Unexpected token o in JSON at position 1
// 6.对象转换为Unicode
let obj39 = {
    name: "zhangsan",
    age: 18,
}
console.log(escape(obj39)); // [object%20Object]
// 7.对象转换为Base64
let obj40 = {
    name: "zhangsan",
    age: 18,
}
console.log(btoa(obj40)); // Uncaught DOMException: Failed to execute 'btoa' on 'Window': The string to be encoded contains characters outside of the Latin1 range.
// 8.对象转换为HTML
let obj41 = {
    name: "zhangsan",
    age: 18,

}
console.log(obj41); // {name: "zhangsan", age: 18}
// 9.对象转换为ASCII
let obj42 = {
    name: "zhangsan",
    age: 18,
}

console.log(obj42.charCodeAt(0)); // NaN
// 10.对象转换为二进制
let obj43 = {
    name: "zhangsan",
    age: 18,
}
console.log(obj43.charCodeAt(0).toString(2)); // NaN
// 11.对象转换为八进制
let obj44 = {
    name: "zhangsan",
    age: 18,
}
console.log(obj44.charCodeAt(0).toString(8)); // NaN
// 12.对象转换为十六进制
let obj45 = {
    name: "zhangsan",
    age: 18,
}
console.log(obj45.charCodeAt(0).toString(16)); // NaN
// 13.对象转换为十进制
let obj46 = {
    name: "zhangsan",
    age: 18,
}
console.log(obj46.charCodeAt(0).toString(10)); // NaN
// 14.对象转换为其他进制
let obj47 = {
    name: "zhangsan",
    age: 18,
}
console.log(obj47.charCodeAt(0).toString(2)); // NaN
console.log(obj47.charCodeAt(0).toString(8)); // NaN
console.log(obj47.charCodeAt(0).toString(16)); // NaN



```

## 3.小结

​	下一节，深浅拷贝！！，后面手写promise！！！

