---
title: JS里面的数组
date: 2023-09-21 10:51:19
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: JS
tags:	
	 - JS
---

# JS里面的数组

## 1.前言

​	JS数组在实际开发中应用面广泛，一些方法只有熟练应用，才能在实际的开发中得心应手。

## 2.代码

```js
// 字符串转数组
let myData = "Manchester,London,Liverpool,Birmingham,Leeds,Carlisle";
let myArray = myData.split(",");
console.log(myArray); // ["Manchester", "London", "Liverpool", "Birmingham", "Leeds", "Carlisle"]

// 数组转字符串
let myNewString = myArray.join(",");
console.log(myNewString); // Manchester,London,Liverpool,Birmingham,Leeds,Carlisle

// 使用数组的toString()方法也可以达到同样的效果
let myNewString2 = myArray.toString();
console.log(myNewString2); // Manchester,London,Liverpool,Birmingham,Leeds,Carlisle

// 添加和删除数组元素
// push()方法可以接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度
let myArray2 = [];
myArray2.push("Manchester");
myArray2.push("London", "Liverpool", "Birmingham", "Leeds", "Carlisle");
console.log(myArray2); // ["Manchester", "London", "Liverpool", "Birmingham", "Leeds", "Carlisle"]

// pop()方法从数组末尾移除最后一项，减少数组的length值，然后返回移除的项
let myArray3 = [
  "Manchester",
  "London",
  "Liverpool",
  "Birmingham",
  "Leeds",
  "Carlisle",
];
myArray3.pop();
console.log(myArray3); // ["Manchester", "London", "Liverpool", "Birmingham", "Leeds"]

// unshift()和shift()方法从数组前端移除第一项，减少数组的length值，然后返回移除的项
let myArray4 = [
  "Manchester",
  "London",
  "Liverpool",
  "Birmingham",
  "Leeds",
  "Carlisle",
];
myArray4.shift();
console.log(myArray4); // ["London", "Liverpool", "Birmingham", "Leeds", "Carlisle"]

// 删除指定位置的元素
// splice()方法可以删除任意数量的项，只需指定2个参数：要删除的第一项的位置和要删除的项数
let myArray5 = [
  "Manchester",
  "London",
  "Liverpool",
  "Birmingham",
  "Leeds",
  "Carlisle",
];
myArray5.splice(2, 1); // 从位置2开始删除1个元素
console.log(myArray5); // ["Manchester", "London", "Birmingham", "Leeds", "Carlisle"]

// indexOf()方法可以接收一个参数，即要查找的项，然后返回该项所在的位置，如果没找到则返回-1
let myArray6 = [
  "Manchester",
  "London",
  "Liverpool",
  "Birmingham",
  "Leeds",
  "Carlisle",
];
let pos = myArray6.indexOf("London");
console.log(pos); // 1

// 如果数组中有多个相同的项，indexOf()方法只返回第一个匹配的项的位置
let myArray7 = [
  "Manchester",
  "London",
  "Liverpool",
  "Birmingham",
  "Leeds",
  "Carlisle",
  "London",
];
let pos2 = myArray7.indexOf("London");
console.log(pos2); // 1

// lastIndexOf()方法从数组的末尾向前查找，indexOf()方法从前向后查找
let myArray8 = [
  "Manchester",
  "London",
  "Liverpool",
  "Birmingham",
  "Leeds",
  "Carlisle",
  "London",
];
let pos3 = myArray8.lastIndexOf("London");
console.log(pos3); // 6

// 迭代方法
// every()方法对数组中的每一项运行给定函数，如果该函数对每一项都返回true，则返回true
let myArray9 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let everyResult = myArray9.every(function (item, index, array) {
  return item > 2;
});
console.log(everyResult); // false

// some()方法对数组中的每一项运行给定函数，如果该函数对任一项返回true，则返回true
let myArray10 = [1, 2, 3, 4, 5, 6, 7, 8, 9];
let someResult = myArray10.some(function (item, index, array) {
  return item > 2;
});
console.log(someResult); // true

// filter()方法对数组中的每一项运行给定函数，返回该函数会返回true的项组成的数组
let myArray11 = [1, 2, 3, 4, 5, 6, 7, 8, 9];
let filterResult = myArray11.filter(function (item, index, array) {
  return item > 2;
});
console.log(filterResult); // [3, 4, 5, 6, 7, 8, 9]

// map()方法对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组
let myArray12 = [1, 2, 3, 4, 5, 6, 7, 8, 9];
let mapResult = myArray12.map(function (item, index, array) {
  return item * 2;
});

console.log(mapResult); // [2, 4, 6, 8, 10, 12, 14, 16, 18]

// reduce()和reduceRight()方法迭代数组的所有项，然后构建一个最终返回的值
// reduce()方法从数组的第一项开始，逐个遍历到最后
// reduceRight()方法从数组的最后一项开始，向前遍历到第一项
let myArray13 = [1, 2, 3, 4, 5];
let reduceResult = myArray13.reduce(function (prev, cur, index, array) {
  return prev + cur;
});
console.log(reduceResult); // 15

// Date类型
// 创建日期对象
let now = new Date();
console.log(now); // Thu Jul 30 2020 15:20:00 GMT+0800 (中国标准时间)

// 也可以通过传入一个表示日期的字符串来创建Date对象
let someDate = new Date("May 25, 2004");
console.log(someDate); // Tue May 25 2004 00:00:00 GMT+0800 (中国标准时间)

```

## 3.小结

​	这些方法除了笔试时候要记准确外，实际开发中其实不用记，只需要知道有处理数组的这个方法就可以，查起来也挺快的。代码时间长了不写，就会忘，关键得复盘。

