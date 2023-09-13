---
title: 三级for循环
date: 2021-03-07 09:52:13
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:
	- Vue电商
	- Vue
---

## 三级for循环

应用以下数据结构：children嵌套。

[![6KPxBV.png](https://s3.ax1x.com/2021/03/07/6KPxBV.png)](https://imgtu.com/i/6KPxBV)

### 示例

```html
        <!-- 角色列表区域 -->
        <el-table :data="rolelist" border stripe>
            <!-- 展开列
             -->
             <el-table-column type="expand">
                 <template slot-scope="scope">
                     <!-- pre是进行对应的美化，childern下的内容就是该 行角色的所有权限 -->
                     <!-- 一行有二十四列 -->
                     <el-row :class="['bdbottom',i1 === 0 ? 'bdtop':'','vcenter']" v-for="(item1,i1) in scope.row.children" :key="item1.id">
                         <!-- 渲染一级权限 -->
                         <el-col :span="5">
                             <el-tag> {{item1.authName}}</el-tag>
                             <i class="el-icon-caret-right"></i>
                         </el-col>
                         <!-- 渲染二级和三级权限 -->
                         <el-col :span="19">
                             <!-- 通过for循环，嵌套渲染二级权限 -->
                             <el-row :class="[i2 === 0 ? '':'bdtop','vcenter']" v-for="(item2,i2) in item1.children" :key="item2.id">
                                 <!-- 二级权限 -->
                                <el-col :span="6">
                                    <el-tag type="success">{{item2.authName}}</el-tag>
                                    <i class="el-icon-caret-right"></i>
                                </el-col >
                                <!-- 三级权限 -->
                                <el-col :span="18" >
                                    <el-tag type="warning" v-for="(item3,i3) in item2.children" :key="item3.id">{{item3.authName}}</el-tag>
                                </el-col>
                             </el-row>
                         </el-col>
                     </el-row>
                     <pre>
                        {{scope.row}}
                     </pre>
                 </template>
             </el-table-column>
            <!-- 索引列 -->
            <el-table-column type="index" label="序号"></el-table-column>
            <el-table-column label="角色名称" prop="roleName"></el-table-column>
            <el-table-column label="角色描述" prop="roleDesc"></el-table-column>
            <el-table-column label="操作" prop="level" width="300px">
                <template slot-scope="scope">
                    <el-button size="mini" type="primary" icon="el-icon-edit">编辑</el-button>
                    <el-button size="mini" type="danger" icon="el-icon-delete">删除</el-button>
                    <el-button size="mini" type="warning" icon="el-icon-setting">分配权限</el-button>
                </template>
            </el-table-column>
        </el-table>
```

> 注意：v-for作用是遍历，可以理解为标签赋值(个数由数据的个数而定)，注意遍历的对象。以上示例三次遍历的对象分别是两个row标签和一个tag标签，则复制了多个row标签，tag标签，对应请求来的的数据。

