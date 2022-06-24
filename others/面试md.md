### 20220513

#### 1.post和get的区别

#### 2.var,let,const作用域

（1）var是ES5提出的，let和const是ES6提出的。

（2）const声明的是常量，必须赋值

​		1）一旦声明必须赋值

​		2）声明后不能再修改

​		3）如果声明的是引用类型数据，可以修改其属性

（3）let和var声明的是变量，声明之后可以更改，声明时可以不赋值

（4）var允许重复声明变量，后一个变量会覆盖前一个变量。let和const在同一作用域不允许重复声明变量，会报错。

（5）var声明的变量存在变量提升（将变量提升到当前作用域的顶部）。即变量可以在声明之前调用，值为undefined。

（6）let和const不存在变量提升。即它们所声明的变量一定要在声明后使用，否则报ReferenceError错。

（7）var不存在块级作用域。let和const存在块级作用域。

（8）ES5中作用域有：全局作用域、函数作用域。没有块作用域的概念。

（9）ES6(简称ES6)中新增了块级作用域。块作用域由 { } 包括，if语句和for语句里面的{ }也属于块作用域。

#### 3. http状态码

| code | msg                                                          |
| ---- | ------------------------------------------------------------ |
| 200  | 请求成功                                                     |
| 301  | 资源（网页等）被永久转移到其它URL                            |
| 302  | 资源（网页等）临时转移到其它URL                              |
| 304  | 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源 |
| 404  | 请求的资源（网页等）不存在                                   |
| 500  | 内部服务器错误                                               |

#### 4.js练习

##### 4.1 递归函数

```js
//斐波那契数列
function fib(n){
    // 边界条件
    if(n==1 || n==2){
        return 1
    }
    // 规律
    return fib(n-1)+fib(n-2)
}
console.log(fib(7))
```

##### 4.2. 找出字符串中出现最多的字符及出现次数

```js
//同级字符串中出现最多的字符
let str = 'javascrippt'
// 如何统计每一个字符出现的次数
// 准备一个空对象，记录每个字符出现的次数
let obj = {}
let max = 1
for(let i = 0; i < str.length; i++){
    let char = str[i]
    if(obj[char] === undefined){
        obj[char] = 1
    }else{
        obj[char] += 1
        if(obj[char]>max){
            max = obj[char]
        }
    }
}
let max_str = ''
for(let k in obj){
    // k是obj的属性名
    if(obj[k] === max){
        max_str = max_str + k + ' '
    }
}
console.log(`最大次数为${max},字符为${max_str}`)
```

##### 4.3 定时器

```js
// 定时器
for(var i=0;i<3;i++){
    setTimeout(() => {
            console.log(i)
    }, 0);
    console.log(i)
}
//var变量为全局变量，变量i是同一个i,setTimeout的回调函数被启动时，会到全局作用域去找i的值
// 打印结果：012333

for(let i=0;i<3;i++){
    setTimeout(() => {
            console.log(i)
    }, 0);
    console.log(i)
}
//let为块级作用域，变量i不是同一个i,setTimeout的回调函数被启动时，会到块级作用域去找i的值
// 打印结果：012012
```

##### 4.4 翻转字符串

```js
let str = 'hello'
function reverse(str){
    return str.split('').reverse().join('')
}
console.log(reverse(str))
```

##### 4.5 冒泡排序

```js
let num = [13, 6, 2262, 63, 95, 274]

for (let i = 0; i < num.length; i++) {
    for (let j = i; j < num.length; j++) {
        let temp
        if (num[j] > num[j + 1]) {
            temp = num[j + 1]
            num[j + 1] = num[j]
            num[j] = temp
        }
    }
}

console.log(num)
```

##### 4.6 作用域

```js
var uname = 'jack'
function change() {   作用域链
    //var声明提升
    alert(uname)  // undefined
    var uname = 'lily'
    alert(uname)  //?
}
change()

//undefined lily
```

##### 4.7 短路表达式

```js
foo = foo || bar

//常用于函数参数的空判断
//相当于下列代码
var foo;
if(foo){
    foo=foo;
}else{
    foo=bar;
}
```



#### 5 常用git命令

**本地仓库**

```bash
# 初始化仓库
$ git init

#提交文件至暂存区
$ git add [file]

#提交所有文件至暂存区
$ git add .

#提交版本
$ git commit -m "版本描述"

#分支
$ git branch

#合并
$ git merge
```

**远程仓库**

```bash
#克隆
$ git clone <url>

#更新（从远程仓库更新到本地）
$ git pull

#上传
$ git push
```

#### 6 express传参方式

| 传参方式   |                |             |
| ---------- | -------------- | ----------- |
| 查询字符串 | /detail?lid=2  | `req.query` |
| 路由传参   | /detail/5      | req.pramas  |
| post传参   | 结合内置中间件 | req.body    |

#### 7 null和undefined的区别

（1）null表示没有对象

​			1） 作为函数的参数，表示该函数的参数不是对象

​			2） 作为对象原型链的终点

 （2）undefined表示缺少值

​			1）定义了形参，没有传实参，显示undefined

​			2）对象属性名不存在时，显示undefined

​			3）函数没有写返回值，即没有写return，拿到的是undefined

​			4）写了return，但没有赋值，拿到的是undefined

 （3）null和undefined转换成number数据类型

​			1）null 默认转成 0

​			2）undefined 默认转成 NaN

 （4）在 if 语句中 null 和 undefined 都会转为false，两者用相等运算符比较也是相等`null==undefined //true`

#### 8 数据库中的多表查询

（1）INNER JOIN：如果表中有至少一个匹配，则返回行

（2）LEFT JOIN：从左表返回所有的行，如果右表中没有匹配，对应的列返回Null

（3）RIGHT JOIN：从右表返回所有的行 ，如果左表中没有匹配，对应的列返回Null

（4）FULL JOIN：只要其中一个表中存在匹配，则返回行（即结合左连接和右连接的结果）

（5）MySQL不支持FULL JOIN，但是可以用 LEFT JOIN **UNION** RIGHT join代替

#### 9 fs模块

- fs模块是Node.js的一个核心模块,专门用来操作系统中的文件,常用的操作方式是对文件的读取和写入
- 使用require('fs')载入fs模块，模块中所有方法都有同步和异步两种形式。
- 异步是通过回调函数获取结果，同步是通过方法的返回值获取结果。

#### 10 数组

**常用属性**

| 属性     | 描述                     |
| -------- | ------------------------ |
| `length` | 设置或返回数组元素的个数 |

**常用方法**

| 方法         | 描述                                                 |
| ------------ | ---------------------------------------------------- |
| `concat()`   | 连接两个或更多的数组，并返回结果。                   |
| `includes()` | 判断一个数组是否包含一个指定的值。                   |
| `indexOf()`  | 搜索数组中的元素，并返回它所在的位置。               |
| `isArray()`  | 判断对象是否为数组。                                 |
| `join()`     | 把数组的所有元素放入一个字符串。                     |
| `map()`      | 通过指定函数处理数组的每个元素，并返回处理后的数组。 |
| `pop()`      | 删除数组的最后一个元素并返回删除的元素。             |
| `push()`     | 向数组的末尾添加一个或更多元素，并返回新的长度。     |
| `reverse()`  | 反转数组的元素顺序。                                 |
| `shift()`    | 删除并返回数组的第一个元素。                         |
| `slice()`    | 选取数组的一部分，并返回一个新数组。                 |
| `sort()`     | 对数组的元素进行排序。                               |
| `splice()`   | 从数组中添加或删除元素。                             |
| `toString()` | 把数组转换为字符串，并返回结果。                     |
| `unshift()`  | 向数组的开头添加一个或更多元素，并返回新的长度。     |
| ...          |                                                      |

