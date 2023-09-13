---
title: 生命周期函数和Vue监听
date: 2021-08-18 10:18:43
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:
	- Vue
---

### 生命周期函数和vue监听

```js
 // 页面渲染之前,多次跳转到同一个页面，created()方法只会执行一次，如果要多次执行就要vue的监听
  created() {
    this.init();
  },
  //监听路由跳转,只要路由改变就调用
  watch: {
    $route(to,from) {
      this.init()
    }
  },
```



