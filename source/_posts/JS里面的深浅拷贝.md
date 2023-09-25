---
title: JS里面的深浅拷贝
date: 2023-09-21 11:29:21
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: JS
tags:	
	 - JS
---

# JS里面的深浅拷贝

## 1.什么是深拷贝，什么事浅拷贝？

在 JavaScript 中，深拷贝和浅拷贝是两种不同的对象复制方式，它们在复制对象时的行为不同。下面我将解释这两种拷贝方式以及如何实现它们。

### 浅拷贝（Shallow Copy）

浅拷贝是指创建一个新的对象，然后将原始对象的属性值复制到新对象中。但是，如果属性值本身是对象，那么新对象中的该属性将引用原始对象中的相同对象。这就意味着，如果s你修改新对象中的属性值，原始对象中的对应属性值也会受到影响，因为它们引用的是同一个对象。

在 JavaScript 中，可以使用多种方式进行浅拷贝，包括：

1. **使用对象展开运算符（Spread Operator）：**

   ```js
   javascriptCopy code
   const originalObj = { name: 'John', age: 30 };
   const shallowCopy = { ...originalObj };
   ```

2. **使用`Object.assign`方法：**

   ```js
   javascriptCopy code
   const originalObj = { name: 'John', age: 30 };
   const shallowCopy = Object.assign({}, originalObj);
   ```

### 深拷贝（Deep Copy）

深拷贝是指创建一个新的对象，然后递归地复制原始对象及其所有嵌套对象的属性值，确保新对象中的所有属性都是独立的，不会与原始对象中的属性共享引用。这样，修改新对象中的属性值不会影响原始对象。

在 JavaScript 中，实现深拷贝通常需要自己编写递归函数或使用第三方库，因为深拷贝涉及到处理嵌套对象和循环引用的复杂情况。以下是一个简单的深拷贝示例，使用递归方法：

```js
javascriptCopy code
function deepCopy(obj) {
  if (typeof obj !== 'object' || obj === null) {
    return obj; // 如果不是对象或是null，直接返回
  }
  
  if (Array.isArray(obj)) {
    // 如果是数组，创建一个新数组并递归复制每个元素
    return obj.map(item => deepCopy(item));
  }
  
  // 如果是普通对象，创建一个新对象并递归复制每个属性
  const newObj = {};
  for (const key in obj) {
    if (obj.hasOwnProperty(key)) {
      newObj[key] = deepCopy(obj[key]);
    }
  }
  
  return newObj;
}

const originalObj = { name: 'John', info: { age: 30 } };
const deepClone = deepCopy(originalObj);
```

需要注意的是，深拷贝可能会更消耗内存和计算资源，因为它要递归遍历对象的所有属性。在处理大型嵌套对象时，需要小心使用深拷贝以避免性能问题。

## 2.哪些是深拷贝，哪些是浅拷贝？

以下是一些常见的 JavaScript 拷贝方法，以及它们是深拷贝还是浅拷贝的示例：

### 浅拷贝（Shallow Copy）：

1. **对象展开运算符（Spread Operator）：**

   ```js
   javascriptCopy code
   const originalObj = { name: 'John', age: 30 };
   const shallowCopy = { ...originalObj };
   ```

   这是浅拷贝，因为它只会复制原始对象的一层属性，如果对象中有嵌套对象，新对象中的嵌套对象仍然与原始对象共享引用。

2. **`Object.assign`方法：**

   ```js
   javascriptCopy code
   const originalObj = { name: 'John', age: 30 };
   const shallowCopy = Object.assign({}, originalObj);
   ```

   同样是浅拷贝，因为它也只复制原始对象的一层属性。

### 深拷贝（Deep Copy）：

1. **递归自定义深拷贝函数：**

   ```js
   javascriptCopy code
   function deepCopy(obj) {
     // 实现深拷贝的递归函数，复制所有嵌套对象的属性值
   }
   const originalObj = { name: 'John', info: { age: 30 } };
   const deepClone = deepCopy(originalObj);
   ```

   这是深拷贝，因为它递归地复制了原始对象及其所有嵌套对象的属性，确保新对象中的所有属性都是独立的，不与原始对象共享引用。

2. **使用第三方库如 `Lodash` 的 `_.cloneDeep` 方法：**

   ```js
   javascriptCopy code
   const _ = require('lodash');
   const originalObj = { name: 'John', info: { age: 30 } };
   const deepClone = _.cloneDeep(originalObj);
   ```

   `_.cloneDeep` 是深拷贝方法，它会递归复制所有嵌套对象的属性。

深拷贝会复制对象及其所有嵌套对象的属性，确保它们是独立的，而浅拷贝只复制对象的一层属性，嵌套对象仍然与原始对象共享引用。选择拷贝方法取决于你的需求，深拷贝通常用于确保对象之间的完全独立性，而浅拷贝通常用于创建对象的快照或浅层复制。

## 3.JSON.parse(JSON.stringify(obj))

`JSON.parse(JSON.stringify(obj))` 是一种常见的进行深拷贝的方法，但要注意它有一些限制和注意事项。

**优点：**

- 它是一种相对简单的深拷贝方法，不需要编写自定义的递归函数。
- 它可以用于大多数普通对象和数组，将它们从原始对象中完全复制到新的对象中。

**限制和注意事项：**

1. **不支持特殊数据类型：** JSON 格式不支持复杂的数据类型，如函数、正则表达式、`undefined` 等。如果原始对象包含这些类型，它们会在序列化和反序列化过程中丢失或被转换为 `null`。
2. **不支持循环引用：** 如果原始对象包含循环引用（即对象引用自身），则该方法会引发错误，因为 JSON 格式无法表示循环引用。
3. **不复制对象的原型链：** 新对象不会继承原始对象的原型链。
4. **性能问题：** 对于大型嵌套对象或数组，这种方法可能会导致性能问题，因为它需要进行序列化和反序列化操作。

总之，`JSON.parse(JSON.stringify(obj))` 是一种简单的深拷贝方法，适用于普通对象和数组，但需要注意其限制，特别是不支持特殊数据类型和循环引用。如果你的对象包含这些情况，或者需要更高性能的深拷贝，可能需要考虑使用其他深拷贝方法，如自定义递归函数或第三方库。
