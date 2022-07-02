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

### 1.4 编译

```shell
npm run build
```

#### 1.5 本地服务器

**vue项目执行npm run build之后生成的dist文件**，**不能直接通过vscode开启服务访问，会报错**

```shell
安装
serve  npm install serve -S -g 
启动服务
serve dist
```

## 2.vue2基础使用

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
- axios的基础路径属性
  - `axios.defaults.baseURL = '...'`
  - 作用: 用axios发的请求, 如果是相对路径 则会自动拼接到这个路径后
  - 注意: 必须在 use 前设置, 然后再注入到vue里

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
- 自定义组件组件
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



#### 2.2.9Vuex

全局状态共享: 把数据在多个.vue文件中共享

- 实现方案: 把 store对象, 存储到 vue的实例对象里 -- `main.js`
- `state`
  - 把共享的数据存储在 `store.state` 属性里
  - 利用 `$store.state` 来读取属性(`{{}}`中可以省略this)
  - 辅助函数`...mapState([value])`（在`computed`属性中引入）

```js
//...mapState原理
function mapState(names){
  let obj = {}
  names.forEach(name=>{
    obj[name] = function(){
      return this.$store.state(name)
    }
  })
  return obj
}
```

- `mutations`
  - 为了安全性考虑: 要修改属性必须通过指定的方法
  - 在`mutations`中存放`函数名（state,参数）`
  - 需要用 `this.$store.commit(函数名，参数)` 来触发
  - 辅助函数`...mapMutations(函数名)`，使用时`函数名(参数)`

```js
//...mapMutations原理
function mapMutations(funcs){
  let obj = {}
  funcs.forEach(func=>{
    obj[func] = function(){
      return this.$store.commit(func,arguments[0])
    }
  })
  return obj
}
```

- `getters`
  - 计算属性，利用`state`中已有的值计算新值
  - `getters`中存放`函数名（state）`
  - `$store.getters.函数名`
  - 辅助函数`...mapGetters([函数名])`
- `actions`
  - 存放网络请求相关操作，请求的数据在多个组件中使用时可以采用该方法
  - `actions`中存放`函数名（store,参数）`
  - `this.$store.dispatch(函数名)`
  - 辅助函数`...mapActions(方法名)`
  - `actions`添加方法，发送请求-->`state`中添加属性，保存请求的返回值-->`mutations`中添加方法更新`state`中的值-->请求结束后，触发`mutations`中 的方法，来把值更新到`state`中
- `modules`
  - 用于大型项目拆分模块
  - 引入模块`import ... from ...`
  - `modules`存放引入模块的名称
  - 使用时在`state`中引入`模块名称`，模块中的数据`{{模块名称.属性}}`

## 3.Vue3基础使用

### 3.1 TypeScript

[官方文档](https://www.typescriptlang.org/docs/)

#### 3.1.1 安装

`npm install -g typescript`

#### 3.1.2 使用

`tsc 文件名`

#### 3.1.2 特性

- 强类型语言，代码非常严格, 有任何错误 都会`静态报错`
- TS支持为变量声明数据类型
- 编译工具的原理: 把TS中的特殊语法去掉,转为JS
- TS语言不能直接运行, 必须转换成 JS 才能运行, 这就需要编译工具的配合
- TS会检测同时打开的文件中, 是否有同名的变量, 并报错

### 3.2 vue3的特点

>  vue3 不再要求只能有唯一的根元素，支持使用Typescript
>
> vue3没有全局的东西，不存在this关键词

#### 3.2.1 默认属性

- 改造1
  - vue2的属性默认自动`全部`响应式. 一旦某些属性不需要响应式 则浪费资源
  - vue3: 手动用 `ref` 把值(`普通数据类型`)改成响应式
  - `缺点`: vue3的ref写法, 只能一个个改

```typescript
import { defineComponent, ref } from 'vue'
export default defineComponent({
  // setup: 相当于创建周期, 组件创建完毕时触发
  setup() {
    console.log('setup:组件创建完毕!')
    // vue2: data中的所有属性都是响应式的, 只要修改数据页面会自动变
    // -- 底层为了实现这种效果, 需要为每个属性添加监听器
    // -- 问题: 浪费额外的资源
    // vue3: 把数据的监听器 改为手动模式 -- 由用户来选择哪些加哪些不加
    // ref(): 会把普通的值, 装载到一个具有监听器的对象里. 值的变化就会自动更新DOM元素
    var num = ref(10)
    console.log('num:', num)
    // 这个return相当于  data(){ return{} }
    // 只有书写在这个{}对象中的属性, 才能在页面上使用
    return {
      num: 10,
      count: ref(10), //带监听器的10
    }
  },
})
```

- 改造2:
  - 提供 reactive 方式: 直接把对象类型改成响应式
  - 缺点: 使用时必须用 `data.` 来取值，直接用扩展运算符会取消data的响应式

```typescript
import { defineComponent, reactive, ref } from 'vue'
export default defineComponent({
  setup() {
    // vue3 手动为每个属性添加响应式特征, 太累
    // 作者: 提供了 reactive, 可以批量为多个属性添加响应式
    const data = reactive({
      num: 10,
      count: 20,
    })

    return { data, n: ref(100) }
  },
})
```

- 改造3:
  - 能不能 像reactive方式一次改多个, 又能像`ref`方式 使用时直接用?
  - 作者提供了 `toRefs` 的方法:  把 reactive改造的对象中的属性, 全都转换成1个1个的 ref 方式的属性

```typescript
import { defineComponent, reactive, toRefs } from 'vue'
export default defineComponent({
  setup() {
    // 一次性改多个属性为响应式
    const data = reactive({
      num: 10,
      count: 20,
    })

    // ... 展开语法, 把对象中的属性 展开放在其他对象里
    return { ...toRefs(data) }
  },
})
```

#### 3.2.2 计算属性与监听器

- 计算属性:
  - 示例：`var num_2 = computed(() => num.value * 2)`
  - 响应式对象的值, 用value读取
- 监听器：
  - 示例：`watch(num, (to, from) => {...}`
  - 参数1: 要监听的属性，参数2: 回调函数, to新值  from旧值

```vue
<template>
  <div>
    <button @click="num++">{{ num }}</button>
    <p>num2倍: {{ num_2 }}</p>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, ref, watch } from 'vue'

export default defineComponent({
  setup() {
    var num = ref(10)
    console.log(num)

    // 计算属性:
    // 响应式对象的值, 用value读取
    var num_2 = computed(() => num.value * 2)

    // 参数1: 要监听的属性
    // 参数2: 回调函数, to新值  from旧值
    watch(num, (to, from) => {
      console.log('to:', to)
      console.log('from:', from)
    })

    return { num, num_2 }
  },
})
</script>

<style scoped></style>

```

#### 3.2.3 axios

- vue3没有过滤器语法, 使用函数写法转换数据
- vue3中没有 this 关键词, 因为vue3没有全局的东西
- axios 只能局部使用, 先安装 npm i axios

```vue
<template>
  <div v-if="data">
    <div>页数: {{ data.pageNum }}</div>
    <div class="cell" v-for="x in data.data" :key="x.nid">
      <span>{{ x.title }}</span>
      <!-- vue3没有过滤器语法, 使用函数写法转换数据 -->
      <span>{{ date(x.pubTime) }}</span>
    </div>
  </div>
</template>

<script lang="ts">
// vue3中没有 this 关键词, 因为vue3没有全局的东西
// axios 只能局部使用, 先安装 npm i axios
import axios from 'axios'

import { defineComponent, onMounted, ref } from 'vue'

export default defineComponent({
  setup() {
    var data = ref(null)

    // 生命周期
    onMounted(() => {
      const url = `http://www.codeboy.com:9999/mfresh/data/news_select.php`

      axios.get(url).then(res => {
        console.log(res)
        //值保存到本地
        data.value = res.data
        console.log(data)
      })
    })

    // vue3没有过滤器语法, 用函数代替
    function date(value: string) {
      // TS语言不支持隐式类型转换, 必须手动转换
      var d = new Date(parseInt(value))
      var year = d.getFullYear()
      var month = d.getMonth() + 1
      var day = d.getDate()
      return `${year}/${month}/${day}`
    }
    // 凡是在页面上使用的, 都要放return
    return { data, date }
  },
})
</script>

<style scoped lang="scss">
.cell {
  display: flex;
  width: 700px;
  padding: 10px;
  border-bottom: 1px dashed gray;
  justify-content: space-between;
}
</style>
```

#### 3.2.3 路由系统

- `router-link`跳转：与vue2相同
- 编程式跳转：
  - 引入路由
  - `import { useRouter } from 'vue-router'`
  - `const $router = useRouter()`
  - 创建跳转函数
  - `var methods={跳转方法}`
  - 返回函数
  - `return {...methods}`

```vue
<template>
  <div>
    <router-link to="/">首页</router-link>
    <router-link to="/about">关于</router-link>
    <hr />
    <button @click="goHome">首页</button>

    <button @click="goAbout">关于</button>
    <!-- 路由系统的占位符 -->
    <router-view />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { useRouter } from 'vue-router'

export default defineComponent({
  setup() {
    console.log('this', this)
    // 第三方的模块, 必须用 use 来引入
    const $router = useRouter()

    var methods = {
      goAbout() {
        $router.push('/about')
      },
      goHome() {
        $router.push('/')
      },
    }

    return { ...methods }

    // 方法的添加方案1: 1个1个写, 1个1个添加 -- 麻烦
    // function goAbout() {}
    // function goHome() {}
    // function add() {}
    // return { goAbout, goHome, add }
  },
})
</script>

<style scoped lang="scss">
a {
  display: inline-block;
  padding: 10px 30px;
  background-color: #eee;
  color: black;
  text-decoration: none;

  // 自带高亮样式
  &.router-link-exact-active {
    background-color: orange;
    color: white;
  }
}
</style>

```

#### 3.2.3 组件与vuex

- 组件与vue2写法一致
- vue2的语法.  vue3兼容
- vuex
  - 直接使用： `$store.state.变量`
  - vue3 不支持辅助函数, 没有mapState，可以使用计算属性
    - 引入store：`import { useStore } from 'vuex'`
    - 使用store：`const $store = useStore()`
    - 计算属性：`words: computed(() => $store.state.words)`

**App.vue**

```vue
<template>
<template>
  <div>
    <!-- 组件 -- components -->
    <input type="text" v-model="a" />
    <p>a:{{ a }}</p>
    <button @click="$store.commit('updateWords', a)">
      共享数据
    </button>
    <my-header />
    <my-footer />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import MyFooter from './components/MyFooter.vue'
import MyHeader from './components/MyHeader.vue'

export default defineComponent({
  components: { MyHeader, MyFooter },
  setup() {
    // a 配合双向绑定使用
    return { a: ref('') }
  },
})
</script>

<style scoped></style>
```

**Index.js**

```ts
import { createStore } from 'vuex'

export default createStore({
  // 共享数据
  state: {
    words: '壮壮再见!',
  },
  getters: {},
  mutations: {
    updateWords(state, words) {
      state.words = words
    },
  },
  actions: {},
  modules: {},
})

```

**Myfooter.vue**

```vue
<template>
  <div class="my-footer">
    <h1>我的脚</h1>
    <p>{{ words }}</p>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue'
import { useStore } from 'vuex'
// import { mapState } from 'vuex'

export default defineComponent({
  // vue2的语法.  vue3兼容, 所以可以用
  // computed: { ...mapState(['words']) },
  setup() {
    // vue3 不支持辅助函数, 没有mapState
    // 用 计算属性
    const $store = useStore() //引入store

    return {
      // 利用计算属性, 读取words的值, 实际上得到的是 箭头函数的返回值
      words: computed(() => $store.state.words),
    }
  },
})
</script>

<style scoped>
.my-footer {
  background-color: blue;
  padding: 40px;
}
</style>
```



## 4.Vue实战

