---
title: HTML_超文本标记语言
date: 2021-01-25 09:15:59
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: HTML
tags:
	- HTML
---

## HTML:超文本标记语言,一般由一对一对标签组成。

***最准确的网页设计思路是把网页分成三个层次，即：结构层(HTML)、表示层(CSS)、行为层(Javascrip*t)。**

### 1,HTML标签：标签带有CSS属性；

#### 1.基础标签：

```html
<!--后面的属性是搜索引擎爬虫我们网页是关于什么的-->
<html lang="en">
    根标签
</html>
<head>
    写个浏览器看的，给浏览器设置的
</head>
<title>标题标签</title>
<body>
    写给用户看的
</body>
<!--万国码-->
<meta charset='utf-8'>
<!-- 后面属性告诉搜索引擎爬虫我们网页是关于什么的 -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="life"     content="life is shit">
```

```html
<p>
    让内容成段展示
</p>
<h1>
    1.有六级(h1到h6)
    2.标题
    3.加粗
    4.成段展示
</h1>
<strong>
    <em>加粗又斜体</em>
</strong>
<ins>
    下划线
</ins>
<del>
    中划线
</del>
<address>
    1.写地址
    2.成段展示，且斜体
</address>
```

```html
<div>
    1.分块
    2.充当盒子
    3.可捆绑操作
    4.独占一行
</div>
<span>
    1.分块
    2.充当盒子
    3.可捆绑操作
    4.可一行使用
</span>
```

```html
<!--回车-->
<br>
<!--水平线-->
<hr>
```

#### 2.高级标签:

##### HTML编码：

```html
<!--回车，空格：文本分隔符-->
<!--html编码>      
<!--html编码的空格表达方式-->
&nbsp;
<!--小于符-->
&lt;
<!--大于符-->
&gt;
```

##### 列表：

```html
<!--有序列表,可添加添加属type="a/A/1/i/I-->
<!--添加reversed="reversed"属性，逆序-->
<!--start="2"从第几个开始排序，只能数字-->
<ol>
    <li></li>
    <li></li>
    <li></li>
</ol>
<!--无序列表-->
<!--type="disc/square/circle"-->
<!--可用父子结构做导航栏，作为其骨架-->
<ul>
    <li></li>   
    <li></li>  
    <li></li>  
</ul>   
```

##### 图片：

```html
<!--src后面的是图片资源地址-->
<!--height=500px,width="",一般只写一个-->
1.网上的url
2.本机的绝对路径
3.本地的想对路径
-->
<!--图片占位符 alt="图片出错后显示的内容"-->
<!--图片提示符 titile="这是什么图"-->
<!--height="500px",wdith=""一般只写一个！-->
<!--border=15px-->
<img src=""> 
```

##### a标签：

```html
<!--1.超链接
2.作为锚点记录位置 href="#id"
3.打电话 na href="tel:123456" href="maito:2893313676@qq.com"
4.协议限定符 href="javascript" 后面可以运行javascript代码
src(Source)是指向物件的来源地址，是引入，在 img、script、iframe 等元素上使用； href(Hypertext Reference)是超文本引用，指向需要连结的地方，是与该页面有关联的，是引用，在 link和a 等元素上使用。src通常用作“拿取”（引入），href 用作 "连结前往"（引用）。-->

<a href="" target="_blank">
	<img src="">
</a>
```

##### 表单：

```html
<!--表单：能发送数据，向后端发送数据-->
<form method="get",action="">
    <input type="text" name="usename">
	<input type="password" name="password">
    <input type="submut">
</form>
<!--单选框-->
<form method="get",action="">
<!--checked="checked" 默认选中-->
    <input type="radio" name="star" value="小明" checked="checked">
	<input type="radio" name="star" value="小丽">
    <input type="radio" name="star" value=“小芳”>
    
</form>
<!--复选框-->
<form method="get",action="">
    <input type="checkbox" name="star" value="小明">
	<input type="checkbox" name="star" value="小丽">
    <input type="checkbox" name="star" value=“小芳”> 
</form>

<!--下拉菜单-->
<form method="get",action="">
 <slect>
	<option>beijing</option> 
    <option>shanghai</option>
    <option>tianjin</option>
  </slect>
</form>
```

## 2,总结：凡是带有inline的元素都有文字的特性(空格4px)

### 1.行级元素：inline

```html
<!--1.内容决定元素所在位置(不换行)
    2.不可以通过css改变宽高
-->
span strong em a del
```

### 2.块级元素：block

```html
<!--1.一个元素独占一行-->
<!--2.可以通过css改变宽高-->
div p ul li ol form address
```

### 3.行级块元素：inline-block

```html
<!--1.内容决定元素所在位置(不换行)
	2.可以通过css改变大小
```

### 4.行转块：

```css
span{
    display: block;
}
```

### 5.块转行

```css
div{
    display：inline;
}
```

## 3,自定义标签：用标签选择器来初始化标签

### 1.

```html
<em></em>
```

```css
em {
    font-style：normal;
    color:#f40;
    
}
```

### 2.

```html
<ul>
    
</ul>
```

```css
ul {
    list-style: none;
    padding: 0;
    margin: 0;
}
```

### 3.通配符选择器可以初始化一切代码：

```css
*{
    padding: 0;
    margin: 0;
    text-decoration: none;
    list-style: none;
}
```





