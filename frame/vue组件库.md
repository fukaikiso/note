# `VUE`组件库

各大互联网企业或个人研发的整套基于vue的自定义组件**库**。

`ElementUI` 饿了么团队研发的基于PC的`vue`组件库。

`MintUI` 饿了么团队研发的基于移动端的`vue`组件库。

`Vant`  有赞团队推出的移动端`vue`组件库。



## `ElementUI`

Element，一套为开发者、设计师和产品经理准备的基于 Vue 2.0 的桌面端组件库。

### 搭建`ElementUI`基础环境（基于脚手架）

基础环境：安装node   配置淘宝源   安装vuecli   

```shell
# 设置淘宝源，下载时速度快
npm config set registry http://registry.npm.taobao.org/
# 安装脚手架，安装完毕后，可以使用vue命令 创建脚手架项目
npm install -g @vue/cli
```

1. 新建脚手架项目。找一个干净目录： `d:/code/VueUI/day01/demo`，执行命令：

   ```shell
   vue create  ele-project
   # 依次选择
   Manually select features
   选择两个： Babel - Router  
   2.x
   回车
   回车
   回车
   ```

2. 在项目中安装`ElementUI`组件库。

   ```shell
   # 保证该安装命令，在脚手架项目根目录下执行
   # 安装完毕后 将会在package.json出现element-ui的依赖配置
   npm i element-ui -S
   ```

3. 配置引入`ElementUI`组件库中的组件。

   ```javascript
   import ElementUI from 'element-ui';
   import 'element-ui/lib/theme-chalk/index.css';
   // Vue.use()方法将会自动调用ElementUI主js的install方法
   // 在install方法中，ElementUI将所有的组件都会注入Vue对象
   // 所以不需要在页面中组件，就可以直接使用组件的标签。
   Vue.use(ElementUI);
   ```

4. 在页面中使用。

   ```html
   <el-button type=""></el-button>
   ```



脚手架项目中一个组件是如何渲染到页面中的？

涉及到的文件：

`public/index.html`

`src/main.js`

`src/App.vue`

`src/router/index.js`

`src/views/HomeView.vue`

访问：`http://localhost:8080/`  可以看到页面中的内容：`导航、home`



脚手架项目本质上属于单页面应用，所有内容都会显示在`index.html`中。在`index.html`里，`vue`将会管理`#app`的`div`。因为在真正运行`html`时，脚手架将会自动在`html`中引入`main.js`。

在main.js中通过`new Vue()` 的方式加载`router`等插件并且管理`#app`。这样就可以根据不同的请求资源路径在`#app`中显示不同的内容。

```javascript
new Vue({
  router,
  render: h => h(App)
}).$mount('#app')
```



**`ElementUI`比较适合写一些后台管理网站。** 



#### `NavMenu`导航菜单

`NavMenu`用于实现导航，基本结构：

```html
<el-menu mode="horizontal">
	<el-menu-item>导航选项1</el-menu-item>
	<el-menu-item>导航选项2</el-menu-item>
	<el-menu-item>导航选项3</el-menu-item>
	<el-menu-item>导航选项4</el-menu-item>
</el-menu>
```

案例：访问：http://localhost:8080/nav，看到水平导航组件效果。

1. 新建页面：`views/Nav.vue`。  编写导航组件。
2. 配置路由：配置  `/nav`  与 `views/Nav.vue`组件的映射关系。 



#### 设置`NavMenu`的默认激活状态

```html
<el-menu mode="horizontal" default-active="3">
	<el-menu-item index="1">导航选项1</el-menu-item>
	<el-menu-item index="2">导航选项2</el-menu-item>
	<el-menu-item index="3">导航选项3</el-menu-item>
	<el-menu-item index="4">导航选项4</el-menu-item>
</el-menu>
```



#### 设置`NavMenu`的下拉子菜单

```html
<el-menu mode="horizontal" default-active="3">
	<el-menu-item index="1">导航选项1</el-menu-item>
	<el-menu-item index="2">导航选项2</el-menu-item>
	<el-submenu index="3">
        导航选项3
		<el-menu-item index="3-1">炫酷黑</el-menu-item>
		<el-menu-item index="3-2">中国红</el-menu-item>
    </el-submenu>
	<el-menu-item index="4">导航选项4</el-menu-item>
</el-menu>
```



#### 垂直导航

删除mode属性，默认垂直导航

```html
<el-menu default-active="3">
    ....
</el-menu>
```



#### 修改组件库组件的默认样式的方案

1. 若希望修改组件的默认样式，先去文档中看看，该组件是否已经提供相关属性，如果有，则首选通过属性控制样式。
2. 如果没有属性：
   1. 为组件添加`class`属性，通过style修改组件默认样式。
   2. 为组件添加`style`属性（内联样式），直接修改组件属性。
   3. 右键检查，查看希望修改的标签样式类名，在`vue`代码中通过在`style`标签中覆盖该样式，实现样式的修改。若这种方式由于优先级不够修改不成功，则添加：`!important`。



### `ElementUI`的布局容器组件  `Container`

用于布局的容器组件，方便快速搭建页面的基本结构：

`<el-container>`：外层容器。当子元素中包含 `<el-header>` 或 `<el-footer>` 时，全部子元素会垂直上下排列，否则会水平左右排列。

`<el-header>`：顶栏容器。

`<el-aside>`：侧边栏容器。

`<el-main>`：主要区域容器。

`<el-footer>`：底栏容器。

### 基于`ElementUI`编写后台管理网站

#### 点击左侧边栏中的菜单项，动态更新`main`部分的内容

选择**嵌套路由**

嵌套路由的方案本质是通过路由地址的跳转来动态更新页面的局部内容

设计嵌套路由方案：

```
访问： /components 看到组件页面的基本布局 headder aside main
访问： /components/container 看到组件页面中嵌套Container
访问： /components/form  看到组件页面中嵌套Form
访问： /components/table 看到组件页面中嵌套Table
```

实现步骤：

1. 准备好3个组件：`Container.vue`   `Form.vue`   `Table.vue`

2. 配置嵌套路由：`router/index.js`   配置 `children:[]`

3. 在`el-main`中写一个“占位符”： `<router-view />`

4. 测试访问：

   ```
   http://localhost:8080/components/container
   http://localhost:8080/components/form
   http://localhost:8080/components/table
   ```

5. 希望点击左侧边栏菜单项直接跳转，可以开启`el-menu`的`router`模式。并且修改`menu-item`的`index`作为跳转路径。

6. 修改`menu`的默认选中项：`default-active`

   ```
   :default-active="$route.path"
   ```

7. 添加redirect，为/components路由设置默认二级路由：

   ```
   redirect: '/components/container'
   ```

   

#### `Table` 组件

`Table`用于使用表格的方式呈现数组数据，基本用法：

```html
<template>
  <el-table :data="tableData" style="width: 100%"
    stripe  border>
    <el-table-column prop="name" label="姓名"> </el-table-column>
    <el-table-column label="年龄">
      <template slot-scope="scope"> {{ scope.row.age }} 周岁 </template>
    </el-table-column>
    <el-table-column prop="gender" label="性别"> </el-table-column>
    <el-table-column prop="married" label="婚否">
      <template slot-scope="scope">
        {{ scope.row.married ? "已婚" : "未婚" }}
      </template>
    </el-table-column>
    <el-table-column label="操作" align="center">
      <template slot-scope="scope">
        <el-button type="primary" icon="el-icon-edit" circle></el-button>
        <!-- scope.$index返回当前行的下标 -->
        <el-button 
          @click="del(scope.$index)"
          type="danger" icon="el-icon-delete" circle></el-button>
      </template>

    </el-table-column>
  </el-table>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        { name: "亮亮", age: 18, gender: "男", married: false },
        { name: "晓宇", age: 16, gender: "女", married: false },
        { name: "小新", age: 28, gender: "男", married: false },
        { name: "涛哥", age: 38, gender: "男", married: true },
      ],
    };
  },
  methods: {
    del(index){
      this.tableData.splice(index, 1)
    }
  }
};
</script>
```



#### `Form`表单

`Form`组件用于描述表单，`Form`中可以包含很多表单组件，用于收集用户数据：

```html
<el-form :model="form" label-width="80px">
  <el-form-item label="活动名称">
    <el-input v-model="form.name"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary">立即创建</el-button>
    <el-button>取消</el-button>
  </el-form-item>
</el-form>
```

Form 组件提供了表单验证的功能，只需要通过 `rules` 属性传入约定的验证规则，并将 Form-Item 的 `prop` 属性设置为需校验的字段名即可。校验规则参见 [async-validator](https://github.com/yiminghe/async-validator)

```html
<el-form :model="form" label-width="80px"  :rules="rules">
  <el-form-item label="名称" prop="name">
    <el-input v-model="form.name"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary">立即创建</el-button>
    <el-button>取消</el-button>
  </el-form-item>
</el-form>
```

```javascript
rules : {
    name: [
        {required:true, message:'用户名不能为空', trigger: 'blur'}
    ]
}
```

点击提交按钮，也需要对表单进行验证，这时就可以直接调用form对象的validate方法来进行表单对象的自检，如下：

```html
<el-form :rules="rules" ref="form">
	.....
</el-form>
```

```javascript
onSubmit(){
    this.$refs['form'].validate((v)=>{
        if(v){
            成功
        }else{
         	失败   
        }
    })
}
```

### 移动端组件库

从git中拉取新项目：

```shell
# 找个干净目录： /day02/demo/
git clone https://gitee.com/mingxuchn/web2203-code.git
# 进入项目目录后，安装node_modules
cd WEB2203-CODE
npm  install 
```

## `MintUI`

### 安装配置`MintUI`

1. 在项目目录下，执行安装命令：

   ```shell
   npm i mint-ui -S
   ```

2. 在`main.js`中引入`mintui`：

   ```javascript
   import MintUI from 'mint-ui'
   import 'mint-ui/lib/style.css'
   Vue.use(MintUI)
   ```

3. 使用组件。



### 实现注册页面

1. 新建页面： `views/Register.vue`。编写页面内容。
2. 配置路由：访问 `/regsiter`  看到该页面即可。



### `Header`组件

Header组件用于显示标题栏，title属性指定标题文本。提供了两个插槽：left/right, 用于在标题栏左右两侧嵌入`HTML`元素。

```html
<!-- 标题栏 -->
<mt-header title="用户注册">
    <mt-button icon="back" slot="left"></mt-button>
    <router-link to="#" slot="right">登录</router-link>
</mt-header>
```



#### `Field`组件

`Field`组件用于实现表单输入框，基本写法：

```html
<mt-field	type="text|password|email|...."
          	placeholder=""
          	value=""
          	readonly     只读
          	disabled     禁用
          	state="success | error | warning"     文本框的状态
          >
</mt-field>
```

测试：访问：`/field`   看到  `testing/Field.vue`.



### 实现注册页面

1. 编写Header、Field、Button，完成页面基本结构。
2. 表单验证。为Field组件绑定焦点失去事件，验证输入框的值。



表单验证时发现为组件`mt-field`绑定`blur`事件时无效，应该如下设置：

```html
<mt-field @blur.native.capture="checkName"></mt-field>
<mt-field @focus.native.capture="checkZZZZ"></mt-field>
```

为`mt-field`组件直接绑定`@blur`事件不会在焦点失去时生效，因为会被`vue`当做是`mt-field`组件的自定义事件。这种事件需要在`mt-field`组件内部通过`$emit()`来主动触发。所以需要添加修饰符：`@blur.native`告诉`vue`，这个`blur`是`DOM`原生的焦点失去事件，当焦点失去时自动触发。

`mt-field`组件最终会编译成一个非常复杂的`a`标签。如果直接给`mt-field`绑定`@blur`事件，那么该焦点失去事件将会直接加到最外层的`a`标签身上。

```html
<a class="mint-cell mint-field">
    <div class="mint-cell-left"></div> 
    <div class="mint-cell-wrapper">
        <div class="mint-cell-title">
            <span class="mint-cell-text">用户名</span>
        </div> 
        <div class="mint-cell-value">
            <input placeholder="请输入用户名" 
                   type="text" class="mint-field-core"> 
            <div class="mint-field-clear" style="display: none;">
                <i class="mintui mintui-field-error"></i>
            </div> 
            <span class="mint-field-state is-default">
                <i class="mintui mintui-field-default"></i>
            </span> 
            <div class="mint-field-other"></div>
        </div>
    </div> 
    <div class="mint-cell-right"></div>
</a>
```

当用户触发了`input`的`blur`，`input`的`blur`默认不会冒泡到父容器`a`上，所以在a上绑定`blur`事件不会因为事件冒泡现象自动执行。所以需要`@blur.native.capture`, 使得事件处理函数在焦点失去事件捕获阶段就先（先于`input`的`blur`）执行（而不是在冒泡阶段调用）。



### `NavBar`组件

`navbar`表示顶部导航，内部可以包含多个导航选项卡，基本写法如下：

```html
<mt-navbar v-model="selected">
	<mt-tab-item id="1">UI</mt-tab-item>
	<mt-tab-item id="2">电商</mt-tab-item>
	<mt-tab-item id="3">网页</mt-tab-item>
	<mt-tab-item id="4">交互</mt-tab-item>
</mt-navbar>
<script>
	data(){
        return {
            selected: "1"
        }
    }
</script>
```

案例：访问：`/nav`     看到   `testing/Nav.vue`.



### 脚手架项目中静态资源（图片）的访问方法

在`VueCli`脚手架项目中，图片的存放位置通常有两个位置：`src`下、 `public`下。

1. 如果将图片放在`src/assets`目录，可以如下编写相对路径访问图片：

   ```html
   <img src="../assets/001.png">
   <img src="@/assets/001.png">
   ```

   `@`在脚手架项目中默认表示`src`。所以`@`开头相当于从`src`向下寻找文件。

   如果图片放在assets下，并且使用相对路径来访问图片，在项目**编译打包**时，将会为图片重命名（`001.2cb338f3.png`），放入`/img`文件夹中，并且将会篡改编译后的图片路径：

   ```html
   <img src="/img/001.2cb338f3.png" alt="">
   ```

   这种操作意味着脚手架将会对`src`下的图片做统一管理。

   <span style="color:red;"> 如果图片足够小，脚手架将会把图片转成Base64图片编码，直接写入img的src属性，减少网页对小图片的访问次数，提高网站性能。 </span>

2. 如果将图片放入`public`下，可以通过如下路径访问图片：

   ```
   public/images/001.png
   public/images/004.png
   public/images/007.png
   public/images/025.png
   ```

   ```html
   <img src="/images/001.png">
   <img src="/images/004.png">
   <img src="/images/007.png">
   <img src="/images/025.png">
   ```

   `public`下的资源直接通过`/`访问即可，因为`public`下的资源在编译打包时将会直接复制粘贴到`dist`目录中。所以项目部署后可以通过`/`来直接访问`dist`文件夹中的资源。

3. 图片什么时候放到`assets`？什么时候放到`public`？

   一些项目中必要的图标适合放`assets`下（会有一些优化方案），较大的图片适合放`public`或另外一台图片服务器中，通过绝对路径来访问。

4. 如果为src设置动态路径：

   ```html
   <img src="@/assets/index_0.png" slot="icon" alt="">             
   需要动态设置src：
   <img :src="`@/assets/index_0.png`" slot="icon" alt="">             
   ```

   如果动态处理相对路径src，加上冒号后，vueloader不会对该图片资源进行编译，会把该路径直接输出到src，导致图片找不到。所以需要添加require方法手动编译：

   ```html
   <img :src="require(`@/assets/index_0.png`)" slot="icon" alt="">   
   ```

   这样，`viewloader`就可以编译该资源，并且把访问路径设置给`src`属性。

   



### 实现首页中顶部组件内容

1. 修改`HomeView.vue`。
2. 添加`header`组件。
3. 添加`navbar`组件。
4. **添加`tabbar`底部选项卡组件。**



### `Tabbar`组件

`Tabbar`组件用于实现底部选项卡。基本结构：

```html
<mt-tabbar v-model="tabSelected">
  <mt-tab-item id="index">
    <img slot="icon" src="../assets/.....png">
    首页
  </mt-tab-item>
  <mt-tab-item id="me">
    <img slot="icon" src="../assets/.....png">
    我的
  </mt-tab-item>
</mt-tabbar>
data(){
	return {
		tabSelected: 'index'
	}
}
```

### `Tabbar`组件

`Tabbar`组件用于实现底部选项卡。基本结构：

```html
<mt-tabbar v-model="tabSelected">
  <mt-tab-item id="index">
    <img slot="icon" src="../assets/.....png">
    首页
  </mt-tab-item>
  <mt-tab-item id="me">
    <img slot="icon" src="../assets/.....png">
    我的
  </mt-tab-item>
</mt-tabbar>
data(){
	return {
		tabSelected: 'index'
	}
}
```



### 基于嵌套路由实现`首页`、`我的`的切换

1. 设计嵌套路由方案。

   ```
   点击首页：  /home/index 看到 HomeView.vue 中嵌套 Index.vue
   点击我的：  /home/me  看到 HomeView.vue 中嵌套 Me.vue
   ```

2. 准备好所有的组件页面：

   1. `HomeView.vue`中添加`router-view`占位符。
   2. 新建`Index.vue`。把首页资源搬过来。
   3. 新建`Me.vue`。

3. 配置嵌套路由。

4. 访问测试地址：

   ```
   /home/index    看到 HomeView.vue 中嵌套 Index.vue
   /home/me       看到 HomeView.vue 中嵌套 Me.vue
   ```

5. 通过`watch`监听`tabSelected`的变化，`tabSelected`的变化代表了激活状态的变化



### `Swipe`组件

轮播图组件：

```html
<mt-swipe>
  <mt-swipe-item>
      <img src="...">
  </mt-swipe-item>
  <mt-swipe-item>
      <img src="...">
  </mt-swipe-item>
  .....
</mt-swipe>
```



### 学子问答项目实践

前端通过发送`http`请求获取后端提供的数据，从而查看每个类别下的文章列表。 

#### 项目架构

基于**前后端分离**架构：

1. 前端技术栈：`vuecli`、`vue2.0`、`MintUI`等。
2. 后端技术栈：`nodejs`、`mysql`。

通讯协议使用`http`协议。



#### 搭建服务端环境

1. 下载`sever.zip`, `xzqa.sql`。

2. 将`xzqa.sql`导入`mysql`。

   ```shell
   # 点击shell按钮，打开终端，执行命令：
   mysql -uroot < 把文件拖拽进来，自动生成路径
   # 执行完毕后，可以通过命令，登录mysql，查看表结构与数据
   mysql -uroot 
   show databases;
   use xzqa;
   show tables;
   select * from xzqa_category;
   desc xzqa_category;
   .........
   ```

3. 解压`server.zip`，进入项目目录，执行命令，启动服务器：

   ```shell
   node app.js
   ```

4. 测试接口。

   ```
   http://localhost:3000/category
   ```

   

#### 当首页挂载完毕后立即加载类别列表

当首页挂载完毕后需要通过`axios`向服务端发送请求，获取类别列表，遍历渲染到页面中

**实现思路：**

1. 下载安装`axios`。

   ```shell
   # 进入项目目录后，执行安装命令
   npm install --save axios vue-axios
   ```

   安装完毕后，将会在`package.json`中生成`axios`的依赖。

   在`main.js`中配置`axios`：

   ```javascript
   import axios from 'axios'
   import VueAxios from 'vue-axios'
   Vue.use(VueAxios, axios)
   ```

2. 在`Index.vue`的`mounted`声明周期方法里，通过`axios`发送`http`请求，获取类别列表。

   ```javascript
   mounted(){
       // 发送http请求， 加载类别列表
       this.axios.get('/category').then(res=>{
         console.log('加载类别列表：', res)
         // 把 res.data.results 存入 data.cats 变量中
         this.cats = res.data.results
       })
     }
   ```

   

3. 获取类别列表后，在页面中通过`v-for`遍历它，显示在导航中。

   ```html
   <mt-tab-item :id="item.id+''" 
                v-for="item in cats" :key="item.id">
       {{item.category_name}}
   </mt-tab-item>
   ```

#### 实现切换顶部导航，更新文章列表

   当切换顶部导航后，需要获取当前选中项类别的`ID`，重新发送`http`请求获取相应类别下的文章列表。拿到新列表后直接替换当前列表显示即可。

   1. 为绑定顶部导航选中项的变量：`selected`添加`watch`监听。 
   
   2. 一旦捕获到顶部导航的变化，立即获取当前选中项的`id`。立即向服务端发送`http`请求，获取当前类别下的首页文章列表数据。
   
      ```
      http://localhost:3000/articles?cid=${this.selected}&page=1
      ```
   
   3. 渲染列表。

   

#### 实现触底加载下一页

   业务需求：**当**滚动到底部时，发送`http`请求，加载当前类别的下一页数据。一旦获取到最新数据后，将新数组追加到旧数组末尾即可。

   `MintUI`提供了`InfiniteScroll`指令，实现滚动到底的监听。

#### `Infinite Scroll`指令

   无限滚动指令用于监听元素滚动触底事件，基本用法：

   ```html
   <div v-infinite-scroll="loadMore" 函数名称，当触底后自动调用该函数
        infinite-scroll-distance="50" 触发无限滚动的距离阈值>
       <p>....</p>
       <p>....</p>
       <p>....</p>
   	......    
   </div>
   methods: {
   	loadMore(){
   		.....
   	}
   }
   ```

   示例：访问：`/inf`   看到  `/testing/Inf.vue`

   

#### 实现触底加载下一页

   业务需求：**当**滚动到底部时，发送`http`请求，加载当前类别的下一页数据。一旦获取到最新数据后，将新数组追加到旧数组末尾即可。

   1. 在`data`中声明一个变量：`page`，用于描述当前页码。默认值为1。
   
   2. 为列表添加无限滚动指令，一旦滚动到底，执行`loadMore`方法。
   
   3. 在`loadMore`方法中发送`http`请求，加载当前类别的下一页数据。获取到新数组后，需要把新数组追加到旧数组末尾。
   
   4. 完成相关业务后，发现一个`bug`，切换顶部导航，`page`需要重置为1。
   
      ```
      this.page = 1
      ```
   
      

   至此发现发送了以下3个请求，都需要访问文章列表：

   1. mounted时加载UI类别下的首页。
   2. 点击顶部导航，加载当前类别下的首页。
   3. 触底加载时，需要加载当前类别下的下一页数据。

   发现，他们仨都是向  /articles 地址发请求，只不过传递不同的参数，最终获取到文章列表数据。所以没有必要写三遍，为了提高代码复用性，可维护性，可以封装一个方法：

   `loadArticles()`用于接收参数`cid`和`page`，发送`/articles`请求，返回查询到的结果。

   ```
   loadArticles(cid, page, callback){
   	this.axios.get(`/articles?cid=${cid}&page=${page}`).then(res=>{
   		let articles = res.data.results  -> 查询结果文章列表
   		// 自定义的方法，需要执行异步任务，并且返回异步任务的结果
   		// 解决方案：1) callback     2) Promise
   		callback(articles)
   	})
   }
   
   mounted(){
   	this.loadArticles(1, 1, (articles)=>{
   		执行后续业务即可
   	})
   }
   watchSelected(){
   	this.loadArticles(变量, 1, (articles)=>{
   		执行后续业务即可
   	})
   }
   loadMore(){
   	this.loadArticles(变量, 变量, (articles)=>{
   		执行后续业务即可
   	})
   }
   ```

   

#### 实现文章详情页

   当点击列表中的某一个列表项时，跳转到文章详情页显示该文章的详细信息。这个跳转过程需要传递参数：选中项文章的`id`。

   ```
   http://localhost:3000/detail?id=237
   ```

   **实现流程：**

   1. 准备好`Article.vue`，配置路由，访问`/article`时看到`Article.vue`.
   
   2. 处理路由跳转时的参数传递问题。需要从`/home/index`跳转到`/article`并且需要携带参数：选中项的文章`id`。两种方案：
   
      1. 方案1：查询字符串传参        
      
         ```html
         <router-link to="/article?id=237">跳转</router-link>
         ```
      
         在article页面中获取参数id：
      
         ```
         let id = this.$route.query.id
         ```
      
      2. 方案2：路径传参
      
         ```html
         <router-link to="/article/237">跳转</router-link>
         ```
      
         在article页面中获取藏在路径最后一部分的字符串：
      
         ```javascript
         //如下配置路由：
         {
             path: '/article/:id',
             component: Article.....
         }
         ```
      
         ```javascript
         this.$route.params.id
         ```
      
         

   ```
   Cannot read properties of null (reading 'subject')
   不能读取null的属性，读取subject属性时报的这个错。说明代码执行了：
   null.subject，哪里写了.subject呢？发现{{article.subject}}，意味着article就是个null。再看看为啥。
   ```

   

### `Moment.js`

   `moment.js`是一个`Javascript`的日期时间类库。专门处理日期时间、字符串之间的转换。常用API如下：

   1. 获取一个`moment`对象：
   
      ```javascript
      let day = moment()   // moment对象描述当前时刻
      let day = moment(毫秒值)
      let day = moment.unix(秒值)
      let day = moment('2022-01-02')
      let day = moment('2022/01/02', 'YYYY/MM/DD')
      let day = moment('03/25/2011', 'MM/DD/YYYY')
      ```
   
   2. 把`moment`对象转成字符串：
   
      ```javascript
      day.format('YYYY-MM-DD')    //  2022-07-06
      day.format('YYYY-MM-DD HH:mm:ss')    //  2022-07-06  17:47:30
      day.format('YYYY年MM月DD日')    //  2022年07月06日
      ```

   

#### 安装`moment`，配置`moment`

   在项目目录下，执行安装命令：

   ```shell
   npm install --save moment
   ```

   安装完毕后`package.json`中将会出现依赖。

   在`main.js`中将`moment`对象引入`Vue`，这样在页面中就可以直接使用`this.moment`

   ```javascript
   import moment from 'moment'
   Vue.prototype.moment = moment
   ```

   

   