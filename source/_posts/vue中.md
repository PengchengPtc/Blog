---
title: vue中“$”未定义
date: 2021-09-01 11:30:44
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:
	- Vue
---

首先下载jQuery

```javascript
npm install jquery --save
```

然后在main.js中

```javascript
import $ from 'jquery'

window.jQuery = $
window.$ = $
```

这样组件里面的$就可以正常使用了

