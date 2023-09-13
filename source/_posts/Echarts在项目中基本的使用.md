---
title: Echarts在项目中基本的使用
date: 2021-03-05 15:28:15
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:
	- Vue电商
	- Vue
---

## Echarts在项目中的基本使用:参考官方网站：[Echarts](https://echarts.apache.org/zh/tutorial.html#5%20%E5%88%86%E9%92%9F%E4%B8%8A%E6%89%8B%20ECharts)

### 1.导入echarts

指令如下：

```js
import  echarts from 'echarts'
```

以上指令只只适用5.0版本以下的Echats

以下提供解决方案：

1. > 引入echarts的地方改为
   >
   > ```js
   > import * as echarts from 'echarts'
   > ```

2. > webpack的DefinePlugin里加入如下字段
   >
   > ```js
   > // 此处根据情况自行修改，结果为boolean就行，true的情况下会多一些日志信息
   > '__DEV__': process.env.node_env === 'dev' 
   > ```
   >
   > 或者
   >
   > ```bash
   > npm un echarts && npm i -E echarts@3.7.2 zrender@3.6.3
   > ```

### *2.为Echarts准备一个具有大小(宽高)的Dom*

```js
<div id="main" style="width: 600px;height:400px;"></div>
```

### *3.基于准备好的dom，初始化echarts实例*

```js
var myChart = echarts.init(document.getElementById('main'));
```

### 4.准备数据和配置项

```js
var option = {
            title: {
                text: 'ECharts 入门示例'
            },
            tooltip: {},
            legend: {
                data:['销量']
            },
            xAxis: {
                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        };

```

### 5.*展示数据:即调用里面的myCharts函数*

```js
myChart.setOption(option);
```

### 6.完整代码：.vue文件

```html
<template>
    <div>
    <!-- <h3>面包屑导航区域</h3> -->
    <el-breadcrumb separator="/">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>数据统计</el-breadcrumb-item>
      <el-breadcrumb-item>数据报表</el-breadcrumb-item>
    </el-breadcrumb>
    <!-- 卡片视图区域 -->
    <el-card>
        <!-- 2.为Echarts准备一个具有大小(宽高)的Dom -->
        <div id="main" style="width: 600px;height:400px;"></div>
    </el-card>
    </div>
</template>
<script>
// 1.导入echarts
import * as echarts from 'echarts'


export default {
    data() {
        return{

        }
    },
    created(){

    },
    //此时，页面上的元素已经被渲染完毕了
    mounted() {
        // 3.基于准备好的dom，初始化echarts实例
        var myChart = echarts.init(document.getElementById('main'));

        // 4.准备数据和配置项
         var option = {
            title: {
                text: 'ECharts 入门示例'
            },
            tooltip: {},
            legend: {
                data:['销量']
            },
            xAxis: {
                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        };

        //5.展示数据:即调用里面的myCharts函数
       myChart.setOption(option);
    },
    methods: {

    }
}
</script>
<style lang="less" scoped>


</style>
```

### 从后台调取数据进行展示：折线图

```js
<template>
    <div>
    <!-- <h3>面包屑导航区域</h3> -->
    <el-breadcrumb separator="/">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>数据统计</el-breadcrumb-item>
      <el-breadcrumb-item>数据报表</el-breadcrumb-item>
    </el-breadcrumb>
    <!-- 卡片视图区域 -->
    <el-card>
        <!-- 2.为Echarts准备一个具有大小(宽高)的Dom -->
        <div id="main" style="width: 750px;height:400px;"></div>
    </el-card>
    </div>
</template>
<script>
// 1.导入echarts
import * as echarts from 'echarts'
//用于数据合并
import _ from 'lodash'

export default {
      data() {
    return {
      //需要跟请求的折线图数据合并的options
      options: {
        title: {
          text: '用户来源'
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross',
            label: {
              backgroundColor: '#E9EEF3'
            }
          }
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: [
          {
            boundaryGap: false
          }
        ],
        yAxis: [
          {
            type: 'value'
          }
        ]
      }
    }
  },
    created(){

    },
    //此时，页面上的元素已经被渲染完毕了
   async mounted() {
        // 3.基于准备好的dom，初始化echarts实例
        var myChart = echarts.init(document.getElementById('main'));


        const {data: res} = await this.$http.get('reports/type/1')
        if(res.meta.status !== 200) {
            return this.$message.error('获取折线图数据失败')
        }


        // 4.准备数据和配置项
        // 合并数据
        const result = _.merge(res.data,this.options)
        
        //5.展示数据:即调用里面的myCharts函数
       myChart.setOption(result);
    },
    methods: {

    }
}
</script>
<style lang="less" scoped>


</style>
```

> 1. 将原先的options删除
> 2. 直接展示调取的res.data，没有鼠标跟随效果，故不可行
> 3. 故要添加新的options,目的是实现鼠标跟随效果
> 4.  要用lodash合并res.data和新的options，命名为result，成为最终的options



