---
title: Vue项目中请求方式
date: 2021-07-30 12:24:25
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:
	- Vue
---

### 第一种，未封装

main.js文件

```js
axios.defaults.baseURL = 'http://vueshop.pixiv.download/api/private/v1/'
axios.interceptors.request.use(config => {
  console.log(config)
  config.headers.Authorization = window.sessionStorage.getItem('token')
  //在最后必须return config
  return config
})
//把这个包挂载到Vue的原型对象上,每一个组件都可以通过this，访问到$http从而发起axios请求，直接this.$http
Vue.prototype.$http = axios
```

> 然后this.$http可以全局使用。

.vue文件

```js
    async getRightSList(){
         const {data:res}  = await this.$http.get('rights/list')
         if(res.meta.status !== 200) {
             return this.$message.error('获取数据失败！')
         }
         this.rightsList = res.data
         console.log(this.rightsList)
        }
```

### 第二种，方法单独封装到api文件

request.js文件

```js
import axios from 'axios'

//配置请求的根路径
axios.defaults.withCredentials = false //cookie跨域
const request = axios.create({
    baseURL: 'http://vueshop.pixiv.download/api/private/v1/',
    // request timeout
    timeout: 5000 
  })
```

api.js文件

```js
import request from '../utils/request'
export async function getToken(options) {
  const result = await request.post('login',options)
  return result
}
```

简化

```js
import request from '../utils/request'
export async function getToken(options) {
  return await request.post('login',options)
}
```

.vue文件

```js
import { getToken } from "../api/login";
getToken(this.loginForm).then((res) => {
          console.log(res);
        });
```

### 第三种，方法封装到store里面

