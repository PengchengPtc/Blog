---
title: x++和++x的区别是什么？
date: 2021-04-11 11:36:34
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: C#
tags:
	- C#
---

x++和++x的区别：

++x是x的值先自增1，再计算x的值。

x++是先计算x的值，再将x的值自增1。

示例：

```
int x=10;
 
System.out.println(x++);  
 
System.out.println(x);
```

第一个输出10, x++先在当前表达式中使用x的值，然后再将x的值自增1，第二个输出11，因为经过上一条指令x自增了1。

```
int x=10;
 
System.out.println(++x);
 
System.out.println(x);
```

第一个输出11, ++x 先将x的值自增1，然后再在当前表达式中使用x的值，第二个也是输出11，经过上一条指令x自增了1。