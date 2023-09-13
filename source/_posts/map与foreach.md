---
title: map与foreach
date: 2021-10-28 16:36:44
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: JS
tags:	
	 - JS
---

### map( )

> `**map()**` 方法创建一个**新数组**，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。

```js
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

```js
var points = this.toFlashList;
points.map((x) => new myMarker(x));
```

### forEach

> `**forEach()**` 方法对数组的每个元素执行一次给定的函数。
>
> 相当于遍历，在原数组上进行修改

```js
const array1 = ['a', 'b', 'c'];

array1.forEach(element => console.log(element));

// expected output: "a"
// expected output: "b"
// expected output: "c"

```

### 小结

> 注意二者区别
