# vue

> 全局安装vue脚手架  `npm i -g @vue/cli`
>
> 官方API： [vue2](https://cn.vuejs.org/v2/api)   [vue3](https://v3.cn.vuejs.org/api/)   [vue/cli](https://cli.vuejs.org/zh/guide/)   [vue/devtools](https://devtools.vuejs.org/)

## 1.vue-cli

### 1.1 创建项目包

`vue create 项目名`

- 项目名不允许有大写字母, 只能是 `小写字母 - 或 _`

- 项目路径中`不允许`有中文和特殊符号

- 目录下不能有同名文件夹

```powershell
vue create [项目名称]
```

### 1.2 运行服务器

- 在vue-pro 目录下执行启动命令:

- vue项目包必须用自带的服务器, 在浏览器手动访问: `localhost:8080`

```powershell
npm run serve
```

### 1.3加载流程

- localhost:8080: 访问的是 `index.html`
- main.js: 引入了 App.vue , 然后加载到 `id=app` 的元素上
- App.vue: 导出vue代码



## 2.vue基础使用

### 2.1 创建vue对象

`new Vue()`: 创建时有固定的初始化`配置项`：

**DOM**

- el : 初始化vue对象时, 设定vue对象管理的元素, 值 id选择器
- render(渲染): 手架中使用, `main.js`文件. 用于加载 `.vue` 文件到 vue对象里

**数据**

- data：存储使用到的数据, 可以在HTML中使用
  - 数据都是存储在 `vue`对象里
- methods： 绑定给元素的方法
  - 方式中的this指向: `当前vue对象`
- computed：称为计算属性
  - 存放在这里的函数, 使用时不用(), 会自动触发. 
  - 适合没有参数的函数
- props：外来的属性
  - 理解成 组件的形参, 接收组件使用时传入的实参
- - 
- watch：监听器，监听一个属性的变化
  - 配置：`func(to,from){...}`

**资源**

- directives：指令
  - 自定义指令都是 `v-` 开头
  - 参数1: 代表指令所在的元素，参数2: 指令的值, 通过=赋值的
  - 两种语法
    - 值是函数: 在DOM元素创建时触发, 还未展示到页面 `func(el,bindings){...}` 
    - 值是对象: 精确配置触发的时机。例如: `{inserted(el){...}}` 
- components：组件
  - 默认语法: `components: {组件名}`  组件名就是标签名
  - 自定义语法: `components:{标签名: 组件名}`

- filters：过滤器，通过过滤器的处理, 把返回值显示到页面上
  - 使用：`{{ 值 | 过滤器 }}`
  - 配置：`func(值){...}`，返回值就是过滤后的结果

**生命周期**

- 

**注意**：

- 图片在JS中使用, 必须用 require 方法引入, 否则无法加载

### 2.2 vue语法

#### 2.2.1 vue指令

指令: 就是vue提供的一些特殊的属性, 都是`v-`开头

- `v-show`: 
  - 显示还是隐藏, 利用css display:none -- 适合频繁切换隐藏的场景。
  - `<p v-show="true"></p>`

- `v-if`: 
  - 移除/添加元素，适合不频繁的, 特别是一次性的隐藏/显示。
  - `<p v-if="true"></p>`，v-else-if,v-else同理

- `v-once`: 
  - 一次性渲染, 后续不更新。
  - `<p v-once></p>`

- `v-pre`: 
  - 原样输出 `{{}}`。
  - `<p v-pre></p>`

- `v-text/v-html`:  
  - 对应 innerText 和 innerHTML，替换原内容。
  - `<p v-text="kw">111</p>`

- `v-for`: 
  - 遍历数组 生成元素
  - 语法有3种
    - v-for="值 in/of 数组"
    - v-for="(值,序号) in/of 数组"
    - v-for="值 in/of 数字"
  - key: 给生成的元素添加唯一标识
    - 用途:当`数组有变化`时, 提升元素重用的效率;   如果数组不变则没用

- `v-on`: 
  - 事件绑定语法 .   原生事件 onclick
  - vue2中提供了语法糖:    `@事件名=""`

- `v-bind`:
  - 属性绑定语法
  - vue2中提供语法糖： `:属性名=""`

- `v-model`:
  - 双向绑定
  - 会自动判断所在的元素类型, 然后为对应的属性绑定值
  - `v-model="变量"`
  - 表单元素: 输入框, 单选框, 多选框, 下拉选框.. 用户能操作修改值
  - 作用: 实时变化绑定的数据

- `v-slot`: 
  - 插槽
  - 组件负责布局操作, 使用插槽作为占位符使用
  - 组件在使用时, 其双标签写法中的内容, 会替换掉插槽
  - 命名插槽: `<slot name='名字'/>`
    - 使用时有3种语法
    - slot='名字'   - vue1
    - v-slot:名字   - vue2
    - #名字  - vue2语法的语法糖

- 


#### 2.2.2 属性与事件

  - 在HTML中提供了新的语法, 代表DOM操作

  - `{{}}` 插值语法, 类似 模板字符串的 `${}`  其中可以书写 JS代码

  - 属性绑定语法

    - vue1写法 `v-bind:属性名=""`
    - vue2写法 `:属性名="JS代码"`

  - 事件绑定语法

    - 事件关联的方法, 必须书写在methods属性里

    - vue1写法 `v-on:事件名`

    - vue2写法 `@事件名`

      使用的差异: 如果方法不需要传递实参 `可以省略()`

```vue
<button @click="事件方法" ></button>
<button @click="事件方法(实参, 实参)" ></button>
```

![image-20220620221211288](vue.assets/image-20220620221211288.png)

**常用动态属性**

- class
  - :class="{类: true/false}"  真生效 假不生效
- style
  - :style="{属性名: 值}"
  - 注意属性名带 `_`  需要小驼峰 或 字符串

- - 

**特殊属性**

- ref
  - `<input type="text" ref="自定义" />`
  - 把变量和元素绑在一起，变量会存储在 vue的 $refs 属性里
  - 例如设置颜色`this.$refs.自定义.style.color = 'green'`
- key
  - :key="唯一标识"
  - key为元素添加唯一标识，在数组内容发生修改的时候, 可以提高性能, 直接复用元素 

#### 2.2.3网络请求

- 第三方的axios模块: 需要自己安装 `npm i axios vue-axios`
- 引入方式分两种
  - 局部: 在.vue文件中, `import axios from 'axios'`
  - 全局:在main.js中，
    - `import axios from 'axios'`（仅原型注入axios无代码提示）
    - `import VueAxios from 'vue-axios';`
    - `Vue.use(VueAxios, axios)`,use:是vue提供的专门加载第三方模块的方法

- 使用时, 固定语法
  - get: `axios.get(地址).then(res=>{})`
- 如何展示到页面上
  - `前提设定`:只有存储在配置项data中的属性, 才能在页面上显示
  - 在data中, 声明一个属性
  - 在请求中,把请求结果中的数据存入本地的:`this.data = res.data`
- 使用时:  为了提高效率 和 用户体验
  - 用v-if判定:data存在再用!
  - template: 虚拟容器, 可以为多个元素统一进行if判断

#### 2.2.4组件

- 用于拆分大型页面, 拆分成多个独立的`.vue`文件 -- 团队合作, 复杂->简单
- 存放在 components 目录里
- 文件名要求 `最好` 大驼峰, 至少两个单词
  - 原因: 怕和系统标签重名
- 推荐根元素的 class名 是 文件名的 `中划线命名法`
- 组件使用分三步: `引入` -=> `注册` ->`使用`
  - 引入
    - `import ... from './components/...'`
    - export default 中`components: { MyFooter }`
  - 注册
    - 普通方式:  `components: {组件名}`
    - 自定义方式: `components:{ 自定义名称: 组件 }`
  - 使用: 单标签 + 双标签 + 大驼峰 + 中划线 写法都支持
    - 推荐:`<xxx-xxx />`

#### 2.2.5 生命周期

- 作用： 配合网络请求用, 实现自动发请求的操作
- 钩子函数: 在固定事件发生时, 自动触发的函数就叫 钩子函数
  - 创建: 内存中,还没显示到页面
    - 创建前: beforeCreate
    - 创建完: created

  - 挂载: 显示到页面上
    - 挂载前: beforeMount
    - 挂载完: mounted

  - 更新: 页面发生更新
    - 更新前: beforeUpdate
    - 更新完: updated

  - 销毁: 组件被移除
    - 移除前: beforeDestroy
    - 移除后: destroyed


```js
  beforeCreate() {
    console.log('beforeCreate: 将要创建')
  },
  created() {
    console.log('created: 创建完毕')
  },
  beforeMount() {
    console.log('beforeMount: 将要安装到页面上')
  },
  mounted() {
    console.log('mounted: 安装到页面完毕')
  },
  beforeUpdate() {
    console.log('beforeUpdate: 更新前')
  },
  updated() {
    console.log('updated: 更新完毕')
  },
  beforeDestroy() {
    console.log('beforeDestroy: 将要销毁')
  },
  destroyed() {
    console.log('destroyed: 销毁')
  },
```

#### 2.2.6 父子组件传参

- App.vue
  - <自定义组件  :需要传的参数="..."  />
- 组件
  - export default中`props: ['参数']`

#### 2.2.7 插槽

- App.vue

  - 必须用双标签书写，例如`<my-slot></my-slot>`

  - 向指定name属性的插槽中存放内容：

    ```vue
    <!-- 指定向 名字是 menu的插槽里放东西 -->
    <!-- vue1 -->
    <div slot="menu">这是菜单内容 vue1</div>
    <!-- vue2: 必须配合 template 标签用 -->
    <template v-slot:menu>
        <h2>哈哈哈哈</h2>
    </template>
    <!-- vue3: 必须配合 template, 语法糖# -->
    <template #menu>
        <h2>哈哈哈哈</h2>
    </template>
    ```

    

- 组件

  - 一种特殊的组件: 负责布局, 没有实际内容

  - 插槽占位符组件: `<slot name="..." />`在运行时会替换成组件的标签内容，可以使用name属性命名

#### 2.2.8 路由

- `router-view` 占位符: 路由系统提供的
  - 作用: 会扫描 浏览器的地址栏路径, 找到其对应的组件 进行展示
- 组件:如果是路由切换的组件, 则必须存储在`views`目录里
  - 命名大驼峰, 不需要必须2个单词
- 路由配置文件: `router/index.js`
  - 配置 path 路径 和 组件的对应关系
  - props属性: 为true, 代表允许组件通过 props 属性接收路由参数
  - 路径
    - `*`: 通配符, 匹配所有没有的路径
    - `/`: 根路径 首页 
    - `/???`: 自定义的其他路径
- 传参的两种方式:
  - 传统: `路径?参数=值&参数=值...`
  - 新的: `路径/值/值/值`  需要配合 路由的配置 `path:'/路径/:参数/:参数'`


> router-view -> 查找浏览器地址栏 -> 到 index.js 中匹配 -> 找到组件

2.2.9 

- `router-view` 占位符: 路由系统提供的
  - 作用: 会扫描 浏览器的地址栏路径, 找到其对应的组件 进行展示
- 组件:如果是路由切换的组件, 则必须存储在`views`目录里
  - 命名大驼峰, 不需要必须2个单词
- 路由配置文件: `router/index.js`
  - 配置 path 路径 和 组件的对应关系
  - props属性: 为true, 代表允许组件通过 props 属性接收路由参数
  - 路径
    - `*`: 通配符, 匹配所有没有的路径
    - `/`: 根路径 首页 
    - `/???`: 自定义的其他路径
- 传参的两种方式:
  - 传统: `路径?参数=值&参数=值...`
  - 新的: `路径/值/值/值`  需要配合 路由的配置 `path:'/路径/:参数/:参数'`


> router-view -> 查找浏览器地址栏 -> 到 index.js 中匹配 -> 找到组件

#### 2.2.9Vuex

全局状态共享: 把数据在多个.vue文件中共享

- 实现方案: 把 store对象, 存储到 vue的实例对象里 -- `main.js`
- 使用时
  - 把共享的数据存储在 store.state 属性里
  - 利用 `$store.state` 来读取属性
  - 为了安全性考虑: 要修改属性必须通过指定的方法
    - 在`mutations`属性里, 制作函数
    - 触发时, 需要用 `commit` 来触发
