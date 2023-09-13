---
title: CSS_一些常用属性
date: 2021-01-25 09:20:50
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: CSS
tags:
	- CSS
---

### CSS常用属性：属性的值用时，可以直接菜鸟教程查

### 设置字体的属性：默认高度16px

```css
/*字体大小，设置的是高*/
font-size: 50px；
/*加粗,值可以写数字*/
font-weight:bolder；
/*斜体*/
font-style: italic;
/*乔布斯发明的字体*/
font-family: arial/cursive;
/*颜色:
1.英文单词（不用于开发）
2.颜色代码
3.颜色函数
*/
color: #ff4400
```

#### 颜色代码(十六进制)：红绿蓝拼接到一起

```css
r                            g                   b
00-ff                      00-ff               00-ff   
#000000 黑
#ff0000 红(满)
#00ff00 绿(满)
#0000ff 蓝(满)
/*保证每两位都是重复可以省些写成一个*/
#ff4400=>#f40 淘宝红
```

#### 颜色函数：0-25

```css
rgb(255,255,255)
```

### 盒子属性：

```css
/*复合属性*/
/*border-width border-style border-color*/
/*border-style:dashed*/
border:1px solid black;
/*每个边可以单独设置*/
border-left:1px solid black;
/*透明色*/
border-left-color: transparent;
```

