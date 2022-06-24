# JSCORE

## 声明提升

- JS代码在运行时, 需要先`声明提升`:  把 `var/let/const/function/class` 声明的变量提升到作用域的顶部, 然后再执行提升后的代码
- 注意事项
  - 函数提升: 整体提升 -- 函数体+函数名
  - 函数表达式中的函数不提升:`var 变量 = function (){}`
    - 假如提升: `var 变量 = `    值被提走了, 表达式语法错误
  - var: 只提升 var 的部分, 不提升 = 赋值



## 拷贝对象

### 浅拷贝

```js
// 拷贝: 复制  copy
// 希望复制对象类型 而非 单纯的引用

var emp1 = { ename: "nan", age: 19, skill: ['run','jump'] }

function simpleCopy(target) {
    //1. 创建一个空的
    var obj = {}

    //2. 把要复制的对象中的属性 遍历后 存储到空对象里
    for (var key in target) {
        obj[key] = target[key]
    }

    //3. 返回复制出来的对象
    return obj
}
```

### 深拷贝

```js
//1.利用json转字符串再转回对象
var emp1 = { ename: "nan", age: 19, skill: ['run','jump'] }
var e = JSON.stringify(emp1)
var emp2 = JSON.parse(e)

//2.利用递归实现
function deepCopy(target) {
    // 判断是否为对象
    if (typeof target != 'object') {
        return target
    }
    // 判断是否为数组
    if (Array.isArray(target)) {
        var obj = []
    } else {
        var obj = {}
    }
    // 判断值类型
    for (const key in target) {
        const value = target[key]
        if (typeof value == 'object') {
            // 若值为对象，则继续深拷贝
            obj[key] = deepCopy(value)
        } else {
            // 若值为基础数据类型，直接赋值
            obj[key] = value
        }
    }

    return obj

}

var emp2 = deepCopy(emp1)
```



## 闭包

### 初级应用

- 闭包指能够引用其他函数作用域中变量的函数
- 闭包能够存储上级函数作用域，防止使用的来自其他作用域的变量被销毁
- ES6之前，只有两种作用域：全局，局部（函数），闭包是解决全局变量污染唯一的方式

```js
//匿名函数自调用，就是为了快速生成一个函数作用域
//匿名函数中返回一个函数，其scopes中，存储上级匿名函数作用域
var fn = (function(){
	var a = 1
    return function(){
        //...使用变量a
    }
})
```

### 循环

- ES6之前，只能用闭包的方式，让变量i变为fn函数私有
- ES6之后可以用块级作用域，将var改为let

```js
var fns = []
//此处循环中var的i是全局变量
for (var i = 0; i < 10; i++) {
    var fn = function () {
        console.log(i) //打印的i，是window中全局的i
    }
    fns.push(fn)
}
for (const fn of fns) {
    fn()
}
```

```js
var fns = []
for (var i = 0; i < 10; i++) {
    //闭包的外层习惯上使用匿名函数自调用
    var fn = (function (x) { //x是匿名函数的形参
        return function () {
            console.log(x)
        }
    })(i) //i是匿名函数的实参
    fns.push(fn)
}
for (const fn of fns) {
    fn()
}
```

### 柯里化

- 柯里化（Currying）是把接受多个参数的函数变换成接受一个单一参数(最初函数的第一个参数)的函数，并且返回接受余下的参数且返回结果的新函数的技术。

```js
function add(a, b) {
    return a + b
}
add(10, 20) //30

// 柯里化语法：多参数 -> 单参数
function ke_add(a) {
    return function (b) {
        return a + b
    }
}
ke_add(10)(20) //30
```

- 柯里化作用：生成函数，并且设定私有属性
- 缺点：持续占据内存，直到函数本身被销毁--浪费内存
- 优点：只要开辟一次内存空间即可--节省CPU性能

```js
function createRegExp(regexp) {
    return function (str) {
        return regexp.test(str)
    }
}

const isNumber = createRegExp(/^\d+$/)
isNumber(121313131)
```



## 修改函数this指向

### apply

```js
//apply(obj,args)指定函数作用域
function show(a, b) {
    console.log('this:', this)
    console.log(this.c + a + b)
}
var emp1 = { name: 'emp1', c: 10, show }
emp1.show(20, 30)

//仿写apply()
Function.prototype.myApply = function (obj, args) {
    //Symbol()作为属性名，避免覆盖已有属性
    const uk = Symbol()
    //给obj临时增加一个uk属性，并赋值为show
    //show.myApply(...),此处this指的是show
    obj[uk] = this
    //...将数组展开
    obj[uk](...args)
    delete obj[uk]
}
show.myApply(emp1, [20, 30])
```

### call

```js
//apply(obj,arg1,arg2...)指定函数作用域
function show(a, b) {
    console.log('this:', this)
    console.log(this.c + a + b)
}
var emp1 = { name: 'emp1', c: 10, show }
emp1.show(20, 30)

//仿写call()
//...args将参数收集到数组
Function.prototype.myCall = function (obj, ...args) {
    //Symbol()作为属性名，避免覆盖已有属性
    const uk = Symbol()
    //给obj临时增加一个uk属性，并赋值为show
    //show.myCall(...),此处this指的是show
    obj[uk] = this
    //...将数组展开
    obj[uk](...args)
    delete obj[uk]
}
show.myCall(emp1, 20, 30)
```

### bind

```js
//bind(obj,arg1,arg2...)方法会创建一个新的函数实例，其this 值会被绑定到传给bind()的对象
function show(a, b) {
    console.log('this:', this)
    console.log(this.c + a + b)
}
var emp1 = { name: 'emp1', c: 10, show }
emp1.show(20, 30)

//仿写bind()
//...args将参数收集到数组
Function.prototype.myBind = function (obj, ...args) {
    //this指向show,将this保存到that中，以供newFn使用
    var that = this
    var newFn = function () {
        //本质上触发newFn,是触发show
        const uk = Symbol()
        obj[uk] = that
        obj[uk](...args)
        delete obj[uk]
    }
    return newFn
}

var b_show = show.myBind(emp1, 20, 30)
b_show()
```

## 防抖与节流

### 防抖

```html
<body>
    <input type="text" id="search">

    <script>
        //防抖动是将多次执行变为最后一次执行
        const search = document.getElementById('search')

        function debounce(delay) {
            //闭包，也可以用块级作用域防止s全局污染
            var s

            return function () {
                // console.log('search => ', this.value)

                // 存储定时器，当每次输入操作时，立即删除当前定时器，防止多次触发
                clearTimeout(s)
                s = setTimeout(() => {
                    console.log('search => ', this.value)
                }, delay);
            }

        }

        search.oninput = debounce(1000)
    </script>
</body>
```

### 节流

```html
<body>
    <button id="reg">提交注册</button>

    <script>
        //节流是将多次执行变成每隔一段时间执行
        //减小监听事件的时间灵敏度，降低频率，节省资源
        const reg = document.getElementById('reg')

        function throttle(delay) {
            var lock = false
            return function () {
                if (lock) return
                console.log('开始注册')
                lock = true
                setTimeout(() => {
                    lock = false
                }, delay)
            }

        }

        reg.onclick = throttle(5000)

    </script>
</body>
```



## 函数

### 构造函数

> 构造函数：按照一定的规则生成对象类型，会自动为传入的数据装配上prototype属性



## ES6

### 块级作用域

### ？.语法

```js
const heros = document.querySelectorAll('#heros>img');
const bigHero = document.querySelector('#big');
const heroName = document.querySelector('#heroName');
heros.forEach(hero => hero.onclick = function () {
    const imgName = this.dataset.name
    big.src = `./heros/${imgName}.jfif`

    const active = document.querySelector('.active')
    //if
    if (active) { active.classList.remove('active') }
    //逻辑短路 值1 && 值2  值1为真才执行值2
    // active && active.classList.remove('active');

    //ES6  对象?.属性名 对象有值才执行后续
    // active?.classList.remove('active')

    this.classList.toggle('active')
    heroName.innerHTML = imgName
    console.log(this.dataset)
})
```

