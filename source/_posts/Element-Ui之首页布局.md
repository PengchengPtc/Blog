---
title: Element-Ui之首页布局
date: 2021-02-25 10:20:41
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:
	- Vue电商
	- Vue
---

### 首页布局：container容器。

```html
<el-container>
<!-- 头部区域 -->
  <el-header>Header</el-header>
<!-- 页面主体区域 -->
  <el-container>
 <!-- 侧边栏 -->
    <el-aside width="200px">Aside</el-aside>
 <!-- 右侧内容主题 -->
    <el-main>Main</el-main>
  </el-container>
</el-container>
```

### 左侧菜单布局：NavMenu导航菜单。

```html
<el-aside width="200px">
        <!-- 侧边栏菜单区域 -->
        <el-menu background-color="#333744" text-color="#fff" active-text-color="#ffd04b">
          <!-- 一级菜单 -->
          <el-submenu index="1">
            <!-- 一级菜单的模板区域 -->
            <template slot="title">
              <!-- 图标 -->
              <i class="el-icon-location"></i>
              <!-- 文本 -->
              <span>导航一</span>
            </template>
            <!-- 二级菜单 -->
            <el-menu-item index="1-4-1">
              <template slot="title">
                <!-- 图标 -->
                <i class="el-icon-location"></i>
                <!-- 文本 -->
                <span>导航一</span>
              </template>
            </el-menu-item>
          </el-submenu>
        </el-menu>
      </el-aside>
```



