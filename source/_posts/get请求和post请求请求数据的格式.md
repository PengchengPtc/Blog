---
title: get请求和post请求请求数据的格式
date: 2022-03-29 09:59:47
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:
	- Vue
---

# 请求格式(get、post)

## 1.params

```js
// 获取分页数据
export function getRepairReport(data) {
  return request({
    url: '/app/repairreport/list',
    method: 'post',
    params: data,
  })
}
```

```js
      applyParams: {
        t: new Date().getTime(),
        page: 1,
        limit: 10,
        totalPage: 0,
        key: '',
      },
```

[![qy9pD0.png](https://s1.ax1x.com/2022/03/29/qy9pD0.png)](https://imgtu.com/i/qy9pD0)

get同理

```js
export function getCarParams(data) {
  return request({
    url: '/app/car/select',
    method: 'get',
    params:data
  })
}
```

## 2.data

### 1.json

```js
  // 提交表单
  export function submitDataFrom(data) {
    return request({
      url: '/app/repairreport/save',
      method: 'post',
      data:data
    })
  }
```

[![qy9hIU.png](https://s1.ax1x.com/2022/03/29/qy9hIU.png)](https://imgtu.com/i/qy9hIU)

### 2.formdata

```js
 // 提交表单
  export function submitDataFrom(data) {
    return request({
      url: '/app/repairreport/save',
      method: 'post',
      data:qs.stringify(data)
    })
  }
```

[![qyCnzj.png](https://s1.ax1x.com/2022/03/29/qyCnzj.png)](https://imgtu.com/i/qyCnzj)

## 3.直接拼接在路径

```js
// 查询详情
export function searchRepairReport(id) {
  return request({
    url: `/app/repairreport/${id}`,
    method: 'post',
  })
}
```

[![qyCDw6.png](https://s1.ax1x.com/2022/03/29/qyCDw6.png)](https://imgtu.com/i/qyCDw6)

