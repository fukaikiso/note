# 微信小程序

## 1 微信公众平台

服务号     为企业、组织开放的账号，提供用户基础服务。

订阅号     为企业、组织、个人开放的账号，提供一些资讯文章的发布。

微信小程序      为企业、组织、个人开放的账号体系，可以在微信内部模拟原生的应用程序，特点：小，用完就走。

```
http://mp.weixin.qq.com
```



### 接入微信小程序

**注册账号完成后将进入小程序后台管理网站，如果有异常情况，保证是自己的微信账号的前提下依然有莫名其妙的问题，建议新建邮箱账号，重新注册。类目选择：教育。**

### 微信小程序的项目目录结构

```
TESTPRO
	app.json               全局配置文件
	app.js				   全局脚本入口文件
	app.wxss			   全局样式文件
	project.config.json    项目配置文件
	pages              	    pges存放所有的页面
		index				页面文件夹    描述小程序中的一个页面
			index.wxml      定义页面结构
			index.wxss      定义页面样式
			index.js        定义页面脚本
			index.json      定义页面配置参数
```

**结论1：**

小程序中的每一个页面由4个文件组成，分别是`wxml/wxss/js/json`。每一个页面会由一个文件夹进行包裹，存放在`pages/`文件夹下。每个文件的功能如上。

**结论2：**

`app.js` 属于全局脚本入口文件，当小程序启动时执行。用于创建`App`对象。`App`对象可以描述整个小程序应用实例。

**结论3：**

`app.wxss` 用于定义全局样式，作用于每一个页面。

**结论4：**

`app.json`用于定义全局配置文件，该配置较多，详解如下。



## 2 app.json

用于定义全局配置文件

### `pages`配置项

pages配置项用于定义当前项目中包含哪些页面，每个页面都需要配置一个路由地址。如果需要新增页面，可以直接在此配置新页面的路由地址，小程序开发工具将会自动生成四件套。

```json
"pages": [
    "pages/index/index",
    "pages/test/test"
],
```

在此配置中，下标为0的路由页面将会是打开小程序后默认显示的首页。所以希望谁是首页，只需要把该页面的路由地址配置在`pages`数组的第一位即可。

### `window`配置项

`window`配置项用于配置当前小程序的窗口表现形式：

```json
  "window": {
    "backgroundTextStyle": "dark",
    "enablePullDownRefresh": false,
    "backgroundColor": "#f00",
    
    "navigationBarBackgroundColor": "#f33",
    "navigationBarTitleText": "学子影院",
    "navigationBarTextStyle": "white"
  },
```

window中的其它配置项：

https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html#window

### `tabbar`配置项

如果小程序是一个多 `tab` 应用（客户端窗口的底部或顶部有 `tab` 栏可以切换页面），可以通过 `tabBar` 配置项指定 `tab` 栏的表现，以及 `tab` 切换时显示的对应页面。



```json
"tabBar": {
    "color": "#444",
    "selectedColor": "#d11",
    "list": [{
        "text": "电影",
        "pagePath": "pages/index/index",
        "iconPath": "/images/index_disable.png",
        "selectedIconPath": "/images/index_enable.png"
    },{
        "text": "影院",
        "pagePath": "pages/theatre/theatre",
        "iconPath": "/images/theatre_disable.png",
        "selectedIconPath": "/images/theatre_enable.png"
    },{
        "text": "我的",
        "pagePath": "pages/me/me",
        "iconPath": "/images/me_disable.png",
        "selectedIconPath": "/images/me_enable.png"
    }]
},
```

### `sitemapLocation`配置项

该配置项用于指定`sitemap.json`配置文件的路径，使小程序可以快速找到`sitemap.json`配置文件。

```
"sitemapLocation": "sitemap.json"
```

通过`sitemap.json`可以定义哪些页面允许微信官方搜索引擎收录。



## 3 微信小程序的组件库

小程序的页面结构由小程序的组件构成。即需要在`wxml`中编写小程序组件来定义页面的结构。微信小程序官方提供了很多组件，详见文档。**注意：`HTML5`的标签在`wxml`中不能使用，必须使用微信定义的组件。**

> **关于组件属性**
>
> 1. 为小程序组件的`boolean`类型属性赋值，无论直接写`true`或者`false`都将会被当做普通字符串来看待（都将会被解释为true，除非用空字符串被解释为false）。推荐为boolean类型属性赋值时使用以下语法：
>
>    ```html
>    <view hover-stop-propagation="{{true}}"></view>
>    <view hover-stop-propagation></view>
>    ```
>
> 2. 小程序组件的属性命名既可以使用驼峰命名法，也可以使用短横线命名法，二者都可实现效果：
>
>    ```html
>    <view hoverStopPropagation  hoverClass=""></view>
>    <view hover-stop-propagation hover-class=""></view>
>    ```

### `view`组件

`view`组件描述一个视图容器。类似`div`。基本使用方式如下：

```html
<view class=""      定义该组件的样式类名
      hover-class=""      定义该组件点击态的样式类名
      hover-stay-time=""
      hover-start-time=""
      hover-stop-propagation="{{true}}">
</view>
```

测试：新建页面：`pages/view/view`。



### `image`组件

`image`组件用于定义图片，基本结构：

```html
<image src="图片路径"
       lazy-load="{{true}}"  是否开启图片懒加载
       show-menu-by-long-press="长按图片是否显示操作菜单"
></image>
```

案例：新建页面：`pages/image/image`。



### `wxss`中新单位：`rpx`

`rpx`：响应式像素

`rpx`可以根据屏幕尺寸的不同动态的为组件的尺寸样式赋值。`rpx`的设计本质：**无论在任何平台下，屏幕的宽度永远都是`750rpx`。** 也就是说在较小尺寸的设备下，`750rpx`描述全屏，而在较大屏幕尺寸下，`750rpx`也一样描述的是全屏。

在不同的设备下`px`与`rpx`都会有不同的换算关系，编程时无需关系这个换算关系，只需关注：使用`rpx`作为组件尺寸单位可以在不同屏幕下等比例缩放。



### `Swiper`轮播图组件

轮播图组件用于显示轮播图：

```html
<swiper
  autoplay="{{true}}"
  interval="3000"
  duration="150"
  circular="{{true}}"
  vertical="{{true}}"
  easing-function="easeInOutCubic"
  indicator-dots="{{true}}"
  indicator-color="#444a"
  indicator-active-color="#1d1"
  
  bindchange="doChange">
	<swiper-item>图片</swiper-item>
	<swiper-item>图片</swiper-item>
	<swiper-item>图片</swiper-item>
</swiper>
```

案例：`pages/swiper/swiper`。



### `text`组件

text组件用于显示文本。

```html
<text space="nbsp|ensp|emsp"
      user-select="{{true}}"
      decode="是否解码(HTML实体)">文本内容</text>
```



### `Navigator`组件

`navigator`组件用于小程序中页面之间的跳转。基本写法如下：

```html
<navigator url="/pages/test/test" opentype="打开类型">
    点我跳转到test</navigator>
```

案例：准备3个页面：`pages/a/a`   `pages/b/b`  `pages/c/c`。

`opentype`的选择：

1. `navigate`     默认的跳转方式，如果使用这种方式进行跳转，将会保留当前页，创建目标页，然后执行动画跳转过去。不能跳转到`tabbar`页面。(因为`tabbar`页面由于优化用户体验需要常驻内存)
2. `navigateBack`   用于返回上一页，这一种方式将会销毁当前页，上一页自然而然的就显示了。也可以借助于`delta`属性回到上`n`页。
3. `switchTab`   用于跳转到`tabbar`页面。如果使用这种方式跳转到`tabbar`页面，将会销毁所有的非`tabbar`页面。
4. `redirect`   用于跳转到非`tabbar`页面。这种方式将会**销毁当前页**，创建目标页，执行动画跳转过去。
5. `reLaunch`  意为重新启动小程序，这种方式进行跳转将会销毁所有页面，重新启动应用，创建目标页，跳转过去。



### `ScrollView`组件

`ScrollView`组件用于提供可滚动的视图容器，自带水平、垂直滚动条。提供了强大的功能。详情请查阅文档。

```html
<scroll-view scroll-x="{{true}}"   开启水平滚动条
             scroll-y="{{true}}"   开启垂直滚动条
             enable-flex
             show-scrollbar
             enhanced
             >
	<view>.....</view>
	<view>.....</view>
	<view>.....</view>
</scroll-view>
```

使用上述结构，需要为`scrollview`容器定义固定的宽、高。这时如果内容超出了容器的宽高范围，`scrollview`将会出现滚动条。



### `Button`组件



### `input`组件

`input`用于描述输入框组件。

```html
<input type=""      输入框的类型   text | number | digit | idcard 
       value=""     输入框的值
       password     指定输入框是否为密码框
       placeholder=""   占位符文本
       maxlength=""   最大长度
       disabled   是否禁用输入框
/>
```

测试案例： `pages/input/input`



#### 完成`input`输入框的双向数据绑定

 **`Vue`中的双向数据绑定**

```html
<template>
	<input type="text" v-model="username">
</template>
<script>
	export default {
        data(){
            return {
                username: ''
            }
        }
    }
</script>
```

**小程序的简易双向数据绑定**

```html
<input type="text" model:value="{{username}}" />
<text>{{username}}</text>
```

```javascript
Page({
    data:{
        username: ""
    }
})
```

上述写法即可实现输入框的`value`与data中的`username`变量之间的双向数据绑定。修改任何一方，对方都会实时更新。



**小程序数据绑定的标准写法**

```html
<input type="text" bindinput="doInput"/>
{{username}}
```

```javascript
Page({
    data: {
        username: ''
    },
    doInput(event){   // 处理输入框的输入事件
        // 获取输入框的值
        let val = event.detail.value
        // 修改data.username即可完成数据绑定
        this.data.username = val   // 为username变量赋值
        this.setData({             // 调用setData()方法为变量赋值
            username: val
        })
    }
})
```



### `wxml`中的动态数据绑定

`wxml`中的动态数据绑定包含以下5种：（案例： `pages/databind/databind`）

1. 内容绑定

   ```javascript
   data: {
       name: 'zs',
       age:15,
       married: false
   }
   ```

   ```html
   <view>{{name}}</view>
   <view>{{age}}</view>
   <view>{{married}}</view>
   ```

2. 属性绑定

   ```javascript
   data: {
   	showbar: true,  
       url: '/images/1.jpg',
       num: 1
   }
   ```

   ```html
   <scroll-view show-scrollbar="{{showbar}}"></scroll-view>
   <image src="{{url}}"></image>
   <image src="/images/{{num}}.jpg"></image>
   ```

3. 样式绑定

   ```javascript
   data: {
   	className: 'v1',
       c: 'blue',
       bw: '1'
   }
   ```

   ```html
   <view class="{{className}}">xxxxx</view>
   <view style="color:{{c}}; border:{{bw}}px solid black;">xxxx</view>
   ```

   

4. 列表渲染

   类似`vue`中`v-for`，可以将`data`中的数组、对象数据遍历后显示在页面中。

   假设有一组数据：

   ```javascript
   data: {
       foods : [
           {id: 1001, name:'煎饼', price:10.0},
           {id: 1002, name:'臭豆腐', price:12.0},
           {id: 1003, name:'螺蛳粉', price:18.0},
           {id: 1004, name:'毛鸡蛋', price:5.0},
       ]
   }
   ```

   `Vue`的列表渲染：

   ```html
   <div v-for="(item,i) in foods" :key="item.id"> 
       ID：{{item.id}}, 商品名称：{{item.name}}, 商品价格：{{item.price}} 
   </div>
   ```

   微信小程序的列表渲染：

   ```html
   <view wx:for="{{foods}}"> 
       ID：{{item.id}}, 商品名称：{{item.name}}, 商品价格：{{item.price}} 
   </view>
   ```

   在小程序中对组件进行列表渲染，需要通过`wx:for`属性来实现。指的注意的是，小程序对数组进行遍历的过程中将会自动分配两个变量：`item`，`index`。item用于表示遍历过程中数组内的每个元素（对象），index用于表示遍历过程中的下标索引。这样就可以直接在组件中使用`{{item.XXX}}`访问对象属性，`{{index}}`访问对象对应的下标。

   发现控制台有一个警告：

   ```
   [WXML Runtime warning] ./pages/databind/databind.wxml
   Now you can provide attr `wx:key` for a `wx:for` to improve performance.
   ```

   如果列表中项目的位置会动态改变或者有新的项目添加到列表中，并且希望列表中的项目保持自己的特征和状态（如 [input](https://developers.weixin.qq.com/miniprogram/dev/component/input.html) 中的输入内容，[switch](https://developers.weixin.qq.com/miniprogram/dev/component/switch.html) 的选中状态），需要使用 `wx:key` 来指定列表中项目的唯一的标识符。

   `wx:key` 的值以两种形式提供

   1. 字符串，代表在 for 循环的 array 中 item 的某个 property，该 property 的值需要是列表中唯一的字符串或数字，且不能动态改变。
   2. 保留关键字 `*this` 代表在 for 循环中的 item 本身，这种表示需要 item 本身是一个唯一的字符串或者数字。

   当数据改变触发渲染层重新渲染的时候，会校正带有 key 的组件，框架会确保他们被重新排序，而不是重新创建，以确保使组件保持自身的状态，并且提高列表渲染时的效率。

   **如不提供 `wx:key`，会报一个 `warning`， 如果明确知道该列表是静态，或者不必关注其顺序，可以选择忽略。**

   `item`与`index`是`wx:for`在遍历过程中自动分配的两个变量，这两个变量可以修改名字，修改方式如下：

   ```html
   <view wx:for="{{foods}}" 
         wx:for-item="f" wx:for-index="i"> 
       Index: {{i}}
       ID：{{f.id}}
       商品名称：{{f.name}}
   </view>
   ```

5. 条件渲染

   类似于`vue`中的`v-if`。主要用于判断某些组件是否进行渲染。

   ```javascript
   data: {
   	islogin: false  // 指定用户是否已经登录   
   }
   ```

   ```html
   <view wx:if="{{islogin}}">欢迎：张三</view>
   <view wx:else>登录  注册</view>
   ```

   常用语法如下：

   ```html
   <view wx:if="{{boolean表达式}}"></view>
   ----------------------------------------------------
   <view wx:if="{{boolean表达式}}"></view>
   <view wx:else></view>
   ----------------------------------------------------
   <view wx:if="{{boolean表达式}}"></view>
   <view wx:elif="{{boolean表达式}}"></view>
   <view wx:elif="{{boolean表达式}}"></view>
   <view wx:elif="{{boolean表达式}}"></view>
   <view wx:else></view>
   ```

   

###  `radioGroup`组件

`radioGroup`用于描述`单选按钮组` 组件，里面只能包含`radio`组件，基本写法如下：

```html
<radio-group>
	<radio color="#00f" value="m" checked>男</radio>
	<radio color="#f00" value="f">女</radio>
</radio-group>
```

案例：`pages/radio/radio`。



## 4 小程序的事件处理

至此，我们已经接触了组件的以下事件：

```html
<swiper bindchange="当轮播图改变当前页时"></swiper>
<scroll-view bindscrolltoupper="当滚动到顶时" 
             bindscrolltolower="当滚动到底时"></scroll-view>
<input bindinput="当输入框内容变化时"/>
<image bindtap="当点击image组件时执行"></image>
```

### 小程序的事件类型  -  两大类

1. 冒泡事件      若触发该事件，该事件会向父节点传递。

   `WXML`的冒泡事件列表：

   | 类型        | 触发条件                                                     |
   | :---------- | :----------------------------------------------------------- |
   | touchstart  | 手指触摸动作开始                                             |
   | touchmove   | 手指触摸后移动                                               |
   | touchcancel | 手指触摸动作被打断，如来电提醒，弹窗                         |
   | touchend    | 手指触摸动作结束                                             |
   | tap         | 手指触摸后马上离开                                           |
   | longpress   | 手指触摸后，超过350ms再离开，如果指定了事件回调函数并触发了这个事件，tap事件将不被触发 |

2. 非冒泡事件      若触发该事件，该事件将不会向父节点传递。   

### 如何绑定事件？

小程序中绑定事件的方法有如下几种：

```html
<button bindtap="tapBtn">按钮</button>
<button bind:tap="tapBtn">按钮</button>
<button catchtap="tapBtn">按钮</button>
```

上述3种方式都可以给按钮绑定`tap`事件，`bind`与`bind:`的区别在于：`bind`方式可以作用于任何组件，而`bind:`对于某些**原生组件**不生效。

> 什么是原生组件？
>
> 原生组件是由`android`、`ios`操作系统直接控制的组件，而非微信小程序的自定义组件。例如：`input`、`camera`、`video`等。

而`catch`方式绑定的事件将会自动阻止事件冒泡。

### 小程序事件处理函数中参数的传递方式

在小程序中，为组件绑定事件的语法如下：

```
//wxml中
<view  bindtap="tapView"></view>

//js中
tapView(){
	执行业务
}
```

为组件绑定事件时，需要在事件属性值中写上事件处理函数的函数名：`tapView`。而且严禁后缀小括号。**那么如何在执行事件处理函数时同时传参？**

例如：

```html
<view>购物项1
	<button bindtap="tapDel" data-i="0" data-j="jj">删除</button>
</view>
<view>购物项2
	<button bindtap="tapDel" data-i="1">删除</button>
</view>
<view>购物项3
	<button bindtap="tapDel" data-i="2">删除</button>
</view>
```

```javascript
Page({
    data: {
        cart: [
            {id:1, name:xxx, price:xxx, num:xxx},
            {id:2, name:xxx, price:xxx, num:xxx},
            {id:3, name:xxx, price:xxx, num:xxx}
        ]
    }
})
tapDel(event){   
	let i = event.target.dataset.i
    let j = event.target.dataset.j
}
```



案例：吃饭睡觉打豆豆。



## 5 小程序的`API`

### 小程序界面交互类`API`

```
wx.showToast
wx.hideToast

wx.showModal

wx.showLoading
wx.hideLoading

wx.showActionSheet
```



### 小程序路由相关`API`  -- 编程式跳转

```javascript
wx.navigateTo()  保留跳转，跳转到非tabbar页面。
wx.switchTab()   切换跳转到tabbar页面。
wx.navigateBack()  销毁当前页，回到上一页。
wx.redirectTo()  销毁当前页，跳转到目标页（非tabbar页面）。
wx.reLaunch()  重启小程序，打开某一个页面。
```

```html
<navigator open-type="navigate"></navigator>
```



#### `wx.navigateTo()`

该方法用于实现保留跳转，保留当前页，跳转到非`tabbar`页面。在两个页面之间跳转的过程中可以传参。两个页面之间跳转并且传递参数的场景包含：正向传参，反向传参。

正向传参：A跳转到B，并且携带参数，在B页面中接收，处理后续业务。

在A页面中传参：

```javascript
wx.navigateTo({url: '/pages/b/b?id=1&name=zs'})
```

在B页面中接收参数：

```
Page({
	onLoad( options ){
		options封装了上一个页面传过来的参数
	}
})
```



反向传参：A跳转到B，在B页面中操作完毕后，将一些参数回传给A页面处理后续业务。

在A页面中注册接收参数的事件处理函数：

```javascript
wx.navigateTo({
    url: '/pages/b/b',
    events: {  // 定义函数，接收B页面回传回来的参数
        acceptData: (data)=>{
            data就是B页面回传回来的数据,该方法将会在B页面回传数据后立即调用
        }
    }
})
```

在B页面中代码的任何位置，编写如下代码，即可向A页面回传数据：

```javascript
let ec = this.getOpenerEventChannel() // 获取与A页面建立的事件通道对象
// 通过事件通道对象，调用emit方法通知A执行事件处理函数，并且传参
ec.emit("acceptData", '北京市')
```



## 6 微信小程序的生命周期

```
wx.redirectTo(){
	1. 加载b页面的 wxml  wxss  js  json
	调用：onLoad()钩子方法
	2. 执行js文件的代码，创建b页面的Page对象，初始化一些数据。
	3. 绘制b页面，执行一个平移动画，将b页面平移到屏幕中，盖在a页面之上。
    4. 当用户点了返回后，将b页面执行平移动画移出屏幕，释放b页面所占内存。
}
```

对于生命周期方法，最重要的点：

1. 每个生命周期方法什么时候执行（执行顺序）？
2. 每个生命周期方法执行多少次？



### 小程序`Page`对象（页面）的生命周期

小程序页面的声明周期方法包含5个：

```
  /**生命周期函数--监听页面加载 */
  onLoad(options) {
  },

  /** 生命周期函数--监听页面初次渲染完成 */
  onReady() {
  },

  /** 生命周期函数--监听页面显示 */
  onShow() {
  },

  /** 生命周期函数--监听页面隐藏 */
  onHide() {
  },

  /** 生命周期函数--监听页面卸载 */
  onUnload() {
  },
```

页面从创建到销毁的过程中，执行顺序为：

```
onLoad -- onShow -- onReady -- [ onHide -- onShow ] -- onUnload
```

以后写业务逻辑时，需要确定业务逻辑代码在那一个生命周期方法中进行编写。所以必须了解每个生命周期方法什么时候执行。执行次数。

```
onLoad  执行一次
onShow  执行多次  重新回到当前页时也会执行
onReady 执行一次
onHide  执行多次  当前页跳转到其他页面时，就会执行
onUnload  执行一次
```



### 小程序`App`对象（应用，在`app.js`中定义）的生命周期

```
  onLaunch(){
    // 当小程序应用启动时执行   一个生命周期执行一次
  },
  onShow(){
    // 当小程序在前台显示时执行，可以执行多次
  },
  onHide(){
    // 当小程序被隐藏到后台时执行，可以执行多次
  }
```

`app.js`文件属于`js`全局入口文件，小程序启动时，加载并执行该`js`。即会在小程序启动时创建`App`对象。该对象在小程序生命中有且仅有一个。该对象中可以任意自定义属性来存储全局共享的数据。



### 小程序网络`API`

在小程序中发送`https`请求，代码如下：

```javascript
wx.request()
```

测试项目服务端接口：

```
https://api.tedu.cn/index.php?cid=1
```

如果访问不了`tedu.cn`，可以修改`DNS`：

右键屏幕右下角的网络 -- 打开网络设置 -- 更改适配器选项  -- 右键自己的网络 -- 属性  -- 双击`Internet 协议版本4`  -- 手动设置`DNS`：`114.114.114.114`。-- 确定。

```javascript
wx.request({
    url: '请求地址',
    method: 'GET',
    data: {}, 请求参数,
    success: (res)=>{ 请求成功后执行的回调方法 },
    fail: (err)=>{ 请求失败后执行的回调方法 }
})
```

`pages/req/req`测试发请求的`API`。

![image-20220722134356976](C:\Users\web\AppData\Roaming\Typora\typora-user-images\image-20220722134356976.png)

出现上述错误，需要将https://api.tedu.cn域名添加到合法域名列表中。

#### 域名配置流程

**扫码登录，http://mp.weixin.qq.com ，进入小程序后台管理网站。**

服务器域名请在 「小程序后台 - 开发管理 - 开发设置 - 服务器域名」 中进行配置。

将https://api.tedu.cn域名添加到合法域名列表。



## 7 学子影院项目实践



### 搭建项目的基本结构

1. 新建项目。`xzyy`
2. 将图片资源复制，粘贴到项目中。
3. 搭建项目的主体结构：三个底部选项卡对应三个页面。`index`  `theatre`  `me`。
4. 微调。准备完毕，开始实现业务。



### 加载首页热映类别下的电影列表

```
https://api.tedu.cn/index.php?cid=1
```

加载电影列表接口如下：

|          | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| 请求地址 | `https://api.tedu.cn/index.php`                              |
| 请求方式 | `GET`                                                        |
| 请求参数 | `cid`: 电影类别`ID`     热映：1    待映：2    经典：3<br>`offset`: 读取数据的起始下标位置  [可选] |
| 返回结果 | 返回相应`cid`类别下的文章列表。从`offset`的下标位置向后查询20条返回。 |

```
https://api.tedu.cn/index.php?cid=1
https://api.tedu.cn/index.php?cid=1&offset=20
经典类别下  下标为25的电影是哪一部？
https://api.tedu.cn/index.php?cid=3&offset=25
```

实现思路：

1. 在`onload`中发送请求，加载首页的电影列表。
2. 将返回的结果存入`data`。
3. 在页面中，通过`wx:for`完成列表渲染。



### 处理顶部导航的选中项的样式

1. 需要在data中声明一个变量：`cid`用于表示当前选中项的类别ID。

2. `cid`的值决定了页面中那一个`text`拥有选中状态的`class`类名。

   ```html
   <text class="hot-item {{cid==1?'hot-item-active':''}}">热映</text>
   ```

3. 这样，可以为三个`text`绑定`tap`事件，点击某一个导航项后，修改`data.cid`的值，改为当前选中项的类别ID值。这样，页面也会动态更新。

4. 不仅要处理样式，还要实现当点击顶部导航后，重新发送请求，访问当前类别下的电影列表。

5. 一旦获取响应结果之后，替换`this.data.movies`，更新`ui`即可。



### 实现触底加载下一页

1. 监听小程序页面的触底事件。

2. 一旦滚到底，再次发送`https`请求，传递参数：`cid`、`offset`。通过这两个参数加载当前类别的下一页数据。

   ```
   https://api.tedu.cn/index.php?cid=1&offset=0    第一页
   https://api.tedu.cn/index.php?cid=1&offset=20   第二页
   https://api.tedu.cn/index.php?cid=1&offset=40   第三页
   .
   .
   https://api.tedu.cn/index.php?cid=1&offset=80   第五页
   ```

3. 获取下一页电影列表后，把结果列表追加到`this.data.movies`数组的末尾。更新列表即可。



### 封装`loadData`方法，加载电影列表

我们发现，当`onLoad`时、`tapNav`时、`onReachBottom`时都需要发送`https`请求加载电影列表，所不同的是，不同场景下传递的参数不同，拿到结果后处理的后续业务不同。所以有必要封装一个方法：`loadData`方法，用于发送加载电影列表请求，并且返回最终列表查询结果。

```javascript
// 回调方法的设计
loadData(cid, offset, callback){
    // 发送请求，加载热映类别下 首页的电影列表
    wx.request({
        url: 'https://api.tedu.cn/index.php',
        method: 'GET',
        data: {cid,  offset},
        success: (res)=>{
            console.log("加载首页数据：", res)
            callback(res.data)  // 通过回调方法的方式返回
        }
    })
}

// 基于Promise的设计
loadData(cid, offset){
    return new Promise((resolve, reject)=>{
    	// 发送请求，加载热映类别下 首页的电影列表
        wx.request({
            url: 'https://api.tedu.cn/index.php',
            method: 'GET',
            data: {cid,  offset},
            success: (res)=>{
                console.log("加载首页数据：", res)
                resolve(res.data)
            }
        })    
    }) 
}

onLoad(){
	this.loadData(1, 0).then((data)=>{
        data就是Promise通过resolve回传回来的res.data 数组
    })
},
    
tapNav(){
    this.loadData(xxx, 0)
}

onReachBottom(){
	this.loadData(xxxx, xxxx)
}
```



#### 小程序缓存设计方案

**什么是缓存？**

客户端发送第一次请求，加载列表数据，加载完毕后将数据保存在客户端中（客户端缓存）。这样当客户端再次发送相同请求时，就可以先去缓存中找一圈，看以前存过没，如果存过，直接拿来用。如果没存过，再发请求。

**如何使用小程序在客户端缓存中存储数据？**

```javascript
wx.setStorage({
    key: '自定义key值',
    data: '具体数据'
})
```

**如何使用小程序从客户端缓存中取出数据？**

```javascript
wx.getStorage({
    key: '自定义key值',
    success: (data)=>{},
    fail: (err)=>{}
})
```

**缓存的实现麻烦在需要根据不同的项目的业务形态，来选择合适的时机更新缓存。**常见的缓存方案：

1. 有的缓存定时更新。每天早上更新、每小时更新、每分钟更新等。
2. 有的缓存第一次打开时更新。     进入小程序时，删掉缓存即可。
3. 通常情况下，都会为列表提供一个下拉刷新操作。加载最新数据的同时更新缓存。



#### 基于下拉刷新更新列表，并更新缓存

1. 开启当前页面的下拉刷新功能。

   在页面的`json`配置文件中，开启下拉刷新功能。

   ```javascript
   {
     "usingComponents": {},
     "enablePullDownRefresh": true,
     "backgroundColor": "#444"
   }
   ```

2. 当监听到用户下拉刷新操作时，发送`https`请求，加载最新数据，更新列表，更新缓存。

   ```javascript
   Page({
       onPullDownRefresh(){
           ....
       }
   })
   ```

   



### 小程序的位置信息-更新左上角城市名

微信小程序提供了一个`API`用于获取客户端的经纬度：

```javascript
wx.getLocation({
    ....
    success: (res)=>{
        .....
    }
})
```

如果除了经纬度之外还需要做**逆地理编码（通过经纬度获取具体地名字符串）**，这个方法就不够用了，需要接入第三方的位置服务：腾讯位置服务。



#### 接入第三方的位置服务：腾讯位置服务 - `lbs.qq.com`

![image-20220725142038574](C:\Users\web\AppData\Roaming\Typora\typora-user-images\image-20220725142038574.png)



1. 登录`lbs.qq.com`。

2. 点击右上角 -- 控制台，进入后台管理页面。打开我的应用。

   ![image-20220725143913671](C:\Users\web\AppData\Roaming\Typora\typora-user-images\image-20220725143913671.png)

3. 创建应用：

   ![image-20220725144256258](C:\Users\web\AppData\Roaming\Typora\typora-user-images\image-20220725144256258.png)

4. 填写表单申请`key`：

   ![image-20220725144752088](C:\Users\web\AppData\Roaming\Typora\typora-user-images\image-20220725144752088.png)

5. 在小程序管理后台，将`https://apis.map.qq.com`添加到合法域名列表中。

   在[小程序管理后台](https://mp.weixin.qq.com/wxamp/home/guide) -> 开发 -> 开发管理 -> 开发设置 -> “服务器域名” 中设置request合法域名，添加https://apis.map.qq.com。

   在小程序开发工具中，验证，是否添加成功：

   ![image-20220725145811973](C:\Users\web\AppData\Roaming\Typora\typora-user-images\image-20220725145811973.png)

6. 写代码访问腾讯位置服务。

   ```javascript
   // 引入SDK核心类，js文件根据自己业务，位置可自行放置
   var QQMapWX = require('../../libs/qqmap-wx-jssdk.js');
   var qqmapsdk = new QQMapWX({
       key: '申请的key'
   });
   qqmapsdk.search({
       keyword: '酒店',
       success: (res)=>{  查询成功 res结果..  },
       fail: (err)=>{ 查询失败 }
   })
   ```

   

### 小程序的位置信息-更新左上角城市名

1. 封装一个方法：`getLocationInfo()` 用于获取城市名称，在`onLoad`时调用该方法。

2. 在`getLocationInfo()`方法中访问腾讯位置服务，调用`reverseGeocoder`方法获取城市名称（需要在`app.json`配置权限）。

   ```javascript
   getLocationInfo(){
       let QQMapWX = require('../../libs/qqmap-wx-jssdk')
       let qqmapsdk = new QQMapWX({
           key: 'A7CBZ-FZ73U-PUPV7-BINEG-ICD57-KAB6J'
       })
       qqmapsdk.reverseGeocoder({
           success: (res)=>{
               ..... res.result.address_component.city
           }
       })
   }
   ```

   `app.json`，申请定位权限。

   ```json
   "permission": {
       "scope.userLocation": {
           "desc": "赶紧给我权限，不给手机爆炸，5/4/3/2.."
       }
   },
   ```

3. 将`city`在页面中显示出来。在`data`中声明变量：`city`。



### 实现电影详情页

1. 下载 `movie.wxss` `movie.wxml`，创建页面：`pages/movie/movie`。替换掉`wxml`与`wxss`即可。

2. 点击首页列表项，跳转到详情页，显示电影详情。

   1. 跳转的过程需要传参：需要将选中项电影的ID传递给`movie`页面。
   2. 在`movie`页面中接收ID，发送`https`请求加载当前ID的电影详细信息。
   3. 获取到详细信息后，渲染页面。

   |          | 说明                             |
   | -------- | -------------------------------- |
   | 请求地址 | `https://api.tedu.cn/detail.php` |
   | 请求方式 | `GET`                            |
   | 请求参数 | `id`:待查询的电影ID              |
   | 返回结果 | 相应ID的电影的详细数据           |

   ```
   https://api.tedu.cn/detail.php?id=233
   ```

   

#### 渲染页面

1. 渲染头部基本信息区域。

2. 渲染简介区域。

3. 渲染演职人员列表 与 导演列表。

4. 渲染剧照列表。

   1. 将剧照列表显示出来。`mode="aspectFill"`

   2. 点击剧照图片，打开新窗口，以高清大图方式显示剧照图片列表。

      ```javascript
      wx.previewImage()
      ```

   3. 重新修改每一个图片的路径，改为高清图片（去掉@后缀）

   4. 点击剧照中的某一张时，需要向事件处理函数传递参数`index`，显示当前选中的图片。

   5. 处理事件委托。



## 8 小程序云开发

腾讯拿出一部分云服务器为小程序开发者准备了一整套开发后端程序的云开发架构。使得小程序开发者可以不必过多了解后端知识，也可以完成正常的前后端交互。

云开发提供的基本能力有：

1. 云数据库    云开发提供了一个云端数据库可以让小程序开发者直接在小程序端直接操作数据的增删改查。
2. 云存储   云开发提供了一个云服务资源用于文件存储。可以让小程序开发者在小程序端直接进行文件的上传于下载。
3. 云函数   云开发提供了一个云服务器资源用于提供网络服务接口。可以让小程序开发者在小程序端编写函数，通过开发工具将函数部署至云端，并且在小程序端调用这些云端函数。



### 接入云开发平台

打开小程序开发工具，点击工具栏中的云开发按钮，开通云开发。

填写云服务器的名字（`web2203`），选择个人账户预付款-资源均衡性-0元/月免费版

点击确定后，小程序将会为开发者分配云服务器资源（初始化）等待即可。



### 云数据库

云数据库是一个可以让小程序开发者在前端直接操作的云端数据库。与`mysql`不同，云数据库是一款基于`json`的非关系型数据库。

mysql:

| id   | name | age  | gender | school_id |
| ---- | ---- | ---- | ------ | --------- |
| 1    | zs   | 18   | m      | 1         |
| 2    | ls   | 19   | f      | 2         |
| 3    | ww   | 20   | m      | 1         |

| id   | name     | loc    | area |
| ---- | -------- | ------ | ---- |
| 1    | 清华大学 | 五道口 | 1000 |
| 2    | 北京大学 | 中关村 | 850  |

小程序云数据库：

```json
[
    {
        id:1,
        name:zs,
        age:18,
        gender:m,
        school: {
            id:1,
            name: 清华大学,
            loc: 五道口,
            area: 1000
        }
    },
    {
        id:2,
        name:ls,
        age:19,
        gender:f,
        school: {
            id:2,
            name: 北京大学,
            loc: 中关村,
            area: 850
        }
    },
    {
        id:3,
        name:ww,
        age:20,
        gender:m,
        school: {
            id:1,
            name: 清华大学,
            loc: 五道口,
            area: 1000
        }
    }
]
```

上述数据，从云数据库的角度可以如下描述：

有一个**集合**，里面存储了3条**记录**（3篇**文档**），每一条记录包含5个**字段**。不同的字段拥有不同的数据类型。其中`school`字段属于**对象类型**，包含4个**属性**。



### 通过小程序提供的相关`API`操作云数据库



#### 添加数据

```javascript
let db = wx.cloud.database()
db.collection('test').add({
    data: {待添加的对象},
    success: (res)=>{
        console.log(添加成功后的回调)
    }
})
```

案例：点击按钮，向test集合中添加一条记录。

1. 新建云开发项目。选择**使用云开发**。
2. 新建页面：`pages/db/db`，设计个按钮，点击后添加一条记录。

**注意事项**

当使用`collection.add()`方法添加新记录时，小程序不仅会将该记录添加到集合中，而且会为该记录分配两个字段：`_id`    `_openid`。

`_id`: 自动生成的当前文档的主键ID。（不重复）

`_openid`: 该字段用于表明当前记录属于哪一个用户。同一个用户向集合中添加的记录所自动生成的`_openid`字段值是相同的。云数据库使用该字段可以方便的解决集合的权限问题。



#### 查询数据

通过ID查询一条记录

```javascript
let db = wx.cloud.database({env: 环境ID});
db.collection('test').doc("记录 _id").get({
    success: (res)=>{
        res就是查询结果
    }
})
```

通过where条件查询多条记录

```javascript
let db = wx.cloud.database({env: 环境ID});
db.collection('test').where({
    gender: '男'
}).get().then(res=>{
    
})
```



### 实现学子影院详情评论列表的展示

1. 新建云开发项目。学子影院云开发版         `/day07/demo/xzyycloud`

2. 将`xzyy`中的资源拖拽到新项目的`miniprogram`中即可。

   ```
   需要拖拽的资源：
   /images
   /libs
   /pages
   app.js
   app.json
   app.wxss
   ```

3. 打开详情页面，在`onLoad`的时候，查询云数据库，获取当前电影的影评列表。

4. 在页面中完成列表渲染。



### `Collection`对象

`db.collection('test')`可以获取操作`test`集合的`Collection`对象：

| 方法                | 说明               |
| ------------------- | ------------------ |
| Collection.doc()    | 通过ID查询一条记录 |
| Collection.get()    | 开启查询云数据库   |
| Collection.where()  | 添加筛选条件       |
| Collection.skip(n)  | 跳过n行            |
| Collection.limit(n) | 向后查询n条        |
| Collection.add()    | 添加记录           |
| Collection.update() | 修改记录           |
| Collection.remove() | 删除记录           |
| ...                 | ...                |

如何查询年龄小于30的用户？

```javascript
let _ = db.command
db.collection('test').where({
    age: _.lt(30)
}).get()
```

API 提供了以下查询指令：

| 查询指令 | 说明                 |
| :------- | :------------------- |
| eq       | 等于                 |
| neq      | 不等于               |
| lt       | 小于                 |
| lte      | 小于或等于           |
| gt       | 大于                 |
| gte      | 大于或等于           |
| in       | 字段值在给定数组中   |
| nin      | 字段值不在给定数组中 |

更多具体的查询指令 `API` 文档可参考[数据库 API 文档](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/reference-sdk-api/database/Command.html)。



### 在首页中实现选择城市业务

在首页中，点击左上角城市名，跳转页面，进入城市列表页，在城市列表页选择一个城市，返回首页，更新左上角城市名称。

1. 新建城市列表页面。`pages/citylist/citylist`。

2. 在城市列表页中显示所有的城市信息。

   1. 点击侧边栏字母后，将`scrollview`滚动到相应位置：

      ```html
      <scroll-view scroll-into-view="{{letter}}">
          <view id="A">A</view>
          <view id="B">B</view>
          <view id="C">C</view>
          <view id="D">D</view>
         	...
      </scroll-view>
      ```

3. 点击某一个城市，回传给首页。

   首页中点击左上角，跳转到城市列表页。

   在城市列表页中选择某一个城市，获取城市名称，<span style="color:red">将城市名称存入app.js中（全局唯一，全局共享）</span>

   ```javascript
   getApp().globalData.city = '北京市'
   ```

   当回到首页后，将会执行`onShow`生命周期方法，可以在此处访问`app.js`，拿到城市名称，更新左上角。

   ```javascript
   let c = getApp().globalData.city
   this.setData({city : c})
   ```

4. 在首页中拿到数据后，更新左上角城市名称。

5. 在城市列表页中重新加载当前城市信息。

6. 点击当前城市名称`text`后，将城市名称存入`globalData`，回到上一页。



### 处理未授权时的城市选择业务

点击重新授权，弹出引导窗口，引导用户进入设置页，修改权限。



### 加载影院模块影院列表

点击影院底部选项卡，在影院页面中加载当前选中城市的电影院列表。

**实现步骤**

1. 去`ftp`下载 `theatre.zip`。解压之后将四件套覆盖现有的`theatre`目录。
2. 加载当前城市名。
3. 加载当前城市中所有的电影院。
4. 列表渲染。



### `event.target`与`event.currentTarget`的区别

二者都是用于获取事件源对象，不同的是`event.target`拿到的是点击时的最底层的子元素；而`event.currentTarget`拿到的是绑定事件的那个元素（无论是冒泡触发的，还是直接触发的）

```html
<view class="v1" bindtap="tapview" data-i="1">
	<view class="v2" data-i="2"></view>
</view>
```

```javascript
tapview(event){
    event.target
    event.currentTarget
}
```

当点击v2，触发tap事件，该事件由于冒泡，也将执行v1的tapview方法：

event.target:     **v2**     因为点击的最底层的元素是v2。

event.currentTarget:      **v1**    因为事件处理函数绑定在v1上。

当点击v1，触发tap事件，该事件也将执行tapview方法：

event.target:     **v1**   因为点击的最底层的元素是v1。

event.currentTarget:   **v1**    因为事件处理函数绑定在v1上。



### 小程序自定义组件

微信官方提供了很多组件用于编写页面结构。有很多团队在此基础之上重新封装了很多好用的组件组成了小程序自定义组件库。例如：`vant`组件库。可以使用如下标签来编写页面结构：

```html
<van-button></van-button>
<van-cell></van-cell>
<van-image></van-image>
......
```

小程序开放了一些自定义组件的接口，可以允许用户进行组件化编程。

#### 基于自定义组件制作一个自己的按钮组件

```html
<my-button title="按钮上的字" 
           color="按钮的颜色" 
           round
           bind:doubletap="handleDoubletap"></my-button>

handleDoubletap(){
	console.log('么么哒...')
}
```



#### 创建一个自定义组件

1. 新建小程序`Component`，（小程序开发工具右键即可选择新建组件）。

2. 在组件的wxml中编写组件的基本结构，在wxss中编写组件的基础样式。

3. 当需要使用该组件时，在`json`配置文件中引入该组件，然后再页面里就可以通过自定义组件标签使用该组件。

   ```json
   me.json
   {
       "usingComponents": {
           "my-button": "/components/mybutton/index"
           自定义标签名 :  组件路径
       }
   }
   ```

   ```html
   me.wxml
   <my-button></my-button>
   ```

   

#### 为自定义组件设计自定义属性

```html
<my-button title="按钮上的字"></my-button>
```

`my-button`组件在显示文本时，需要查看组件的`title`属性，`title`属性是什么，按钮上就显示什么。

1. 在组件的`index.js`中，声明该自定义属性：

   ```javascript
   Component({
       properties: {
           "title" : {
               type: String,
               value: '按钮文本'   // 属性默认值：按钮文本
           }
       }
   })
   ```

2. 在组件的wxml中使用该属性一起渲染组件显示效果：

   ```html
   <view class="button">{{title}}</view>
   ```

3. 在使用该组建时，为该属性赋值（传参）：

   ```html
   <my-button title="重新赋值新文本"></my-button>
   ```

   

#### 为组件设计自定义事件

1. 在使用子组件时，经常需要捕获到子组件执行过程中的某一个时间节点后执行某些业务逻辑。就需要为组件设计自定义事件。

   ```html
   <scroll-view bind:scolltoupper=""></scroll-view>
   <input bind:input=""/>
   <my-button bind:doubletap=""></my-button>
   ```

   自定义事件的流程：

   1. 在子组件内部通过捕获基础事件找到触发自定义事件的时间节点。
   2. 调用`this.triggerEvent()`触发该自定义事件。
   3. 如果父组件在使用该子组件时，绑定了该自定义事件的处理函数，则会自动调用。



### `Vant`组件库

下载安装并且引入：

1. 通过`npm`命令，初始化项目，安装`vant`组件库。

   ```shell
   # 进入项目的miniprogram文件夹后执行命令：
   npm init -y
   npm i @vant/weapp -S --production
   ```

   完毕后，将会在`miniprogram`文件夹下出现`package.json`与`node_modules`文件夹。

2. 修改`app.json`，去掉`style:'v2'`。

3. 点击小程序开发工具左上角：工具--构建`npm`。即可完成代码的编译构建。

   一旦构建完毕后，小程序开发工具将会把`node_modules`中的源代码编译到`miniprogram_npm`目录下。

4. 开始使用`vant`组件库。

   



### 微信登录

微信小程序官方提供了一个获取用户微信昵称、头像等资料的`API`：

```
wx.getUserProfile({
	success: (res)=>{
	
	}
})
```

通过`success`可以获取微信的昵称与头像。

如果希望实现一个完整的登录业务（可以在小程序中自己维护用户信息、修改头像、昵称、新增手机号、身份证号等字段），必然需要将用户数据存自己家数据库。而不是每次使用都去直接访问微信。

**所以一个完整的登录流程如下：**

1. 在自家数据库中建用户表，收集用户数据：

   | id   | openid  | nickName | avatarUrl     | age  | phone   | ...  |
   | ---- | ------- | -------- | ------------- | ---- | ------- | ---- |
   | 1    | 568sd5a | zs       | http://zs.jpg | 11   | 1333333 | ...  |
   | 2    | 6845945 | ls       | http://ls.jpg | 13   | 1444444 | ...  |
   | ...  | ...     | ...      | ...           | ...  | ...     | ...  |

2. 当用户第一次微信登录时，需要将用户的信息存入自家数据库。

3. 当用户再次登录时，拿到微信信息后，还需要查询自己家数据库该用户信息，获取最新的头像、昵称，显示在界面中。



### 登录成功后实现头像的修改

登录成功后，点击头像，跳转到图库（打开摄像机拍照）选择图片。更新`avatarUrl`。但是这种操作只能本地修改，如果重新登录，头像依然是微信头像。如果希望持久化保存头像，需要将头像上传到文件服务器，把`users`数据库中的头像访问路径更新掉才可以。

#### 本地头像的修改

登录成功后，点击头像，跳转到图库（打开摄像机拍照）选择图片。更新`avatarUrl`。

```javascript
wx.chooseMedia({
    count: 1,
    mediaType: ['image'],
    success: (res)=>{
    	....  
        let path = res.tempFiles[0].tempFilePath
    }
})
```



#### 持久化修改头像

1. 小程序通过`wx.chooseMedia`方法选择图片，获取选中图片的路径。
2. 将选中的图片上传至服务器，从而获取一个可以在任何网络环境下都可以直接访问的图片链接地址：`https://host/xxx/xxxx/xxx.jpg` 。在此，可以将图片上传至小程序**云存储**空间。云存储类似一个网盘，小程序可以通过`API`实现文件的上传与下载。
3. 上传完毕后，将会立即得到访问该图片的路径。
4. 将访问路径更新到云数据库的`avatarUrl`字段即可。这样当以后用户登录时，就可以直接拿到最新的头像路径，从云存储中访问头像图片。



#### 云存储上传文件`API`

在小程序端通过以下代码实现文件的上传：

```javascript
wx.cloud.uploadFile({
    filePath: '',     // 本地待上传文件的路径
    cloudPath: '',    // 上传至云存储后，在云端存储时使用的文件路径（不可重复）
    success: (res)=>{
        .....
    }
})
```















































































































































































