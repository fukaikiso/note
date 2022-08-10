# UNIAPP

## 1 重点知识

### 1.1 面试题

### 1.1.1 移动端应用的种类

 **①NativeApp：**原生App，Android中使用Java/Kotlin开发，iOS中使用Objective-C/Swift开发。不足：费用高；优势：效率高。

 **②WebApp****：**使用HTML/CSS/JS编写，运行在浏览器中，封装为APP安装文件，在应用商店中上架。优势：一套代码可以运行在两个平台；不足：执行效率不如原生。

 **③H5****：**使用HTML/CSS/JS编写，运行在浏览器中，不需要应用商店中上架，也没有图标，通过二维码在朋友圈中快速分享。优势：一套代码可以运行在两个平台；不足：执行效率不如原生。

 **④HybridApp****：**混合/混编App，使用HTML/CSS/JS/Native.js(Java/OC=>JS)。优势：一套代码可以运行在两个平台，还可以调用系统底层原生功能；不足：执行效率不如原生。

 **⑤BridgedApp：**桥接App，只使用JS编写，执行环境会把JS编译为Java/OC，再手机中，运行时就是纯原生代码。优势：一套代码可以运行在两个平台, 执行效率高; 不足：两个平台不能做到完全一样。

 **⑥FlutterApp：**使用Dart语言开发，直接在Android/iOS手机中的显卡里进行绘图。优势：一套代码可以运行在两个平台，执行效率高，效果完全一样； 不足：全新的语言，Google开发的进度比较慢。

 **⑦小程序**

### 1.2 行业小知识

- ADB:Android Debugger Bridge，安卓调试器，是Windows和安卓系统间通信通道，类似于数据线，用于传输数据





## 2 uni-app概述

 官网：https://uniapp.dcloud.io

### 2.1 概述

 uni-app 是一个使用 Vue.js 开发所有前端应用的框架，开发者编写一套代码，可发布到iOS、Android、Web（响应式）、以及各种小程序（微信/支付宝/百度/头条/飞书/QQ/快手/钉钉/淘宝）、快应用等多个平台。

![image-20220807085730012](D:\STU\note\note\frame\assets\image-20220807085730012.png)

**演示1：创建一个示例项目，在浏览器中调试运行 —— 即uni-app编译为H5网站**

​    ①点击工具栏中的“运行”>“运行到浏览器”>“Chrome”，

​    ②HBuilder会编译整个项目为html/css/js代码，启动一款开发服务器，自动打开浏览器

 **演示2：创建一个示例项目，在安卓手机中调试运行 —— 即uni-app编译为App**

​    ①下载并安装一款安卓模拟器（例如夜神或逍遥或雷电）

​    ②在HBuilder设置adb的路径：“运行”>“运行到手机或模拟器”>“ADB路径设置”，重启HBuilder和夜神模拟器，等待一会儿（3-5分钟）....

​    ③HBuilder中编译当前项目，安装到手机中开始运行：“运行”>“运行到手机或模拟器”>“手机名称”

 **演示3：创建一个示例项目，作为微信小程序中调试运行 —— 即uni-app编译为微信小程序**

​    ①下载并安装“微信开发者工具”——用于最后一步“提请人工审核”

​    ②打开微信开发者工具的“服务端口”——就允许其他开发工具导入项目进来  

​       微信开发者工具中的“设置”>“安全设置”>“服务端口”打开即可

​    ③HBuilder中设置微信开发者工具软件的路径

​       HBuilder中点击“运行”>“运行到小程序模拟器”>“运行设置”>输入微信开发者工具的路径

​    ④编译当前uni-app为小程序代码，导出到微信开发者工具

​        HBuilder中点击“运行”>“运行到小程序模拟器”>“微信开发者工具”

   稍等片刻，微信开发者工具就会启动并打开编译好的项目

### 2.2 项目目录

项目目录介绍：

 ![img](D:\STU\note\note\frame\assets\clip_image002.jpg)

### 2.3 条件编译

 不同的运行平台终归有些专有的特性，无法实现跨平台完全兼容，例如：微信小程序导航栏右上角的关闭图标。uni-app提供了一种“条件编译”机制，可以针对特定的平台编译执行特定的代码，否则不执行。语法如下：

| 示例代码                                    |
| ------------------------------------------- |
| #ifdef H5                                   |
| 仅在H5平台下编译执行的代码                  |
| #endif                                      |
| #ifdef H5 \|\| APP \|\|  MP-WEIXIN          |
| 仅在H5和APP和微信小程序平台下编译执行的代码 |
| #endif                                      |
| #ifndef H5                                  |
| 仅在非H5平台下编译执行的代码                |
| #endif                                      |

 说明：

​    ①条件编译语句可以编写在template / style / script 等各类代码中。

​    ②更多的条件编译平台可以参见手册：https://uniapp.dcloud.io/platform

## 跨域

**main.js**

```js
import {base} from '@/service/index.js' 
Vue.prototype.$base = base
import Vue from 'vue'
// #ifdef H5
Vue.prototype.$base = '/api'
// #endif
```

**manifest.json**

```json
	"h5" : {
		"port":8080,
		"disableHostCheck":true,
		"proxy":{
			"/api":{
				"target":"http://www.codeboy.com:9999/",
				"changeOrigin":true,
				"secure":true,
				"pathRewrite":{
					"^/api":""
				}
			}
		}
	}
```

