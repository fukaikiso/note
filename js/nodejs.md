# Nodejs全栈

## 1 Nodejs基础

[nodejs文档]([API 文档 | Node.js 中文网 (nodejs.cn)](http://nodejs.cn/api-v16/index.html))

- npm nodemon 实时监测文件变化，重启服务器

### 1.1 全局对象

（1） Node.js环境中全局对象为global

（2） Node.js环境声明的变量不会被添加到全局对象中，变量声明后只能在当前文件中使用

```javascript
var message = "hello"
console.log(global.message) //undefined
```



### 1.2 模块系统

（1）Node.js默认支持某块系统，该系统遵循CommonJS规范

（2）一个Javascript文件就是一个模块，在模块文件中定义的变量和函数默认只能在模块文件内部使用，如果需要在其他文件中使用，必须显式声明将其进行导出

#### 1.2.1 内置模块

（1）引用内置模块不需要添加路径

（2）常用内置模块：

- global: 全局模块/全局对象，不需要引入
- console: 控制台
- path : 模块内提供了一些和路径操作相关的方法
- fs : 文件操作系统，提供了和操作文件相关的方法
- http: 处理网络客户端的请求
- url: 处理客户端请求过来的url
- querystring: 查询字符串，处理客户端通过get/post请求传递过来的参数 
- util
- ...

**global**

```js
//浏览器端，每个JS文件都是全局作用域，存在全局污染
//Node.js，每个JS文件都是一个独立的作用域，不存在全局污染

// 在nodejs下,每一个文件就是一个独立的模块
//nodejs会自动给每一个js文件里的代码添加一个匿名函数,
//文件里所有的代码都包含在这个函数中,
//这个函数中有五个参数
//__dirname 当前模块的绝对路径
//__filename  当前模块的绝对路径+模块名称
//module:当前模块对象,module.exports:当前模块的导出对象
//require:一个函数,用来导入其他模块,返回值是导入模块的内容
//exports:module.exports的别名,指向同一个对象
(function(__dirname,__filename){
	console.log(__dirname);
	console.log(__filename);
	var js02 = require('./02.js');
	console.log(js02)
})

//导入模块
const fs = require('fs')

//导出模块
module.exports = {...}
```

**console**

```js
console.log(1);//打印日志
console.info(2);//打印消息
console.warn(3);//打印警告
console.error(4);//打印错误

//计时，注意time和timeEnd中参数需要一致
console.time('tao');
for(var i=1;i<=100000;i++){
}
//结束计时
console.timeEnd('tao');

```

**process**

```js
//进程:系统上的每个软件运行都是代表一个进程，进程占用一定的CPU、内存
process.arch //查看当前CPU架构   //'x64'
process.platform //查看当前的操作系统  //'win32'
process.pid //查看当前进程的编号，随机生成  //996
process.kill() //用于结束指定编号的进程

//立即执行
//process.nextTick(回调函数:()=>{ })
```

**Buffer**

```js
//缓冲区:是内存中的一块区域，用于临时存储数据

//创建Buffer，分配空间,大小为5个字节，并存储字符
//一个汉字占3个字节
var buf=Buffer.alloc(9,'abc涛');//alloc 分配
console.log(buf);
//将buffer数据转为字符串
console.log(buf.toString());

```

**timer**

（1）一次性定时器

```js
//setTimeout(回调函数,间隔时间)
//回调函数，把函数作为参数传递，内部会自动调用
//3000毫秒以后会自动调函数
//3000毫秒以后，回调函数才会进入到事件队列
var timer=setTimeout(function(){//setTimeout 暂停
   console.log('boom!')
},3000);
console.log(2);//先2然后3秒之后boom!
//清除 clear 
clearTimeout(timer);
```

（2）周期性定时器

```js
//setInterval(回调函数,间隔时间)
//周期性定时器
//每隔2000毫秒，把回调函数放入到事件队列
var timer=setInterval(function(){
    console.log('嘀嘀嘀')
},2000);
console.log(2);//先2然后2秒之后嘀嘀嘀
//清除
clearInterval(timer);
```

（3）立即执行定时器

```js
//setImmediate(回调函数:()=>{ })/clearImmediate()
```

**querystring**

```js
//查询字符串：浏览器端向服务器端传递参数的一种形式，位于网址中
//http://www.code.com:9999/products.html?kw=小米&a=1

//解析网址查询字符串
//querystring.decode()=querystring.decode()
//引入查询字符串模块
//核心模块自动会到安装目录下去寻找
const querystring=require('querystring');
//查询字符串
var str='user=tao&pwd=123456';
//获取传递的值，使用引入的模块中提供的方法
var obj=querystring.parse(str);
//获取传递的值，使用引入的模块中提供的方法
console.log(obj);
console.log(`登录成功! 用户名: ${obj.user} 密码: ${obj.pwd}`);

//序列化为网址查询字符串的对象
//querystring.encode()=querystring.encode()

```

**url**

```js
//网址模块(URL)：统一资源定位，互联网上的任何资源都有对应的网址；最终通过网址获取服务器端的资源
//http://www.code.com:9999/product_details.html?lid=1
//协议    域名/IP地址   端口 请求的服务器端资源  查询字符串
//http 不加密协议     https 加密协议

//new URL()
const myURL = new URL( 'https://example.org?user=abc&psw=123');
// https://example.org

//获取和设置网址的序列化的查询部分
//url.search
//获取表示网址查询参数的 URLSearchParams 对象
//url.searchParams
```

**http模块**

```js
//WEB服务器：为浏览器提供资源的服务器，例如：网页，图片，数据...
//HTTP协议：超文本传输协议，是浏览器端和WEB服务器之间的通信协议
//(1)通用头信息
//既包含一部分请求的也包含一部分响应
//Request URL:要请求的资源 http://www.codeboy.com:9999/
//Request Method:请求的方法，对资源的操作方式，get/post...
//Status Code:响应的状态码:200ok
//(2)响应头信息(Response,服务器端发出的)
//Location:设置要跳转的URL,通常结合着状态码302使用
//Content-Type:响应的内容类型，解决中文乱码'text/html;charset=utf-8'
//(3)请求头信息(Request,浏览器发出的)

//使用http模块可以创建WEB服务器，为浏览器提供服务
// 引入http模块
const http = require('http')
// 创建web服务器
const app = http.createServer()
// 设置端口
app.listen(3000,()=>{console.log('服务器启动成功')})
// 本地服务器ip  127.0.0.1或者localhost
// 使用浏览器访问   http://127.0.0.1:3000   或者  http://localhost:3000  其中http://可以省略

//引入http模块
const http=require('http');
//创建WEB服务器
const app=http.createServer();
//设置端口
app.listen(3000,()=>{
    console.log('服务器启动成功');
});
//接收请求，做出响应
//监听请求，如果有请求自动调用回调函数
app.on('request',(req,res)=>{
    //判断请求的资源
if(req.url=='/login'){
    res.setHeader('Content-Type','text/html;charset=utf-8');
    res.write('登录成功');
}else if(req.url=='/study'){
    res.statusCode=302;
    res.setHeader('Location','https://www.tmooc.cn/');
}else{
    res.statusCode=404;
    res.write('Not Found');
}
   //无论要响应任何内容，最后都会结束并发送
    res.end();
});

```

**fs**

```js
//1.读取目录
//异步
//fs.readdir(path,()=>{ })
//同步
//fs.readdirSync(path)
//读取结果是数组
const fs = require('fs')
fs.readdir('../day03',function(err,result){
    //err可能产生的错误，如果有错误抛出
    if(err){
        throw err;
    }
    //arr读取成功的结果
    console.log(result);
});//readdir 读取目录

//2.清空写入
//fs.writeFile(pat,data,()=>{})
//fs.writeFileSync(pat,data)


//3.追加写入
//fs.appendFile(pat,data,()=>{})
//fs.appendFileSync(pat,data)

//4.读取文件
//fs.readFile(path,()=>{})
//fs.readFileSync(path)
//读取结果格式为buffer,需要保存到一个变量并调用toString()

//5.删除文件
//fs.unlink(path,()=>{ })
//fs.unlinkSync(path)

//6.检测文件是否存在
//fs.existsSync(path)

//7.拷贝文件
//fs.copyFile(path,file,()=>{ })
//fs.copyFileSync(path,file)

//8.查看文件状态
//stat(path,()=>{})
//statSync(path)
//是否为目录： isDirectory()
//是否为文件： isFile()

//9.创建目录
//mkdir(path,()=>{})
//mkdirSync(path)
```

**stream**

```js
//createReadStream() 创建可以读取的文件流
//createWriteStream() 创建可以写入的文件流
//pipe() 管道，可以将读取的流添加到写入的流，最终完成文件拷贝事件名称,回调函数
//on('data',()=>{ }) 添加事件，用于监听某一个操作，一旦监听到会自动调用回调函数；事件名称是固定的字符串形式

//引入fs系统模块
const fs=require('fs');
//使用流的方式读取文件,文件分为很多段
var rs=fs.createReadStream('./1.mp4');
//使用流的方式写入文件,会创建空文件
var ws=fs.createWriteStream('./2.mp4');
//把读取的流添加到写入的流
//pipe 管道
rs.pipe(ws); //'./1.mp4'拷贝文件为'./2.mp4'
```

#### 1.2.2 自定义模块

```javascript
//模块导出
//模块文件都有一个module对象，保存和当前模块相关信息
//在模块对象中有一个属性 exports，它的值是一个对象，模块内部需要被导出的成员都应该存储在到这个对象中
console.log('你好')
function msg(name){
    console.log('hello,'+name)
}
module.exports = msg

//模块导入
//模块导入会立即执行导入模块的代码
//在导入其他模块时，建议使用 const 关键字声明常量，防止模块被重置
const express = require('express')
const msg = require('./module')
msg('world')
//你好
//hello,world
```

### 1.3 NPM

**NPM** : Node Package Manger,用于管理Node软件包

[npm文档]([npm 中文文档 | npm 中文网 (npmjs.cn)](https://www.npmjs.cn/))

#### 1.3.1 package.json

（1）package.json文件用于描述应用程序

（2）创建pakage.json文件命令

- 创建 `npm init`
- 快速创建`npm init -y`，即 `npm init -yes`

| 属性         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| name         | 包名                                                         |
| version      | 包的版本号                                                   |
| description  | 包的描述                                                     |
| homepage     | 包的描述                                                     |
| author       | 包的作者姓名                                                 |
| contributors | 包的其他贡献者姓名                                           |
| dependencies | 依赖包列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下 |
| main         | main 字段指定了程序的主入口文件，require('moduleName') 就会加载这个文件。这个字段的默认值是模块根目录下面的 index.js |
| keywords     | 关键字                                                       |

####  1.3.2 下载及使用

**下载**

（1）命令：`npm install <pakage>` ，或`npm i <pakage>`，全局安装`npm install <pakage> -g`

（2）执行过程：

- 软件包会被存储在 node_modules 文件夹中，如果在应用中不存在此文件夹，npm 会自动创建。
- 软件包会被记录在 package.json 文件中. 包含软件包的名字以及版本号。
- npm 会在应用中创建 package-lock.json 文件, 用于记录软件包及软件包的依赖包的下载地址及
  版本。

**使用**

（1）在引入第三方软件包时，在 require 方法中不需要加入路径信息，只需要使用软件包的名字即可，
require 方法会自动去 node_modules 文件夹中进行查找。

（2）将应用程序提交到版本库之前，将 node_modules 文件夹添加到 .gitignore 文件中

```bash
git init
git status
echo "node_modules/" > .gitignore
git status
git add .
git commit -m "our first commit"
```

**更新npm**

（1）windows

```powershell
npm install npm -g
```

（2）淘宝镜像

```powershell
npm install -g cnpm --registry=https://registry.npmmirror.com
```

**查看安装信息**

（1）查看全局安装的模块

```powershell
npm list -g
```

（2）查看某个模块的版本号

```powershell
npm list grunt
```

#### 1.3.3  语义版本控制

1. 版本号规范
   `Major Version 主要版本`：添加新功能 (破坏现有 API) -> 6.0.0
   `Minor version 次要版本`：添加新功能 (不会破坏现有 API, 在现有 API 的基础上进行添加) ->
   5.13.0
   `Patch version 补丁版本`：用于修复 bug -> 5.12.6

2. 版本号更新规范
   `^5.12.5`: 主要版本不变，更新次要版本和补丁版本
   `~5.12.5`: 主要版本和次要版本不变，更新补丁版本
   `5.12.5`: 使用确切版本，即主要版本，次要版本，补丁版本固定

#### 1.3.4 查看软件包信息

（1） 查看软件包实际版本： `npm list`, `--depth`选项指定查看依赖包的层级

（2）查看软件包元数据

```shell
npm view mongoose
npm view mongoose versions
npm view mongoose dist-tags dependencies
```

#### 1.3.5 管理软件包

（1）下载特定版本的软件包

```shell
npm i <pkg>@<version>
npm i mongoose@2.4.2 lodash@4.7.0
```
```shell
cat package.json
npm list --depth 0
```

（2）删除软件包

```shell
npm uninstall <pkg>
npm uninstall mongoose
npm un mongoose
```

（3）更新软件包

```shell
npm outdated
npm update
```

（4）搜索模块

```shell
npm search express
```

（5）查看当前目录下的模块

```shell
npm list
```

#### 1.3.6 项目依赖 VS 开发依赖

- 项目依赖：无论在开发环境还是线上环境只要程序在运行的过程中需要使用的软件包就是项目依赖。比如 lodash，mongoose
- 开发依赖：在应用开发阶段使用，在生产环境中不需要使用的软件包，比如 TypeScript 中的类型声明文件
- 在 `package.json `文件中, 项目依赖和开发依赖要分别记录，项目依赖被记录在 `dependencies` 对象
  中，开发依赖被记录在 `devDependencies `中，使开发者可以在不同的环境中下载不同的依赖软包
- 在下载开发依赖时，要在命令的后面加上` --save-dev` 选项或者` -D `选项。`npm i eslint -D`
- 在开发坏境中下载所有依赖软件包: `npm install`
- 在生产环境中只下载项目依赖软件包: `npm install --prod`

#### 1.3.7 本地安装与全局安装

1. 本地安装与全局安装
本地安装：将软件包下载到应用根目录下的 node_modules 文件夹中，软件包只能在当前应用中
使用。
全局安装：将软件包下载到操作系统的指定目录中，可以在任何应用中使用。
通过 -g 选项将软件包安装到全局： `npm install <pkg> -g`
查看全局软件包安装位置：` npm root -g`
删除全局中的软件包: `npm un npm-check-updates -g`
查看全局中安装了哪些软件包: `npm list -g --depth 0`
查看全局中有哪些过期软件包: `npm outdated -g`
2. nodemon
问题：在 node 环境中每次修改 JavaScript 文件后都需要重新执行该文件才能看到效果。
通过 nodemon 可以解决此烦恼，它是命令工具软件包，可以监控文件变化，自动重新执行文件。
`npm install nodemon@2.0.7 -g`
`nodemon app.js`
3. `npm-check-updates` 强制更新
`npm-check-updates `可以查看应用中有哪些软件包过期了，可以强制更新 `package.json `文件中
软件包版本
1. 将 `npm-check-updates` 安装到全局： `npm install npm-check-updates -g`
4. 查看过期软件包： `npm-check-updates`
`npm uninstall <pkg>`
`npm uninstall mongoose`
`npm un mongoose`
3. 更新 package.json： `ncu -u`
5. 安装软件包： `npm i`
6. 检测： `npm outdated`或 `npm-check-updates`

#### 1.3.8 更改npm镜像地址

由于 npmjs.com 是国外的网站，大多数时候下载软件包的速度会比较慢，如何解决呢？
可以通过配置的方式更改 npm 工具的下载地址。
1. 获取 npm 配置
    `npm config list -l --json`
    `-l `列表所有默认配置选项
    `--json` 以 json 格式显示配置选项
2. 设置 npm 配置
    获取 npm 下载地址： `npm config get registry`
    获取 npm 用户配置文件: `npm config get userconfig`
3. 更改 npm 镜像地址

```shell
npm config set registry https://registry.npm.taobao.org
npm config set registry https://registry.npmjs.org/
cat .npmrc
```

### 1.4 异步编程

#### 1.4.1 回调函数

在异步编程中，异步 API 执行的结果就是通过回调函数传递参数的方式传递到上层代码中的。

```javascript
const fs = require("fs")
fs.readFile("./index.html", "utf-8", function (error, data) {
	if (error) console.log("发生了错误")
	console.log(data)
})
```

#### 1.4.2 回调地狱

回调地狱是回调函数多层嵌套导致代码难以维护的问题。
基于回调函数的异步编程一不小心就会产生回调地狱的问题。

```js
const fs = require("fs")
fs.readFile("./x.txt", "utf-8", function (error, x) {
	fs.readFile("./y.txt", "utf-8", function (error, y) {
		fs.readFile("./z.txt", "utf-8", function (error, z) {
			console.log(x)
			console.log(y)
			console.log(z)
		})
	})
})
```

```js
const x = fs.readFile('./x.txt', 'utf-8')
const y = fs.readFile('./y.txt', 'utf-8')
const z = fs.readFile('./z.txt', 'utf-8')
console.log(x)
console.log(y)
console.log(z)
```

#### 1.4.3 基于Promise的异步编程

1. Promise 概述
Promise 是 JavaScript 中异步编程解决方案，可以解决回调函数方案中的回调地狱问题。
可以将 Promise 理解为容器，用于包裹异步 API 的容器，当容器中的异步 API 执行完成后，
Promise 允许我们在容器的外面获取异步 API 的执行结果，从而避免回调函数嵌套。
Promise 翻译为承诺，表示它承诺帮我们做一些事情，既然它承若了它就要去做，做就会有一个过
程，就会有一个结果，结果要么是成功要么是失败。
所以在 Promise 中有三种状态, 分别为等待(pending)，成功(fulfilled)，失败(rejected)。
默认状态为等待，等待可以变为成功，等待可以变为失败。
状态一旦更改不可改变，成功不能变回等待，失败不能变回等待，成功不能变成失败，失败不能变
成成功。
2. Promise 基础语法

```js
const fs = require("fs")
const promise = new Promise(function (resolve, reject) {
	fs.readFile("./x.txt", "utf-8", function (error, data) {
		if (error) {
			// 将状态从等待变为失败
			reject(error)
		} else {
			// 将状态从等待变为成功
			resolve(data)
		}
	})
})
promise
.then(function (data) {
	console.log(data)
})
.catch(function (error) {
	console.log(error)
})
```

3. Promise 链式调用

```js
const fs = require('fs')

function readFile(path){
    return new Promise((resolve,reject)=>{
        fs.readFile(path,'utf-8',(error,result)=>{
            if(error){
                reject(error)
            }else{
                resolve(result)
            }

        })

    })
}

// then方法接收正确执行的结果
// catch方法接收错误执行的结果，一旦错误不再执行后面的then
// 无论执行正确与否，均会执行finally,finally的回调函数无参数
readFile('./x.txt')
.then((x)=>{
    console.log(x)
    return readFile('./y.txt')
})
.then((y)=>{
    console.log(y)
    return readFile('./z.txt')
})
.then((z)=>{
    console.log(z)
})
.catch(function (error) {
    console.log(error)
})
.finally((z)=>{
    console.log('end')
})
```

4. Promise.all 并发异步操作

```javascript
const fs = require("fs")
function readFile(path){
    return new Promise((resolve,reject)=>{
        fs.readFile(path,'utf-8',(error,result)=>{
            if(error){
                reject(error)
            }else{
                resolve(result)
            }

        })

    })
}

// all接收一个list作为参数，返回结果也是一个list
Promise.all([
    readFile("./x.txt"),
    readFile("./y.txt"),
    readFile("./z.txt")
]).then(function(data){
    console.log(data)
})
```

#### 1.4.4 基于异步函数的异步编程

1. 异步函数概述

```javascript
getFileContent().then((result)=>{
    console.log(result)
})const fs = require("fs")
function readFile(path){
    return new Promise((resolve,reject)=>{
        fs.readFile(path,'utf-8',(error,result)=>{
            if(error){
                reject(error)
            }else{
                resolve(result)
            }
        })
    })
}
// async 声明异步函数的关键字，异步函数的返回值会被自动填充到 Promise 对象中
// await 关键字后面只能放置返回 Promise 对象的 API
// await 关键字可以暂停函数执行，等待 Promise 执行完后返回执行结果
// await 关键字只能出现在异步函数中
async function getFileContent(){
    let x = await readFile('./x.txt')
    let y = await readFile('./y.txt')
    let z = await readFile('./z.txt')
    return [x,y,z]
}

getFileContent().then((result)=>{
    console.log(result)
})
```

2. util.promisify
在 Node.js 平台下，所有异步方法使用的都是基于回调函数的异步编程。为了使用异步函数提高异
步编程体验，可以使用 util 模块下面的 promisify 方法将基于回调函数的异步 API 转换成返回
Promise 的API。

```javascript
const fs = require("fs")
const util = require('util')
const readFile = util.promisify(fs.readFile)
// 此处readFile还需要传入utf-8
async function getFileContent(){
    let x = await readFile('./x.txt','utf-8')
    let y = await readFile('./y.txt','utf-8')
    let z = await readFile('./z.txt','utf-8')
    return [x,y,z]
}

getFileContent().then((result)=>{
    console.log(result)
})
```

#### 1.4.5 事件循环机制

（1）概述

- 为什么要学习事件循环机制?
  学习事件循环可以让开发者明白 JavaScript 的运行机制是怎么样的。
- 事件循环机制做的是什么事情？
  事件循环机制用于管理异步 API 的回调函数什么时候回到主线程中执行。
  Node.js 采用的是异步 I/O 模型。同步 API 在主线程中执行，异步 API 在底层的 C++ 维护的线程中
  执行，异步 API 的回调函数在主线程中执行。在 JavaScript 应用运行时，众多异步 API 的回调函数
  什么时候能回到主线程中调用呢？这就是事件循环机制做的事情，管理异步 API 的回调函数什么时
  候回到主线程中执行。
- 为什么这种机制叫做事件循环？
  因为 Node.js 是事件驱动的。事件驱动就是当什么时候做什么事情，做的事情就定义在回调函数
  中，可以将异步 API 的回调函数理解为事件处理函数，所以管理异步API回调函数什么时候回到主
  线程中调用的机制叫做事件循环机制。

#### 1.4.6 Event Loop 的六个阶段

1. **Timers**：用于存储定时器的回调函数(setInterval, setTimeout)。
2. **Pending callbacks**：执行与操作系统相关的回调函数，比如启动服务器端应用时监听端口操作的回调函数就在这里调用。
3. **Idle, prepare**：系统内部使用。
4. **IO Poll**：存储 I/O 操作的回调函数队列，比如文件读写操作的回调函数。
    如果事件队列中有回调函数，执行它们直到清空队列。
    否则事件循环将在此阶段停留一段时间以等待新的回调函数进入，这个等待取决于以下两个条件：

	- setImmediate 队列(check 阶段)中存在要执行的回调函数.
	- timers 队列中存在要执行的回调函数. 在这种情况下, 事件循环将移至 check 阶段, 然后移至Closing callbacks 阶段, 并最终从 timers 阶段进入下一次循环。
5. **Check**：存储 setImmediate API 的回调函数。
6. **Closing callbacks**：执行与关闭事件相关的回调，例如关闭数据库连接的回调函数等。
    循环体会不断运行以检测是否存在没有调用的回调函数，事件循环机制会按照先进先出的方式执行他们
    直到队列为空。

#### 1.4.7 微任务与宏任务的区别

1. 微任务的回调函数被放置在微任务队列中，宏任务的回调函数被放置在宏任务队列中。

2. 微任务优先级高于宏任务。

- 当微任务事件队列中存在可以执行的回调函数时，事件循环在执行完当前阶段的回调函数后会暂停进入事件循环的下一个阶段，事件循环会立即进入微任务的事件队列中开始执行回调函数，当微任务队列中的回调函数执行完成后，事件循环再进入到下一个阶段开始执行回调函数。

- nextTick 的优先级高于 microTask，在执行任务时，只有 nextTick 中的所有回调函数执行完成后才会开始执行 microTask。
- 不同阶段的宏任务的回调函数被放置在了不同的宏任务队列中，宏任务与宏任务之间没有优先级的概念，他们的执行顺序是按照事件循环的阶段顺序进行的。

#### 1.4.8 Event Loop 代码解析

​	在 Node 应用程序启动后，并不会立即进入事件循环，而是先执行输入代码，从上到下开始执行，同步
API 立即执行，异步 API 交给 C++ 维护的线程执行，异步 API 的回调函数被注册到对应的事件队列中。
当所有输入代码执行完成后，开始进入事件循环。

- process.nextTick()：此方法的回调函数优先级最高，会在事件循环之前被调用。
- setImmediate()：setImmediate 表示立即执行，它是宏任务，回调函数会被会放置在事件循环的 check 阶段。

```javascript
console.log("start")

setTimeout(() => {
  console.log("setTimeout 1")
}, 0)

setTimeout(() => {
  console.log("setTimeout 2")
}, 0)

console.log("end")
// start end 1 2

setTimeout(() => console.log("1"), 0)
setImmediate(() => console.log("2"))

function sleep(delay) {
  var start = new Date().getTime()
  while (new Date().getTime() - start < delay) {
    continue
  }
}
sleep(1000)
// 1 2

setTimeout(() => console.log("1"), 0)
setImmediate(() => console.log("2"))
//  2 1 或 1 2

// const fs = require("fs")

fs.readFile("./index.html", () => {
  setTimeout(() => console.log("1"), 0)
  setImmediate(() => console.log("2"))
})
// 2 1

setTimeout(() => console.log("1"), 50)
process.nextTick(() => console.log("2"))
setImmediate(() => console.log("3"))
process.nextTick(() => console.log("4"))
// 2 4 3 1

setTimeout(() => console.log(1))
setImmediate(() => console.log(2))
process.nextTick(() => console.log(3))
Promise.resolve().then(() => console.log(4))
;(() => console.log(5))()
// 5 3 4 1 2
process.nextTick(() => console.log(1))
Promise.resolve().then(() => console.log(2))
process.nextTick(() => console.log(3))
Promise.resolve().then(() => console.log(4))
// 1 3 2 4

setTimeout(() => console.log("1"), 50)
process.nextTick(() => console.log("2"))
setImmediate(() => console.log("3"))
process.nextTick(() =>
  setTimeout(() => {
    console.log("4")
  }, 1000)
// )
// 2 3 1 4
```



## Express

**创建服务器**

```javascript
// 首先在node_modules文件夹中下载好依赖
// 引入express
const express = require('express')
// 创建服务器
const app = express()
// 监听端口，回调函数可以省略
const port = 8080
app.listen(port,()=>{
    console.log(`成功启动服务器,端口${port}`)
})

// 托管静态资源目录
app.use(express.static('./public'))

// 使用中间件
app.use(express.urlencoded({
    extended : false
}))

// 引入自定义路由模块
const userRouter = require('./routes/user')
// 配置路由前缀
app.use('/v2/user',userRouter)

// 在所有中间件的最后，添加错误处理中间件
app.use((err,req,res,next)=>{
    console.log(err)
    res.send({code:501,msg:'服务器端错误'})
})
```

**创建连接池模块**

```javascript
// 引入第三方模块
const mysql = require('mysql')
// 创建数据库连接池
const pool = mysql.createPool({
    host : '127.0.0.1',
    port : 3306,
    user : 'root',
    password : '',
    database : 'xz',
    // connectionLimit:15
})
// 导出模块
module.exports = pool
```

**创建路由模块**

```javascript
// 引入模块
const express = require('express')
const pool = require('../pool')
// 创建路由
const router = express.Router()

// 查：检索用户是否存在
router.get('/check_uname',(req,res,next)=>{
    pool.query('select * from xz_user where uname=?',[req.query.uname],(err,result)=>{
        if(err){
            next()
            return
        }
        if(result.length === 0){
            res.send('exists')
        }else{
            res.send('exists')
        }

    })
})
// 删：删除用户
router.delete('/delete/:uid',(req,res,next)=>{
    // 此处是根据uid删除，必须要有传参才能实现删除功能
    pool.query('delete from xz_user where uid=?',[req.params.uid],(err,r)=>{
        if(err){
            next(err)
            return
        }
        if(r.affectedRows === 0){
            res.send({code:501,msg:'删除失败'})
        }else{
            res.send({code:200,msg:'删除成功'})
        }
    })
})
// 增：用户注册
router.post('/register',(req,res,next)=>{
/*     // 验证用户输入的信息
    // 验证用户名是否合法,字母开头，允许5-16字节，允许字母数字下划线
    const unameRegexp = /^[a-zA-Z][a-zA-Z0-9_]{4,15}$/
    if(!unameRegexp.test(req.body.uname)){
        res.send({code:401,msg:'用户名无效'})
        return
    }
    // 验证密码是否合法,以字母开头，长度在6~18之间，只能包含字母、数字和下划线
    const upwdRegexp = /^[a-zA-Z]\w{5,17}$/
    if(!upwdRegexp.test(req.body.upwd)){
        res.send({code:402,msg:'密码无效'})
        return
    }
    // 验证邮箱是否合法
    const emailRegexp = /^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/
    if(!emailRegexp.test(req.body.email)){
        res.send({code:403,msg:'邮箱无效'})
        return
    }
    // 验证电话是否合法
    const phoneRegexp = /1[3-9]\d{9}/
    if(!phoneRegexp.test(req.body.phone)){
        res.send({code:404,msg:'电话无效'})
        return
    }

    // 设置默认头像
    req.body.avatar = 'img/avatar/default.png' */

    pool.query('insert into xz_user set ?',[req.body],(err,r)=>{
        if(err){
            next(err)
            return
        }
        res.send({code:200,msg:'注册成功'})
    })
})
// 改：修改用户
router.put('/update',(req,res,next)=>{
/*     // 验证用户输入的信息
    // 验证用户名是否合法,字母开头，允许5-16字节，允许字母数字下划线
    const unameRegexp = /^[a-zA-Z][a-zA-Z0-9_]{4,15}$/
    if(!unameRegexp.test(req.body.uname)){
        res.send({code:401,msg:'用户名无效'})
        return
    }
    // 验证密码是否合法,以字母开头，长度在6~18之间，只能包含字母、数字和下划线
    const upwdRegexp = /^[a-zA-Z]\w{5,17}$/
    if(!upwdRegexp.test(req.body.upwd)){
        res.send({code:402,msg:'密码无效'})
        return
    }
    // 验证邮箱是否合法
    const emailRegexp = /^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/
    if(!emailRegexp.test(req.body.email)){
        res.send({code:403,msg:'邮箱无效'})
        return
    }
    // 验证电话是否合法
    const phoneRegexp = /1[3-9]\d{9}/
    if(!phoneRegexp.test(req.body.phone)){
        res.send({code:404,msg:'电话无效'})
        return
    } */
    
    pool.query('update xz_user set ? where uid=?',[req.body,req.body.uid],(err,r)=>{
        if(err){
            next(err)
            return
        }
        if(r.affectedRows !== 0){
            res.send({code:200,msg:'update success'})
        }else{
            res.send({code:501,msg:'update err'})
        }
    })

// 导出模块
module.exports = router
})
```