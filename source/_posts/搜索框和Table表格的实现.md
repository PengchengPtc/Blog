---
title: 搜索框和Table表格的实现
date: 2021-03-06 14:45:06
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:
	- Vue电商
	- Vue
---

### 添加搜索框，画Table表格

1. 搜索框：[Element-Ui中的input搜索框中的复合搜索框](https://element.eleme.cn/#/zh-CN/component/input)

   > ```html
   >   <el-input placeholder="请输入内容" v-model="input3" class="input-with-select">
   >     <el-select v-model="select" slot="prepend" placeholder="请选择">
   >       <el-option label="餐厅名" value="1"></el-option>
   >       <el-option label="订单号" value="2"></el-option>
   >       <el-option label="用户电话" value="3"></el-option>
   >     </el-select>
   >     <el-button slot="append" icon="el-icon-search"></el-button>
   >   </el-input>
   > ```

   删减后：并添加一个button按钮，实现搜索就是绑定一个获取数据的事件即可。

   > ```html
   >       <!-- 搜索与添加区域 -->
   >       <!-- 分栏间隔 -->
   >       <el-row :gutter="20">
   >         <el-col :span="7">
   >           <el-input placeholder="请输入内容" v-model="queryInfo.query" clearable @clear="getUserList">
   >           <el-button slot="append" icon="el-icon-search" @click="getUserList"></el-button>
   >           </el-input>
   >         </el-col>
   >         <el-col :span="4">
   >           <el-button type="primary" @click="addDialogVisible=true">添加用户</el-button>
   >         </el-col>
   >       </el-row>
   > ```
   >
   > 属性：clearable              是否可清空                 boolean                                        —                                false        
   >
   > ​			clear                   在点击由 `clearable` 属性生成的清空按钮时触发          —                           然后重新渲染
   >
   > Layout 布局:
   >
   > ```html
   > <el-row :gutter="20">
   >   <el-col :span="16"><div class="grid-content bg-purple"></div></el-col>
   >   <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
   > </el-row>
   > ```
   >
   > 实现效果：
   >
   > [![6nvKmQ.png](https://s3.ax1x.com/2021/03/06/6nvKmQ.png)](https://imgtu.com/i/6nvKmQ)
   >
   > 属性： span                 栅格占据的列数                            number                              —                                 24
   >
   > ​			gutter                栅格间隔                                      number                              —  
   >
   > 注：span可以表示元素的所占长度，gutter可以表示元素之间的间距。                                     

2. Table：[运用element的table表格组件](https://element.eleme.cn/#/zh-CN/component/table)

   > ```html
   >   <template>
   >     <el-table
   >       :data="tableData"
   >       style="width: 100%">
   >       <el-table-column
   >         prop="date"
   >         label="日期"
   >         width="180">
   >       </el-table-column>
   >       <el-table-column
   >         prop="name"
   >         label="姓名"
   >         width="180">
   >       </el-table-column>
   >       <el-table-column
   >         prop="address"
   >         label="地址">
   >       </el-table-column>
   >     </el-table>
   >   </template>
   > ```

   项目实战的代码：prop绑定拿来的数据，应用作用域插槽

   > ```html
   >       <el-table :data="userlist" border stripe>
   >         <el-table-column type="index" label="#"></el-table-column>
   >         <el-table-column label="姓名" prop="username"></el-table-column>
   >         <el-table-column label="邮箱" prop="email"></el-table-column>
   >         <el-table-column label="电话" prop="mobile"></el-table-column>
   >         <el-table-column label="角色" prop="role_name"></el-table-column>
   >         <el-table-column label="状态" prop="mg_state">
   >           <template slot-scope="scope">
   >             <!-- 拿到这一行的数据 -->
   >             <!-- {{scope.row}} -->
   >             <!-- {{ scope.row }} -->
   >             <el-switch v-model="scope.row.mg_state" @change="usesrStateChanged(scope.row)"></el-switch>
   >           </template>
   >         </el-table-column>
   >         <el-table-column label="操作">
   >           <template >
   >             <!-- 拿到这一行的数据 -->
   >             <!-- {{scope.row}} -->
   >             <!-- {{ scope.row }} -->
   >             <!-- 修改按钮 -->
   >             <el-button type="primary" icon="el-icon-edit" size="mini"></el-button>
   >             <!-- 删除按钮 -->
   >             <el-button type="danger" icon="el-icon-delete" size="mini"></el-button>
   >             <!-- 分配角色按钮 -->
   >             <el-tooltip effect="dark" content="分配角色" placement="top" :enterable='false'>
   >                    <el-button type="warning" icon="el-icon-setting" size="mini"></el-button>
   >            </el-tooltip>
   >           </template>
   >         </el-table-column>
   >       </el-table>
   > ```