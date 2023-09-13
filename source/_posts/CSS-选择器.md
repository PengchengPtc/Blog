---
title: CSS_选择器
date: 2021-01-25 09:19:19
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: CSS
tags:
	- CSS
---

## 选择器：CSS选择HTML元素,以下标签加内容才能生效，然后灵活使用。

### 1.id选择器：一一对应

```html
<div id="only">
    
</div>
```

```css
#only {
    background-color:red;
}
```

### 2.class选择器：多对多，一个class值对应多个元素(一种标签），一个元素(一种标签）可以有多个class的值

```html
<div class="demo">
    
</div>
```

```css
.demo {
    background-color:red;
}
```

### 3.标签选择器：

```html
<div>
    
</div>
```

```css
div {
    background-color:red
}
```

### 4.通配符选择器：

```css
* {
    background-color: green;
}
```

### 5.属性选择器：

```css
/*带id都选择*/
[id] {
    background-color: red；
}
[class] {
    background-color: red；
}
[id="only"] {
    background-color: red；
}
```

### 6.!important:

```html
<div style="background-color:red;">
</div>
```

```css
div{
    style="background-color:red!important;
}
```

### 7.父子选择器/派生选择器：前提呈现父子关系，直接间接都可以，两个选择器隔一个空格。

```html
<div class="wrapper">
    <span class="box">
        
    </span>
</div>
```

```css
div span{
    background-color:red;
}
/*或者*/
.wrapper .box{
     background-color:red;
}
```

### 8.直接子元素选择器：

```html
<div>
    <em></em>
    <strong>
        <em></em>
    </strong>
</div>
```

```css
div > em{
     background-color:red;
}
```

### 9.并列选择器：多种标签对应一种选择器，两个选择器连着写

```html
<div class="demo">
    
</div>
<p class="demo">
    
</p>
```

```css
div.demo{
      background-color:red;
}
```

### 10.分组选择器：不同的选择器公用一个代码块

```html
<em></em>
<strong></strong>
<span></span>

```

```css
em,
strong,
span{
    background-color:red;
}
```

### 11.伪类选择器：

```html
<a href=""></a>
```

### 1.hover

```css
/*鼠标移上去变*/
a{
    textdecoration: none;
}
a:hover{
    textdecoration: underline;
    background-color: #f40;
    color: #fff;
    font-size:12px;
    font-weight:bold;
    font-family:arial;
    /*圆角*/
    border-radius:10px;  
}
```



## 选择器优选级：

```html
<!--!important>行间样式>id>class|属性>标签选择器>通配符选择器-->
```

## CSS权重：只要写在同一行的选择器把他们相加。

```html
<!--!important             Infinity(256进制)
    行间样式                      1000
    id                            100
    class|属性|伪类选择器           10
    标签|伪元素                      1
    通配符                           0-->
```

