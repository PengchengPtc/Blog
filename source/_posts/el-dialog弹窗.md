---
title: el-dialog弹窗
date: 2021-03-06 18:26:56
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags:
	- Vue电商
	- Vue
---

## el-dialog弹窗

### Element-Ui官方：[Dialog 对话框](https://element.eleme.cn/#/zh-CN/component/dialog#dialog-dui-hua-kuang)

官方示例：

> ```html
> <el-dialog
>   title="提示"
>   :visible.sync="dialogVisible"
>   width="30%"
>   :before-close="handleClose">
>   <span>这是一段信息</span>
>   <span slot="footer" class="dialog-footer">
>     <el-button @click="dialogVisible = false">取 消</el-button>
>     <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
>   </span>
> </el-dialog>
> ```

### 点击按钮:用@click绑定点击事件

```html
<el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditDialog()"></el-button>
```

### 定义事件

```js
  showEditDialog() {
      console.log('点击了编辑事件',this.editdialogVisible)
  }
```

### 修改弹窗: :visible.sync="editdialogVisible"是定义弹窗是否隐藏，确定和取消都会触发弹窗隐藏。

```html
 <el-dialog
  title="修改用户"
  :visible.sync="editdialogVisible"
  width="50%">
  <span>这是一段信息</span>
  <span slot="footer" class="dialog-footer">
    <el-button @click="editdialogVisible = false">取 消</el-button>
    <el-button type="primary" @click="editdialogVisible = false">确 定</el-button>
  </span>
</el-dialog>
```

### data里面定义editdialogVisible

```html
<script>
    data() {
        return {
            //默认是false,即隐藏，点击事件可以修改其值
            editdialogVisible:false
        }
    }
</script>
```

### 完成点击事件:点击改变editdialogVisible 的布尔值，即可触发弹窗。

```js
  showEditDialog() {
      this.editdialogVisible = true
      console.log('点击了编辑事件',this.editdialogVisible)
  }
```

### 关闭对话框后清空数据

添加点击事件：@close="addCateDialogClosed"

以下是关闭窗口，清空表单和联级选择器的数据的示例。

```html
<template>
     <el-dialog
      title="添加分类"
      :visible.sync="addCatedialogVisible"
      width="50%"
      @close="addCateDialogClosed"
    >
         <!-- 添加分类表单 -->
    <el-form
      :model="addCateForm"
      :rules="addCateFormRules"
      ref="addCateFormRef"
      label-width="100px"
    >
      <el-form-item label="分类名称:" prop="cat_name">
        <el-input v-model="addCateForm.cat_name"></el-input>
      </el-form-item>
      <el-form-item label="父级分类:">
        <!-- options用来指定数据源 -->
        <!-- props用来指定配置对象 -->
          <el-cascader
    expand-trigger="hover"
    v-model="selectedKeys"
    :options="parentCateList"
    :props="cascaderProps"
    @change="parentCateChanged"
    clearable
    change-on-select>
      </el-cascader>
      </el-form-item>
    </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="addCatedialogVisible = false">取 消</el-button>
        <el-button type="primary" 
          @click="addCate">确 定</el-button
        >
      </span>
    </el-dialog>
</template>
<script>
	  //监听对话框的关闭事件，重置表单数据
    addCateDialogClosed() {
      this.$refs.addCateFormRef.resetFields()
      this.selectedKeys = []
      this.addCateForm.cat_level =0
      this.addCateForm.cat_pid =0
    }
</script>
```

