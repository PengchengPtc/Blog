---
title: CSS_引入方式
date: 2021-01-25 09:18:15
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: CSS
tags:
	- CSS
---

## CSS引入方式：

### 1.行间样式：

```html
<div style="height:100px width:100px background-color:red">
    
</div>
```

### 2.页面级CSS:

```html
<head>
    <style type="text/css">
        div{
            height:100px
            width: 100px
            background-color: red
        }  
    </style>
</head>
```

### 3.外部CSS文件：

```css
/*href 属性的值可以是任何有效文档的相对或绝对 URL，包括片段标识符和 JavaScript 代码段。*/
创建index.css,在head标签里面写<link rel="stylesheet" type="text/css" href="index.css"></link>
   div{
            height:100px
            width: 100px
            background-color: red
        }  
```



