---
title: Layout 布局
date: 2021-03-07 08:53:36
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue电商
tags:	
	 - Vue电商
	 - Element-Ui
---

## Layout 布局

通过基础的 24 分栏，迅速简便地创建布局。**即一行有二十四列**。可以理解为一个el-row元素有24个el-col元素。

### 基础使用的示例：

```html
 <el-table-column type="expand">
                 <template slot-scope="scope">
                     <!-- pre是进行对应的美化，childern下的内容就是该 行角色的所有权限 -->
                     <!-- 一行有二十四列 -->
                     <el-row v-for="(item1) in scope.row.children" :key="item1.id">
                         <!-- 渲染一级权限 -->
                         <el-col :span="5">
                             <el-tag>
                             {{item1.authName}}
                            </el-tag>
                         </el-col>
                         <!-- 渲染二级和三级权限 -->
                         <el-col :span="19"></el-col>
                     </el-row>
                     <pre>
                        {{scope.row}}
                     </pre>
                 </template>
  </el-table-column>
```

抽离后：5+19 =24

```html
<el-row>
    <el-col :span="5"></el-col>
    <el-col :span="19"></el-col>
</el-row>
```

