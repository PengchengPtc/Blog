---
title: JS里面的字符串
date: 2023-09-21 10:51:25
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: JS
tags:	
	 - JS
---

# JS里面的字符串

## 1.前言

​	和数组一样，字符串应用的也比较多，其他的其实应用较少。

## 2.代码

```js
// 1.获得字符串的长度,代码如下:
let str = "hello world";
console.log(str.length); // 11

// 2.字符串添加元素,代码如下:
let str1 = "hello";
let str2 = "world";
let str3 = str1 + " " + str2;
console.log(str3); // hello world

// 3.字符串删除元素,代码如下:
let str4 = "hello world";
console.log(str4.slice(0, 5)); // hello
console.log(str4.slice(6)); // world

// 4.字符串查找元素,代码如下:
let str5 = "hello world";
console.log(str5.indexOf("world")); // 6

// 5.字符串替换元素,代码如下:
let str6 = "hello world";
console.log(str6.replace("world", "javascript")); // hello javascript

// 6.字符串截取元素,代码如下:
let str7 = "hello world";
console.log(str7.substr(0, 5)); // hello
console.log(str7.substr(6)); // world

// 7.字符串分割元素,代码如下:
let str8 = "hello world";
console.log(str8.split(" ")); // ["hello", "world"]

// 8.字符串合并元素,代码如下:
let str9 = ["hello", "world"];
console.log(str9.join(" ")); // hello world

// 9.字符串大小写转换,代码如下:
let str10 = "hello world";
console.log(str10.toUpperCase()); // HELLO WORLD
console.log(str10.toLowerCase()); // hello world

// 10.字符串比较,代码如下:
let str11 = "hello world";
let str12 = "hello world";
console.log(str11 === str12); // true

// 11.字符串转换为数组,代码如下:
let str13 = "hello world";
console.log(str13.split(" ")); // ["hello", "world"]

// 12.字符串转换为对象,代码如下:
let str14 = "hello world";
console.log(str14.split(" ")); // ["hello", "world"]

// 13.字符串转换为数字,代码如下:
let str15 = "123";
console.log(Number(str15)); // 123

// 14.字符串转换为布尔值,代码如下:
let str16 = "hello world";
console.log(Boolean(str16)); // true

// 15.字符串转换为日期,代码如下:
let str17 = "2019-12-12";
console.log(new Date(str17)); // Thu Dec 12 2019 08:00:00 GMT+0800 (中国标准时间)

// 16.字符串转换为JSON,代码如下:
let str18 = '{"name": "zhangsan", "age": 18}';
console.log(JSON.parse(str18)); // {name: "zhangsan", age: 18}

// 17.字符串转换为Unicode,代码如下:
let str19 = "hello world";
console.log(escape(str19)); // hello%20world

// 18.字符串转换为Base64,代码如下:
let str20 = "hello world";
console.log(btoa(str20)); // aGVsbG8gd29ybGQ=

// 19.字符串转换为HTML,代码如下:
let str21 = "<p>hello world</p>";
console.log(str21); // <p>hello world</p>

// 20.字符串转换为ASCII,代码如下:
let str22 = "hello world";
console.log(str22.charCodeAt(0)); // 104

// 21.字符串转换为二进制,代码如下:
let str23 = "hello world";
console.log(str23.charCodeAt(0).toString(2)); // 1101000

// 22.字符串转换为八进制,代码如下:
let str24 = "hello world";
console.log(str24.charCodeAt(0).toString(8)); // 150

// 23.字符串转换为十六进制,代码如下:
let str25 = "hello world";
console.log(str25.charCodeAt(0).toString(16)); // 68

// 24.字符串转换为十进制,代码如下:
let str26 = "hello world";
console.log(str26.charCodeAt(0).toString(10)); // 104

// 25.字符串转换为其他进制,代码如下:
let str27 = "hello world";
console.log(str27.charCodeAt(0).toString(2)); // 1101000
console.log(str27.charCodeAt(0).toString(8)); // 150
console.log(str27.charCodeAt(0).toString(16)); // 68
console.log(str27.charCodeAt(0).toString(10)); // 104

// 26.字符串转换为其他类型,代码如下:
let str28 = "hello world";
console.log(Number(str28)); // NaN
console.log(Boolean(str28)); // true
console.log(JSON.parse(str28)); // Uncaught SyntaxError: Unexpected token h in JSON at position 0

// 27.字符串转换为其他编码,代码如下:
let str29 = "hello world";
console.log(escape(str29)); // hello%20world
console.log(btoa(str29)); // aGVsbG8gd29ybGQ=

// 28.字符串转换为其他格式,代码如下:
let str30 = "hello world";
console.log(str30.split(" ")); // ["hello", "world"]
console.log(str30.toUpperCase()); // HELLO WORLD
console.log(str30.toLowerCase()); // hello world

// 29.字符串转换为其他,代码如下:
let str31 = "hello world";
console.log(str31.slice(0, 5)); // hello
console.log(str31.slice(6)); // world
console.log(str31.indexOf("world")); // 6
console.log(str31.replace("world", "javascript")); // hello javascript
console.log(str31.substr(0, 5)); // hello
console.log(str31.substr(6)); // world
console.log(str31.split(" ")); // ["hello", "world"]
console.log(str31.join(" ")); // hello world
console.log(str31.toUpperCase()); // HELLO WORLD
console.log(str31.toLowerCase()); // hello world
console.log(str31 === str31); // true
console.log(str31.split(" ")); // ["hello", "world"]
console.log(str31.split(" ")); // ["hello", "world"]
console.log(Number(str31)); // NaN
console.log(Boolean(str31)); // true
console.log(new Date(str31)); // Invalid Date
console.log(JSON.parse(str31)); // Uncaught SyntaxError: Unexpected token h in JSON at position 0

```

## 3.小结

​	不用记，一样得经常复盘。
