---
title: 点击按钮的传参和Form表单的验证
date: 2021-03-06 19:32:12
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Vue
tags: 	
	- Vue电商
	- Vue
---

## 点击按钮的传参，Form表单的验证，提交表单，删除表单

### 点击的按钮的传参：showEditDialog(scope.row.id)，加(),拿到参数。

```html
        <el-table-column label="操作">
          <template slot-scope="scope">
            <!-- 拿到这一行的数据 -->
            <!-- {{scope.row}} -->
            <!-- {{ scope.row }} -->
            <!-- 修改按钮 -->
            <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditDialog(scope.row.id)"></el-button>
            <!-- 删除按钮 -->
            <el-button type="danger" icon="el-icon-delete" size="mini"></el-button>
            <!-- 分配角色按钮 -->
            <el-tooltip effect="dark" content="分配角色" placement="top" :enterable='false'>
                   <el-button type="warning" icon="el-icon-setting" size="mini"></el-button>
           </el-tooltip>
          </template>
        </el-table-column>
```

### 在定义事件的位置接受参数:用id接收,在data里面定义editForm

```js
  async showEditDialog(id) {
      
      console.log('点击了编辑事件',this.editdialogVisible,id)
      const {data: res} = await this.$http.get('users/'+id)
      if(res.meta.status !== 200) {
        return this.$message.error('查询用户信息失败')
      }
      this.editForm =res.data
      console.log(this.editForm)
      this.editdialogVisible = true
  }
```

```html
<script>
    data() {
        return {
            //只是一个对象因为url后面接id了
            editForm: {

           },
        }
    }
</script>
```

### Form表单的验证：

[参考Element-Ui的官方组件](https://element.eleme.cn/#/zh-CN/component/form)

1. 官方示例代码

   > ```html
   > <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
   >   <el-form-item label="活动名称" prop="name">
   >     <el-input v-model="ruleForm.name"></el-input>
   >   </el-form-item>
   >  <el-form>
   > ```

2. 稍加修饰

   > ```html
   > <el-form :model="editForm" :rules="editFormRules" ref="ruleFormRef" label-width="70px">
   > <el-form-item label="用户名" prop="name">
   >  <el-input v-model="editForm.username" disabled></el-input>
   > </el-form-item>
   > <el-form-item label="邮箱" prop="email">
   >  <el-input v-model="editForm.email"></el-input>
   > </el-form-item>
   > <el-form-item label="手机" prop="mobile">
   >  <el-input v-model="editForm.mobile"></el-input>
   > </el-form-item>
   > </el-form>
   > ```
   >
   > 1.model绑定数据，v-model实现双向绑定，绑定对应的字段。
   >
   > 2.rules="editFormRules"是绑定验证规则的名称
   >
   > 3.prop="name"是绑定验证规则的，只有输入框有验证规则才能用到，对应的字段。
   >
   > 4.disabled是表示禁用状态，禁止输入。
   >
   > 5.label-width="70px"文本最大宽度。
   >
   > 6.ref="ruleFormRef是使用默认的方法。后面会用到为实现修改表单的重置操作,即验证重置。

3. 定义验证规则：

   > ```js
   > <script>
   >  data() {
   >      return {
   >          //只是一个对象因为url后面接id了
   >          //双向绑定的输入框的内容，editForm是名称，里面的属性是具体的字段
   >      editForm: {
   > 	    username:'',
   >         password:'',
   >         email: '',
   >         mobile: ''
   >      },
   >      editFormRules:{
   >      email:[
   >        { required: true, message: '请输入用户邮箱', trigger: 'blur' },
   >        { validator: checkEmail, trigger: 'blur' }
   >       ],
   >       mobile:[
   >        { required: true, message: '请输入用户手机', trigger: 'blur' },
   >        { validator: checkMobile, trigger: 'blur' }
   >      ]
   >    }
   >      }
   >  }
   > </script>
   > ```
   >
   > 注：验证规则checkEmail，checkMobile，是需要定义的，完整的data如下
   >
   > ```js
   > data() {
   >  //验证邮箱的规则
   >  var checkEmail = (rule, value, cb) => {
   >  const regEmail = /^\w+@\w+(\.\w+)+$/
   >  if (regEmail.test(value)) {
   >    return cb()
   >  }
   >  //返回一个错误提示
   >  cb(new Error('请输入合法的邮箱'))
   > }
   > //验证手机号码的规则
   > var checkMobile = (rule, value, cb) => {
   >  const regMobile = /^1[34578]\d{9}$/
   >  if (regMobile.test(value)) {
   >    return cb()
   >  }
   >  //返回一个错误提示
   >  cb(new Error('请输入合法的手机号码'))
   > }
   >  return {
   >    //获取用户列表的参数对象
   >    queryInfo: {
   >      query: "",
   >      // 当前的页数
   >      pagenum: 1,
   >      //当前每页显示多少条数据
   >      pagesize: 2,
   >    },
   >    userlist: [],
   >    total: 0,
   >    // 控制添加用户对话框的添加与隐藏
   >    addDialogVisible:false,
   >    // 添加用户的表单数据
   >    addForm: {
   >        username:'',
   >        password:'',
   >        email: '',
   >        mobile: ''
   >    },
   >    // 添加表单的验证规则的对象
   >    addFormRules: {
   >        username: [
   >          { required: true, message: '请输用户名名称', trigger: 'blur' },
   >          { min: 3, max: 5, message: '长度在 3 到 10 个字符', trigger: 'blur' }
   >        ],
   >        password: [
   >          { required: true, message: '请输入密码', trigger: 'blur' },
   >          { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
   > 
   >        ],
   >        email: [
   >           { required: true, message: '请输入邮箱', trigger: 'blur' },
   >           { validator:checkEmail, message: '邮箱格式不正确，请重新输入', trigger: 'blur'}
   >        ],
   >        mobile: [
   >           { required: true, message: '请输入电话', trigger: 'blur' },
   >           { validator:checkMobile, message: '手机号码不正确，请重新输入', trigger: 'blur'}
   >        ]
   >    },
   >    //定义修改对话框的显示和隐藏
   >    editdialogVisible: false,
   >    //查询到的用户信息的对象
   >    editForm: {
   > 
   >    },
   >    // 修改表单的验证规则对象
   >    editFormRules:{
   >      email:[
   >        { required: true, message: '请输入用户邮箱', trigger: 'blur' },
   >        { validator: checkEmail, trigger: 'blur' }
   >      ],
   >       mobile:[
   >        { required: true, message: '请输入用户手机', trigger: 'blur' },
   >        { validator: checkMobile, trigger: 'blur' }
   >      ]
   >    }
   >  };
   > },
   > ```

4. 具体代码如下：Users.vue

   > ```html
   > <template>
   >   <div>
   >     <!-- <h3>面包屑导航区域</h3> -->
   >     <el-breadcrumb separator="/">
   >       <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
   >       <el-breadcrumb-item>用户管理</el-breadcrumb-item>
   >       <el-breadcrumb-item>用户列表</el-breadcrumb-item>
   >     </el-breadcrumb>
   > 
   >     <!-- 卡片视图区域 -->
   >     <el-card class="box-card">
   >       <!-- 搜索与添加区域 -->
   >       <!-- 分栏间隔 -->
   >       <el-row :gutter="20">
   >         <el-col :span="7">
   >           <el-input placeholder="请输入内容" v-model="queryInfo.query" clearable @clear="getUserList">
   >             <el-button slot="append" icon="el-icon-search" @click="getUserList"></el-button>
   >           </el-input>
   >         </el-col>
   >         <el-col :span="4">
   >           <el-button type="primary" @click="addDialogVisible=true">添加用户</el-button>
   >         </el-col>
   >       </el-row>
   >       <!-- 用户列表区域 -->
   > 
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
   >           <template slot-scope="scope">
   >             <!-- 拿到这一行的数据 -->
   >             <!-- {{scope.row}} -->
   >             <!-- {{ scope.row }} -->
   >             <!-- 修改按钮 -->
   >             <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditDialog(scope.row.id)"></el-button>
   >             <!-- 删除按钮 -->
   >             <el-button type="danger" icon="el-icon-delete" size="mini"></el-button>
   >             <!-- 分配角色按钮 -->
   >             <el-tooltip effect="dark" content="分配角色" placement="top" :enterable='false'>
   >                    <el-button type="warning" icon="el-icon-setting" size="mini"></el-button>
   >            </el-tooltip>
   >           </template>
   >         </el-table-column>
   >       </el-table>
   >       <!-- 分页区域 -->
   >       <!-- layout字符串，展示功能 -->
   >        <el-pagination
   >       @size-change="handleSizeChange"
   >       @current-change="handleCurrentChange"
   >       :current-page="queryInfo.pagenum"
   >       :page-sizes="[1, 2, 5, 10]"
   >       :page-size="queryInfo.pagesize"
   >       layout="total, sizes, prev, pager, next, jumper"
   >       :total="400">
   >     </el-pagination>
   >     </el-card>
   > <!-- 添加用户的对话框 -->
   > <el-dialog
   >   title="添加用户"
   >   :visible.sync="addDialogVisible"
   >   width="50%"
   >   @close="addDialogClosed"
   >   >
   >   <!-- 内容主体区域 -->
   >   <el-form :model="addForm" :rules="addFormRules" ref="addFormRef" label-width="70px">
   >   <el-form-item label="用户名" prop="username">
   >     <el-input v-model="addForm.username"></el-input>
   >   </el-form-item>
   >   <el-form-item label="密码" prop="password">
   >     <el-input v-model="addForm.password"></el-input>
   >   </el-form-item>
   >   <el-form-item label="邮箱" prop="email">
   >     <el-input v-model="addForm.email"></el-input>
   >   </el-form-item>
   >   <el-form-item label="电话" prop="mobile">
   >     <el-input v-model="addForm.mobile"></el-input>
   >   </el-form-item>
   >   </el-form>
   >   <!-- 底部区域 -->
   >   <span slot="footer" class="dialog-footer">
   >     <el-button @click="addDialogVisible = false">取 消</el-button>
   >     <el-button type="primary" @click="addUser">确 定</el-button>
   >   </span>
   > </el-dialog>
   > <!-- 修改用户对话框 -->
   >   <el-dialog
   >   title="修改用户"
   >   :visible.sync="editdialogVisible"
   >   width="50%">
   >   <el-form :model="editForm" :rules="editFormRules" ref="ruleFormRef" label-width="70px">
   >   <el-form-item label="用户名" prop="name">
   >     <el-input v-model="editForm.username" disabled></el-input>
   >   </el-form-item>
   >    <el-form-item label="邮箱" prop="email">
   >     <el-input v-model="editForm.email"></el-input>
   >   </el-form-item>
   >   <el-form-item label="手机" prop="mobile">
   >     <el-input v-model="editForm.mobile"></el-input>
   >   </el-form-item>
   >   </el-form>
   >   <span slot="footer" class="dialog-footer">
   >     <el-button @click="editdialogVisible = false">取 消</el-button>
   >     <el-button type="primary" @click="editdialogVisible = false">确 定</el-button>
   >   </span>
   > </el-dialog>
   >   </div>
   > </template>
   > 
   > <script>
   > export default {
   >   data() {
   >     //验证邮箱的规则
   >     var checkEmail = (rule, value, cb) => {
   >     const regEmail = /^\w+@\w+(\.\w+)+$/
   >     if (regEmail.test(value)) {
   >       return cb()
   >     }
   >     //返回一个错误提示
   >     cb(new Error('请输入合法的邮箱'))
   >   }
   >   //验证手机号码的规则
   >   var checkMobile = (rule, value, cb) => {
   >     const regMobile = /^1[34578]\d{9}$/
   >     if (regMobile.test(value)) {
   >       return cb()
   >     }
   >     //返回一个错误提示
   >     cb(new Error('请输入合法的手机号码'))
   >   }
   >     return {
   >       //获取用户列表的参数对象
   >       queryInfo: {
   >         query: "",
   >         // 当前的页数
   >         pagenum: 1,
   >         //当前每页显示多少条数据
   >         pagesize: 2,
   >       },
   >       userlist: [],
   >       total: 0,
   >       // 控制添加用户对话框的添加与隐藏
   >       addDialogVisible:false,
   >       // 添加用户的表单数据
   >       addForm: {
   >           username:'',
   >           password:'',
   >           email: '',
   >           mobile: ''
   >       },
   >       // 添加表单的验证规则的对象
   >       addFormRules: {
   >           username: [
   >             { required: true, message: '请输用户名名称', trigger: 'blur' },
   >             { min: 3, max: 5, message: '长度在 3 到 10 个字符', trigger: 'blur' }
   >           ],
   >           password: [
   >             { required: true, message: '请输入密码', trigger: 'blur' },
   >             { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
   > 
   >           ],
   >           email: [
   >              { required: true, message: '请输入邮箱', trigger: 'blur' },
   >              { validator:checkEmail, message: '邮箱格式不正确，请重新输入', trigger: 'blur'}
   >           ],
   >           mobile: [
   >              { required: true, message: '请输入电话', trigger: 'blur' },
   >              { validator:checkMobile, message: '手机号码不正确，请重新输入', trigger: 'blur'}
   >           ]
   >       },
   >       //定义修改对话框的显示和隐藏
   >       editdialogVisible: false,
   >       //查询到的用户信息的对象
   >       editForm: {
   > 
   >       },
   >       // 修改表单的验证规则对象
   >       editFormRules:{
   >         email:[
   >           { required: true, message: '请输入用户邮箱', trigger: 'blur' },
   >           { validator: checkEmail, trigger: 'blur' }
   >         ],
   >          mobile:[
   >           { required: true, message: '请输入用户手机', trigger: 'blur' },
   >           { validator: checkMobile, trigger: 'blur' }
   >         ]
   >       }
   >     };
   >   },
   >   created() {
   >     this.getUserList();
   >   },
   >   methods: {
   >     //get请求参数拼接用params
   >     async getUserList() {
   >       const { data: res } = await this.$http.get("users", {
   >         params: this.queryInfo,
   >       });
   >       if (res.meta.status !== 200)
   >         return this.$message.error("获取用户列表失败！");
   >       this.userlist = res.data.users;
   >       this.total = res.data.total;
   >       console.log(res);
   >     },
   >     //监听pagesize改变的事件
   >   handleSizeChange(newSize) {
   >     console.log(newSize)
   >     this.queryInfo.pagesize = newSize
   >     this.getUserList()
   >   },
   >   //监听 页码值，改变的事件
   >   handleCurrentChange(newPage){
   >     console.log(newPage)
   >     this.queryInfo.pagenum = newPage
   >     // 重新获取数据
   >     this.getUserList()
   > 
   >   },
   >   // 监听switch开关状态的改变
   >   async usesrStateChanged(userinfo) {
   >         console.log(userinfo)
   >         const {data:res} = await this.$http.put(`users/${userinfo.id}/state/${userinfo.mg_state}`)
   >   if (res.meta.status !== 200) {
   >     userinfo.mg_state = !userinfo.mg_state
   >     return this.$message.error('更新用户状态失败')
   >   }
   >   console.log(res)
   >   this.$message.success('更新用户状态成功')
   >   },
   >   //监听用户对话框的关闭事件
   >   addDialogClosed(){
   >       //对话框关闭之后，重置表达
   >       this.$refs.addFormRef.resetFields();
   >     },
   >   // 点击按钮，添加新用户
   >   addUser(){
   >       //点击确定按钮，添加新用户
   >       //调用validate进行表单验证
   >       this.$refs.addFormRef.validate( async valid => {
   >           if(!valid) return this.$message.error("请填写完整用户信息");
   >           //发送请求完成添加用户的操作
   >           const {data:res} = await this.$http.post("users",this.addForm)
   >           //判断如果添加失败，就做提示
   >           if (res.meta.status !== 201)
   >               return this.$message.error('添加用户失败')
   >           //添加成功的提示
   >           this.$message.success("添加用户成功")
   >           //关闭对话框
   >           this.addDialogVisible = false
   >           //重新请求最新的数据
   >           this.getUserList()
   >       })
   >   },
   >   //展示编辑用户的对话框
   >   async showEditDialog(id) {
   >       
   >       console.log('点击了编辑事件',this.editdialogVisible,id)
   >       const {data: res} = await this.$http.get('users/'+id)
   >       if(res.meta.status !== 200) {
   >         return this.$message.error('查询用户信息失败')
   >       }
   >       this.editForm =res.data
   >       console.log(this.editForm)
   >       this.editdialogVisible = true
   >   }
   >   }
   > };
   > </script>
   > 
   > <style lang="less" scoped>
   > </style>
   > ```

### 修改用户表单的重置操作

- 绑定close点击事件: @close='editDialogClosed'

  > ```html
  > <!-- 修改用户对话框 -->
  >   <el-dialog
  >   title="修改用户"
  >   :visible.sync="editdialogVisible"
  >   width="50%"
  >   @close='editDialogClosed'
  >   >
  >   <el-form :model="editForm" :rules="editFormRules" ref="editFormRef" label-width="70px">
  >   <el-form-item label="用户名" prop="name">
  >     <el-input v-model="editForm.username" disabled></el-input>
  >   </el-form-item>
  >    <el-form-item label="邮箱" prop="email">
  >     <el-input v-model="editForm.email"></el-input>
  >   </el-form-item>
  >   <el-form-item label="手机" prop="mobile">
  >     <el-input v-model="editForm.mobile"></el-input>
  >   </el-form-item>
  >   </el-form>
  >   <span slot="footer" class="dialog-footer">
  >     <el-button @click="editdialogVisible = false">取 消</el-button>
  >     <el-button type="primary" @click="editdialogVisible = false">确 定</el-button>
  >   </span>
  > </el-dialog>
  > ```

- 定义事件：

  ```js
   //监听修改用户对话框的关闭事件
    editDialogClosed() {
      this.$refs.editFormRef.resetFields()
    }
  ```

  ### 提交的表单的预验证：要应用ref="ruleFormRef"

  1. 为确定绑定点击事件：@click="editUseInfo"

  ```html
    <el-dialog
    title="修改用户"
    :visible.sync="editdialogVisible"
    width="50%"
    @close='editDialogClosed'
    >
    <el-form :model="editForm" :rules="editFormRules" ref="editFormRef" label-width="70px">
    <el-form-item label="用户名" prop="name">
      <el-input v-model="editForm.username" disabled></el-input>
    </el-form-item>
     <el-form-item label="邮箱" prop="email">
      <el-input v-model="editForm.email"></el-input>
    </el-form-item>
    <el-form-item label="手机" prop="mobile">
      <el-input v-model="editForm.mobile"></el-input>
    </el-form-item>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button @click="editdialogVisible = false">取 消</el-button>
      <el-button type="primary" @click="editUseInfo">确 定</el-button>
    </span>
  </el-dialog>
    </div>
  ```

  ​	2.定义事件

  ```js
   //修改用户并提交,打印结果为true则验证成功，否则则失败
    editUseInfo() {
      this.$refs.editFormRef.validate(valid=>{
        console.log(valid)
      })
    }
  ```

  ### 提交表单完成用户信息的修改：发请求，要携带email和mobile，不拼接在url上

  ```js
    //修改用户并提交
   editUseInfo() {
      this.$refs.editFormRef.validate(async  valid=>{
        // console.log(valid)
        // 如果为false,则直接return
      if (!valid) return
        //成功则发起修改用户信息的数据请求，提交数据
       const {data:res} = await this.$http.put('users/'+this.editForm.id,{email:this.editForm.email,mobile:this.editForm.mobile})
       if(res.meta.status !== 200) {
         return this.$message.error('更新用户信息失败！')
       }
       //关闭对话框
       this.editdialogVisible = false
       //刷新数据列表
       this.getUserList()
       //提示修改成功
       this.$message.success('更新用户信息成功')
  
      })
    }
  ```

  ### 删除表单操作

  1. 先提示是否要删除：[应用element-Ui的官方组件](https://element.eleme.cn/#/zh-CN/component/message-box)

     > ```js
     > this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
     >           confirmButtonText: '确定',
     >           cancelButtonText: '取消',
     >           type: 'warning'
     >         })
     > ```
     >
     > 修改后：这个err，return给了confirmRestult变量，该变量接收了
     >
     > ```js
     >   const confirmResult = await this.$confirm('此操作将永久删除该用户, 是否继续?', '提示', {
     >           confirmButtonText: '确定',
     >           cancelButtonText: '取消',
     >           type: 'warning'
     >           // catch是捕获错误的
     >         }).catch(err =>
     >         err)
     > ```
     >
     > 具体的事件
     >
     > ```js
     >  async removeUserById(id) {
     >     console.log(id)
     >     //弹框提示是否提示
     >      const confirmResult = await this.$confirm('此操作将永久删除该用户, 是否继续?', '提示', {
     >           confirmButtonText: '确定',
     >           cancelButtonText: '取消',
     >           type: 'warning'
     >           // catch是捕获错误的
     >         }).catch(err =>
     >         err)
     >         // 如果用户确定删除，则返回值为字符串confirm
     >         // 如果用户取消了删除，则返回值为字符串cancel
     >         console.log(confirmResult )
     >         if (confirmResult !== 'confirm' ){
     >           return this.$message.info('已经取消删除')
     >         }
     >         console.log(确定删除)
     >   }
     > ```
     >
     > 前提是事件和按钮绑定
     >
     > ```html
     > <el-button type="danger" icon="el-icon-delete" size="mini"  @click="removeUserById(scope.row.id)"></el-button>
     > ```

  ### 发请求删除用户

  ```js
   async removeUserById(id) {
      console.log(id)
      //弹框提示是否提示
       const confirmResult = await this.$confirm('此操作将永久删除该用户, 是否继续?', '提示', {
            confirmButtonText: '确定',
            cancelButtonText: '取消',
            type: 'warning'
            // catch是捕获错误的
          }).catch(err =>
          err)
          // 如果用户确定删除，则返回值为字符串confirm
          // 如果用户取消了删除，则返回值为字符串cancel
          console.log(confirmResult)
          if (confirmResult !== 'confirm' ){
            return this.$message.info('已经取消删除')
          }
          console.log('确定了删除')
       
       //删除用户的操作
         const {data:res} = await this.$http.delete('users/' +id)
         if(res.meta.status !== 200){
           return this.$message.error('删除用户失败！')
         }
         this.$message.success('删除用户成功')
         //重新刷新列表
         this.getUserList()
    }
  ```

  

  

