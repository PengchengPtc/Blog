---
title: CSS_盒子模型
date: 2021-01-25 09:23:32
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: CSS
tags:
	- CSS
---

## 盒子模型：四部分,任何一个元素都可以设置为一个盒子。

```css
/* 1.外边距：margin
   2.盒子壁：border
   3.内边距： padding
   4.盒子内容： width + height
  margin + border + padding + （content=width +height)
```

## 盒子模型图：

[![sW863V.jpg](https://s3.ax1x.com/2021/01/20/sW863V.jpg)](https://imgchr.com/i/sW863V)

## 两盒子嵌套，让里面的盒子居中：

```css
/*1.两个盒子content一样大;
  2.外面的盒子套padding；
```

### Padding,margin,border-width是复合值:

```css
/*1.四个值顺时针：上右下左
   2.三个值：上，左右，下
   3.两个值：上下，左右*/
```

## 盒子模型计算：可看控制台查看

```css
/*计算可视区域的大小*/
```

## 通过margin调整标签之间的距离：

```html
<span class="demo"></span>
<span class="demo2"></span>
```

```css
.demo{
    margin-right: 10px
}
.demo2{
    margin-left: 10px
}
```

## 定位：

```css
<div></div>
```

```css
div {
    /*可定位*/
    position: absolute;
    /*左边线距左边距*/
    left：100px;
    /*右边线距上边距*/
  /*  right：100px;*/
    /*上边线距上边距*/
    top: 100px;
    width: 100px;
    height: 100px;
    background-color: red;
}
```

#### body具有天生的magin:8px过。

## 绝对定位与相对定位：

````css
/*
  1.层模型：绝对定位，就脱离原来的位置定位
  2.相对定位：保留原来的位置定位
*/
/*
带有绝对定位的盒子相对于最近的有定位的父级进行定位，如果没有，那么相对于文档进行定位
*/
/*
带有相对定位的盒子相对于他原来的位置进行定位
*/
````

### 定位原则：

```css
/*要定位的盒子设置位absolutely，被定位的盒子设置为relative作为参照。
```

### 固定定位：应用于广告；

```html
<div>
    
</div>
```

```css
div{
    position: fixed;
    width:50px;
    height: 200px;
    background-color: red;
    color: #fff;
}
```

## 块级元素居中：

```html
<div>
    
</div>
```

## 设置一个块级元素居中：

```css
div{
    position: absolute;
    left: 50%;
    top: 50%;
    width: 100px;
    height: 100px;
    background-color: red;
    /*差半个身位，因为上面设置的是相对于左顶点的百分之五十*/
    /*需要设置负值*/
    margin-left: -50px;
    margin-top: -50px;
}
```

### 浮动： 行排列

```css
/*1.脱标：指定位置(动）*/
/*2.浮动的盒子不保留原先的位置*/
float:left/none/right
/*浮动流按一行排列*/
```

## Flex布局：

```css
/*通过给父级添加flex属性，来控制子集*/
```

```css
/*容器属性：**
父级，元素是跟着主轴排列
- flex-direction：row/row-reverse/column/column-reverse决定项目的排列方向
- flex-wrap：决定如何换行
- flex-flow：上面两个的简写
- justify-content：决定主轴的对齐方式（水平方向）
- align-items：决定交叉轴的对齐方式（垂直方向）
- align-content：决定多根轴线的对齐方式

**项目属性：**

- order：定义项目的排列顺序
- flex-grow：定义项目的放大比例
- flex-shrink：定义项目的缩小比例
- flex-basis：定义项目占的主轴长度
- flex：flex-grow、flex-shrink、flex-basis简写，默认0 1 auto
- align-self：单个项目的对齐方式，覆盖原来的父元素的align-items*/
```



