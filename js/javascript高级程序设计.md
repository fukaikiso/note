# JavaScript



## 1 基础语法

### 1.1 数据类型

#### 1.1.1 undefined

（1）默认情况下，任何未经初始化的变量都会取得undefined值

```js
let msg
console.log(msg) //"undefined"
```

（2）对于未声明的变量，调用typeOf时，其返回值仍为undefined，因此为了区分变量是未声明还是声明了未初始化，建议在所有变量声明的同时进行初始化

```js
// 这个变量被声明了，只是值为undefined
let message; 
// 确保没有声明过这个变量
// let age
console.log(typeof message); // "undefined"
console.log(typeof age); // "undefined"
```

#### 1.1.2 Null

（1）null 值表示一个空对象指针

````JS
let car = null;
console.log(typeof car); // "object"
````

（2）undefined是由null派生而来，因此表面上相等

```JS
console.log(null == undefined); // true
```

#### 1.1.3 Boolean

（1） 布尔值有两个字面量值：true,false

（2）流程控制语句会自动执行其他类型值到布尔值，转为false的有：`false`, `""`, `0`, `NaN`, `null`, `undefined`

#### 1.1.4 Number

（1）整数

```js
//使用八进制和十六进制格式创建的数值在所有数学操作中都被视为十进制数值
let intNum = 55; // 整数,默认十进制
let octalNum1 = 070; // 八进制的56，严格模式下八进制无效
let hexNum1 = 0xA; // 十六进制10
```

（2）浮点数

```js
//存在舍入错误
//之所以存在这种舍入错误，是因为使用了IEEE 754 数值，这种错误并非ECMAScript所独有。其他使用相同格式的语言也有这个问题。
console.log(0.1+0.2) //0.30000000000000004
```

（3）NaN

```js
//表示not a number
console.log(0/0); // NaN
console.log(-0/+0); // NaN
console.log(5/0); // Infinity
console.log(5/-0); // -Infinity

//涉及NaN的操作始终返回NaN，NaN不等于NaN
console.log(NaN == NaN); // false

//判断是否为NaN使用函数isNaN
console.log(isNaN(NaN)); // true
console.log(isNaN("blue")); // true，不可以转换为数值
console.log(isNaN(10)); // false，10 是数值
console.log(isNaN("10")); // false，可以转换为数值10
console.log(isNaN(true)); // false，可以转换为数值1
```

（4）数值转换

```js
//Number()
//布尔值，true 转换为1，false 转换为0。
//null，返回0
//undefined，返回NaN
let num1 = Number("Hello world!"); // NaN
let num2 = Number(""); // 0
let num3 = Number("000011"); // 11
let num4 = Number(true); // 1

//parseInt()
let num1 = parseInt("1234blue"); // 1234
let num2 = parseInt(""); // NaN
let num3 = parseInt("0xA"); // 10，解释为十六进制整数
let num4 = parseInt(22.5); // 22
let num5 = parseInt("70"); // 70，解释为十进制值
let num6 = parseInt("0xf"); // 15，解释为十六进制整数
//所以为避免解析出错，建议始终传给它第二个参数
let num1 = parseInt("10", 2); // 2，按二进制解析
let num2 = parseInt("10", 8); // 8，按八进制解析
let num3 = parseInt("10", 10); // 10，按十进制解析
let num4 = parseInt("10", 16); // 16，按十六进制解析

//parseFloat()与parseInt()规则基本一致
//但parseFloat()只解析十进制的值，0开头的忽略0，0x开头的解析为0
let num1 = parseFloat("1234blue"); // 1234，按整数解析
let num2 = parseFloat("0xA"); // 0
let num3 = parseFloat("22.5"); // 22.5
let num4 = parseFloat("22.34.5"); // 22.34
let num5 = parseFloat("0908.5"); // 908.5
let num6 = parseFloat("3.125e7"); // 31250000
```

#### 1.1.5 String

（1）字符串一旦创建，不可改变。只能通过销毁原始字符串，给变量赋予新值

（2）转换为字符串

```js
let value1 = 10;
let value2 = true;
let value3 = null;
let value4;
console.log(String(value1)); // "10"
console.log(String(value2)); // "true"
console.log(String(value3)); // "null"
console.log(String(value4)); // "undefined"

//对于数字，toString可以接收一个底数作为参数
let num = 10;
console.log(num.toString()); // "10"
console.log(num.toString(2)); // "1010"
console.log(num.toString(8)); // "12"
```

（3）模板字符串

```js
//模板字符串可以跨行定义字符，且支持字符串插值
console.log(`Hello, ${ `World` }!`); // Hello, World!

//标签函数
let a = 6;
let b = 9;
//...表示剩余操作符，将不确定个数的参数收集到一个数组中
function simpleTag(strings, ...expressions) {
console.log(strings);
for(const expression of expressions) {
console.log(expression);
}
return 'foobar';
}
let taggedResult = simpleTag`${ a } + ${ b } = ${ a + b }`;
// ["", " + ", " = ", ""]
// 6
// 9
// 15
console.log(taggedResult); // "foobar"

//原始字符串
// Unicode 示例
// \u00A9 是版权符号
console.log(`\u00A9`); // ©
console.log(String.raw`\u00A9`); // \u00A9
```

**String 对象属性**

| 属性                                                         | 描述                       |
| :----------------------------------------------------------- | :------------------------- |
| [constructor](https://www.runoob.com/jsref/jsref-constructor-string.html) | 对创建该对象的函数的引用   |
| [length](https://www.runoob.com/jsref/jsref-length-string.html) | 字符串的长度               |
| [prototype](https://www.runoob.com/jsref/jsref-prototype-string.html) | 允许您向对象添加属性和方法 |

**String 对象方法**

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [charAt()](https://www.runoob.com/jsref/jsref-charat.html)   | 返回在指定位置的字符。                                       |
| [charCodeAt()](https://www.runoob.com/jsref/jsref-charcodeat.html) | 返回在指定的位置的字符的 Unicode 编码。                      |
| [concat()](https://www.runoob.com/jsref/jsref-concat-string.html) | 连接两个或更多字符串，并返回新的字符串。                     |
| [endsWith()](https://www.runoob.com/jsref/jsref-endswith.html) | 判断当前字符串是否是以指定的子字符串结尾的（区分大小写）。   |
| [fromCharCode()](https://www.runoob.com/jsref/jsref-fromcharcode.html) | 将 Unicode 编码转为字符。                                    |
| [indexOf()](https://www.runoob.com/jsref/jsref-indexof.html) | 返回某个指定的字符串值在字符串中首次出现的位置。             |
| [includes()](https://www.runoob.com/jsref/jsref-string-includes.html) | 查找字符串中是否包含指定的子字符串。                         |
| [lastIndexOf()](https://www.runoob.com/jsref/jsref-lastindexof.html) | 从后向前搜索字符串，并从起始位置（0）开始计算返回字符串最后出现的位置。 |
| [match()](https://www.runoob.com/jsref/jsref-match.html)     | 查找找到一个或多个正则表达式的匹配。                         |
| [repeat()](https://www.runoob.com/jsref/jsref-repeat.html)   | 复制字符串指定次数，并将它们连接在一起返回。                 |
| [replace()](https://www.runoob.com/jsref/jsref-replace.html) | 在字符串中查找匹配的子串，并替换与正则表达式匹配的子串。     |
| [replaceAll()](https://www.runoob.com/jsref/jsref-replaceall.html) | 在字符串中查找匹配的子串，并替换与正则表达式匹配的所有子串。 |
| [search()](https://www.runoob.com/jsref/jsref-search.html)   | 查找与正则表达式相匹配的值。                                 |
| [slice()](https://www.runoob.com/jsref/jsref-slice-string.html) | 提取字符串的片断，并在新的字符串中返回被提取的部分。         |
| [split()](https://www.runoob.com/jsref/jsref-split.html)     | 把字符串分割为字符串数组。                                   |
| [startsWith()](https://www.runoob.com/jsref/jsref-startswith.html) | 查看字符串是否以指定的子字符串开头。                         |
| [substr()](https://www.runoob.com/jsref/jsref-substr.html)   | 从起始索引号提取字符串中指定数目的字符。                     |
| [substring()](https://www.runoob.com/jsref/jsref-substring.html) | 提取字符串中两个指定的索引号之间的字符。                     |
| [toLowerCase()](https://www.runoob.com/jsref/jsref-tolowercase.html) | 把字符串转换为小写。                                         |
| [toUpperCase()](https://www.runoob.com/jsref/jsref-touppercase.html) | 把字符串转换为大写。                                         |
| [trim()](https://www.runoob.com/jsref/jsref-trim.html)       | 去除字符串两边的空白。                                       |
| [toLocaleLowerCase()](https://www.runoob.com/jsref/jsref-tolocalelowercase.html) | 根据本地主机的语言环境把字符串转换为小写。                   |
| [toLocaleUpperCase()](https://www.runoob.com/jsref/jsref-tolocaleuppercase.html) | 根据本地主机的语言环境把字符串转换为大写。                   |
| [valueOf()](https://www.runoob.com/jsref/jsref-valueof-string.html) | 返回某个字符串对象的原始值。                                 |
| [toString()](https://www.runoob.com/jsref/jsref-tostring.html) | 返回一个字符串。                                             |

**String HTML 包装方法**

HTML 返回包含在相对应的 HTML 标签中的内容。

以下方法并非标准方法，所以可能在某些浏览器下不支持。

| 方法                                                         | 描述                         |
| :----------------------------------------------------------- | :--------------------------- |
| [anchor()](https://www.runoob.com/jsref/jsref-anchor.html)   | 创建 HTML 锚。               |
| [big()](https://www.runoob.com/jsref/jsref-big.html)         | 用大号字体显示字符串。       |
| [blink()](https://www.runoob.com/jsref/jsref-blink.html)     | 显示闪动字符串。             |
| [bold()](https://www.runoob.com/jsref/jsref-bold.html)       | 使用粗体显示字符串。         |
| [fixed()](https://www.runoob.com/jsref/jsref-fixed.html)     | 以打字机文本显示字符串。     |
| [fontcolor()](https://www.runoob.com/jsref/jsref-fontcolor.html) | 使用指定的颜色来显示字符串。 |
| [fontsize()](https://www.runoob.com/jsref/jsref-fontsize.html) | 使用指定的尺寸来显示字符串。 |
| [italics()](https://www.runoob.com/jsref/jsref-italics.html) | 使用斜体显示字符串。         |
| [link()](https://www.runoob.com/jsref/jsref-link.html)       | 将字符串显示为链接。         |
| [small()](https://www.runoob.com/jsref/jsref-small.html)     | 使用小字号来显示字符串。     |
| [strike()](https://www.runoob.com/jsref/jsref-strike.html)   | 用于显示加删除线的字符串。   |
| [sub()](https://www.runoob.com/jsref/jsref-sub.html)         | 把字符串显示为下标。         |
| [sup()](https://www.runoob.com/jsref/jsref-sup.html)         | 把字符串显示为上标。         |

#### 1.1.6 Symbol【ES6】

（1）基本用法

```js
//符号就是用来创建唯一记号
//调用Symbol()函数时，也可以传入一个字符串参数作为对符号的描述（description），将来可以通过这个字符串来调试代码。但是，这个字符串参数与符号定义或标识完全无关
let genericSymbol = Symbol();
let otherGenericSymbol = Symbol();
let fooSymbol = Symbol('foo');
let otherFooSymbol = Symbol('foo');
console.log(genericSymbol == otherGenericSymbol); // false
console.log(fooSymbol == otherFooSymbol); // false

//符号没有字面量语法
//按照规范，你只要创建Symbol()实例并将其用作对象的新属性，就可以保证它不会覆盖已有的对象属性，无论是符号属性还是字符串属性
let genericSymbol = Symbol();
console.log(genericSymbol); // Symbol()
let fooSymbol = Symbol('foo');
console.log(fooSymbol); // Symbol(foo);

//Symbol()函数不能与new 关键字一起作为构造函数使用,这样做是为了避免创建符号包装对象
let myBoolean = new Boolean();
console.log(typeof myBoolean); // "object"
let myString = new String();
console.log(typeof myString); // "object"
let myNumber = new Number();
console.log(typeof myNumber); // "object"
let mySymbol = new Symbol(); // TypeError: Symbol is not a constructor

//如果你确实想使用符号包装对象，可以借用Object()函数
let mySymbol = Symbol();
let myWrappedSymbol = Object(mySymbol);
console.log(typeof myWrappedSymbol); // "object"
```

（2）使用全局符号注册表

```js
//如果运行时的不同部分需要共享和重用符号实例，那么可以用一个字符串作为键，在全局符号注册表中创建并重用符号
//Symbol.for()
let fooGlobalSymbol = Symbol.for('foo'); // 创建新符号
let otherFooGlobalSymbol = Symbol.for('foo'); // 重用已有符号
console.log(fooGlobalSymbol === otherFooGlobalSymbol); // true

//即使采用相同的符号描述，在全局注册表中定义的符号跟使用Symbol()定义的符号也并不等同
let localSymbol = Symbol('foo');
let globalSymbol = Symbol.for('foo');
console.log(localSymbol === globalSymbol); // false

//还可以使用Symbol.keyFor()来查询全局注册表，这个方法接收符号，返回该全局符号对应的字符串键。如果查询的不是全局符号，则返回undefined。
// 创建全局符号
let s = Symbol.for('foo');
console.log(Symbol.keyFor(s)); // foo
// 创建普通符号
let s2 = Symbol('bar');
console.log(Symbol.keyFor(s2)); // undefined
//如果传给Symbol.keyFor()的不是符号，则该方法抛出TypeError：
Symbol.keyFor(123); // TypeError: 123 is not a symbol
```

（3）使用符号作为属性

​		凡是可以使用字符串或数值作为属性的地方，都可以使用符号

（4）常用内置符号

- `Symbol.asyncIterator`:一个方法，该方法返回对象默认的AsyncIterator。由for-await-of 语句使用
- `Symbol.hasInstance`:一个方法，该方法决定一个构造器对象是否认可一个对象是它的实例。由instanceof 操作符使用
- ...

#### 1.1.7 Object

（1）每个Object实例都有以下属性和方法

```js
//constructor：用于创建当前对象的函数。在前面的例子中，这个属性的值就是Object()函数
//hasOwnProperty(propertyName)：用于判断当前对象实例（不是原型）上是否存在给定的属性。要检查的属性名必须是字符串（如o.hasOwnProperty("name")）或符号。
//isPrototypeOf(object)：用于判断当前对象是否为另一个对象的原型。
//propertyIsEnumerable(propertyName)：用于判断给定的属性是否可以使用or-in 语句枚举。与hasOwnProperty()一样，属性名必须是字符串。
//toLocaleString()：返回对象的字符串表示，该字符串反映对象所在的本地化执行环境。
//toString()：返回对象的字符串表示。
//valueOf()：返回对象对应的字符串、数值或布尔值表示。通常与toString()的返回值相同。
```



### 1.2 语句

#### 1.2.1 基础语句

```js
//if
if(条件){
    //语句
}else if(条件){
    ...
}else{
    ...
}
    
//do-while
do {
    ...
}while(条件)
    
//while
while(条件){
    ...
}
    
//for
for(初始化；条件；每次循环结束执行代码){
    ...
}
```

#### 1.2.2 for in

```js
//for in 会遍历数组所有的可枚举属性，包括原型。例如的原型方法method和name属性
//遍历顺序可能不是实际的内部顺序
//遍历顺序可能不是实际的内部顺序
//故而一般用for in遍历对象而不用来遍历数组
Array.prototype.method=function(){}
var myArray=[1,2,4];
myArray.name="数组";
 
for (var index in myArray){
    console.log(myArray[index]);    //0,1,2,method,name
}
```

#### 1.2.3 for of

```js
//for of不支持普通对象
//for of 不遍历method和name,适合用来遍历数组
Array.prototype.method=function(){}
var myArray=[1,2,4];
myArray.name="数组";

for (var value of myArray) {
    console.log(value);    //1,2,4
}
```

#### 1.2.4 标签语句

```js
//标签语句的典型应用场景是嵌套循环
outermost:
	for (let i = 0; i < 10; i++) {
		for (let j = 0; j < 10; j++) {
			if (i == 5 && j == 5) {
				break outermost;
			}
			num++;
		}
	}
console.log(num); // 55
```

#### 1.2.5 with

```js
//with 语句的用途是将代码作用域设置为特定的对象
//严格模式不允许使用with 语句，否则会抛出错误
//由于with 语句影响性能且难于调试其中的代码，通常不推荐在产品代码中使用with语句。
let qs = location.search.substring(1);
let hostName = location.hostname;
let url = location.href;

//上面代码中的每一行都用到了location 对象。如果使用with 语句，就可以少写一些代码：
with(location) {
	let qs = search.substring(1);
	let hostName = hostname;
	let url = href;
}
```



## 2 作用域

### 2.1 声明提升

- JS代码在运行时, 需要先`声明提升`:  把 `var/let/const/function/class` 声明的变量提升到**作用域**的顶部, 然后再执行提升后的代码
- 注意事项
  - 函数提升: 整体提升 -- 函数体+函数名
  - 函数表达式中的函数不提升:`var 变量 = function (){}`
    - 假如提升: `var 变量 = `    值被提走了, 表达式语法错误
  - var: 只提升 var 的部分, 不提升 = 赋值

```js
// 猜一猜结果是什么?
function b() {
    console.log(1);
}
b()

function b() {
    console.log(2)
}
b()

// 函数作为表达式的一部分, 称为函数表达式
// 函数表达式中的函数 是不提升的
// 加入提升, 则此表达式就会剩下  a =   ; 把值提升, 则表达式不完整会报错!!
a = function b() {
    console.log(3);
}
a()
```

### 2.2 作用域

#### 2.2.1 全局作用域

```js
 // 全局作用域: 就是一个存储了 系统API 的对象
// 不同的 `宿主环境` 提供的全局作用域不同
// 宿主环境: JS运行在什么环境里, 就称为宿主环境 -- 寄生/夺舍
// 例如: 在 node.js 中运行JS, JS的宿主就是 node环境
// 在 浏览器中运行JS, 浏览器就是 JS 的宿主

console.log(window)
// JS除了自身的语法以外, 可以使用宿主的各种功能, 全靠 全局作用域 对象
window.alert('哈哈')

// 全局作用域的特点:
// -- 其中存放了系统的各种API
// -- 在使用全局作用域中的属性时, 可以省略前缀 window.
alert('Hello!')

var a = 10
// 全局变量污染: 使用 var 在 script 中声明的变量, 会存储在全局作用域对象中 -- window里, 称为全局变量污染
// window本来是存储系统API的, 但是你把自定义的属性存储在window中, 造成其污染

// JS做了很多努力, 来避免全局污染 -- 闭包/let/const 块级...

// 应用程序接口（英语：Application Programming Interface，简称：API），又称为应用编程接口, 即 各种提供好的方法和属性
```

#### 2.2.2 脚本作用域

```js
//一个ES6提供的新的全局作用域，存储用户自定义的全局变量
//用let/const声明，存储在script里，没有全局污染
```

#### 2.2.3 块级作用域

```js
//ES6之前用闭包来制作私有的变量，专为函数服务
//ES6之后使用let/const声明块级作用域的变量
```

### 2.3 作用域链

- 如何形成: 在一个作用域中触发函数 生成另一个作用域;  呈现出一种`父子`关系的效果
- 作用域链机制: `子作用域`中使用一个变量时, 按照就近原则查找并使用， 一直向上级作用域中找, 直到找到为止.

```js
// 全局作用域中的变量使用的特点?
// -- 可以省略 window. 前缀
// alert() // window.alert()
// b = 200  //相当于 window.b = 200   对象的属性赋值
var a = 10
function c() {
    a = 100 // 赋值给 c作用域中 var 声明的变量a
    b = 200 // 当前函数作用域中没有 var b, 所以到上层作用域查找
    // 上层全局作用域也没有, 触发另一套机制:  window.b = 200; 认为是省略了 b前方的window.
    var a
    }
c()
console.log(a, b)
```

### 2.4 var/let/const

#### 2.4.1 var与let的区别

```js
//1.var声明的变量是函数作用域，而let是块级作用域

//2.在全局中var声明的变量是window作用域的，而let声明的变量是script作用域的，let不允许全局中重复声明同名变量
var a = 1
let a = 2 //Uncaught SyntaxError: Identifier 'a' has already been declared

//3.暂时性死区
//let在赋值前不能被调用，var赋值前被调用则为undefined
//let的声明提升了，但初始化并未提升
//var的声明和初始化都提升了，初始化为undefined
console.log(name); // undefined
var name = 'Matt';

console.log(age); // Uncaught ReferenceError: Cannot access 'age' before initialization
let age = 26;

//4.不能重复声明
//var声明提升后，能将重复的声明合并为一个
//let不允许重复声明
for (var i = 0; i < 5; ++i) {
	setTimeout(() => console.log(i), 0)
}// 5 5 5 5 5，因为var声明提升，并合并为一个，i是同一个变量

for (let i = 0; i < 5; ++i) {
	setTimeout(() => console.log(i), 0)
}// let为块级作用域，每次循环重新let一个i并赋值
```

#### 2.4.2 let与const的区别

```js
//let与const的区别在于，const声明的变量不可重新赋值
const age = 26;
age = 36; // TypeError: 给常量赋值

//const 声明的限制只适用于它指向的变量的引用。换句话说，如果const 变量引用的是一个对象，那么修改这个对象内部的属性并不违反const 的限制
```

#### 2.4.3 声明风格及最佳实践

- 不使用var
- const 优先，let 次之

### 2.5 闭包

- 闭包是什么?
  - 英文 `closure`
  - 总结: 函数运行时会产生临时的函数作用域, 如果这个函数作用域被 子函数保存了, 则称为闭包
  - 具体: a函数作用域, 被 b函数保存在 scopes 属性里, 就说: a函数作用域是b的闭包
- 函数为什么要有闭包特征呢?

  - 如果 A 函数中 声明了 B函数,  B函数使用了 A函数作用域的属性
  - 常规操作: A函数执行结束后,会自动销毁其 `函数作用域对象`, 导致 x 被销毁, B函数会无法使用
  - 所以 B函数需要把 A函数的作用域保存在自身的 scopes 属性里
  - `B.scopes = [ 0: Closure A {x: 10} ]`
  - 即  A函数作用域 是 B函数的闭包
  - `内层`函数, 保存`外层函数` 作为自己的`闭包`

- 利用闭包 我们可以做什么?

  - 防止全局污染

  - 把函数使用的变量 不在全局中声明,  而是在父级函数中声明, 存储在函数作用域

    固定格式:

    ```js
    var 函数名 = (function(){ 
        var 变量 = 值
        
    	return function(){  }
    })()
    ```

- 闭包特点：只存储对自己有用的属性 , 最大程度节省内存

- 闭包的缺点? `消耗内存`

  - 常规: 函数执行完毕后, 会自动销毁开辟的 `函数作用域` 对象
  - 但是: 因为闭包的存在, 导致对象无法被销毁, 会一直存在于内存中

- 难以理解??

  - `2015`年出版的 ES6 中, 提供了 let/const  搭配 块级/脚本 两个新生作用域, 比闭包使用更加方便快捷,  用于代替闭包
  - 但是: 你开发的软件为了兼容 2015年之前的浏览器, 例如 IE8,  就无法使用新特性, 只能用闭包

## 3 引用类型

- 引用值（或者对象）是某个特定引用类型的实例。
- 引用类型有时候也被称为对象定义，因为它们描述了自己的对象应有的属性和方法。
- 新对象通过使用new 操作符后跟一个构造函数（constructor）来创建。

### 3.1  基本引用类型

#### 3.1.1 Date

**Date 对象属性**

| 属性                                                         | 描述                                 |
| :----------------------------------------------------------- | :----------------------------------- |
| [constructor](https://www.runoob.com/jsref/jsref-constructor-date.html) | 返回对创建此对象的 Date 函数的引用。 |
| [prototype](https://www.runoob.com/jsref/jsref-prototype-date.html) | 使您有能力向对象添加属性和方法。     |

**Date 对象方法**

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [getDate()](https://www.runoob.com/jsref/jsref-getdate.html) | 从 Date 对象返回一个月中的某一天 (1 ~ 31)。                  |
| [getDay()](https://www.runoob.com/jsref/jsref-getday.html)   | 从 Date 对象返回一周中的某一天 (0 ~ 6)。                     |
| [getFullYear()](https://www.runoob.com/jsref/jsref-getfullyear.html) | 从 Date 对象以四位数字返回年份。                             |
| [getHours()](https://www.runoob.com/jsref/jsref-gethours.html) | 返回 Date 对象的小时 (0 ~ 23)。                              |
| [getMilliseconds()](https://www.runoob.com/jsref/jsref-getmilliseconds.html) | 返回 Date 对象的毫秒(0 ~ 999)。                              |
| [getMinutes()](https://www.runoob.com/jsref/jsref-getminutes.html) | 返回 Date 对象的分钟 (0 ~ 59)。                              |
| [getMonth()](https://www.runoob.com/jsref/jsref-getmonth.html) | 从 Date 对象返回月份 (0 ~ 11)。                              |
| [getSeconds()](https://www.runoob.com/jsref/jsref-getseconds.html) | 返回 Date 对象的秒数 (0 ~ 59)。                              |
| [getTime()](https://www.runoob.com/jsref/jsref-gettime.html) | 返回 1970 年 1 月 1 日至今的毫秒数。                         |
| [getTimezoneOffset()](https://www.runoob.com/jsref/jsref-gettimezoneoffset.html) | 返回本地时间与格林威治标准时间 (GMT) 的分钟差。              |
| [getUTCDate()](https://www.runoob.com/jsref/jsref-getutcdate.html) | 根据世界时从 Date 对象返回月中的一天 (1 ~ 31)。              |
| [getUTCDay()](https://www.runoob.com/jsref/jsref-getutcday.html) | 根据世界时从 Date 对象返回周中的一天 (0 ~ 6)。               |
| [getUTCFullYear()](https://www.runoob.com/jsref/jsref-getutcfullyear.html) | 根据世界时从 Date 对象返回四位数的年份。                     |
| [getUTCHours()](https://www.runoob.com/jsref/jsref-getutchours.html) | 根据世界时返回 Date 对象的小时 (0 ~ 23)。                    |
| [getUTCMilliseconds()](https://www.runoob.com/jsref/jsref-getutcmilliseconds.html) | 根据世界时返回 Date 对象的毫秒(0 ~ 999)。                    |
| [getUTCMinutes()](https://www.runoob.com/jsref/jsref-getutcminutes.html) | 根据世界时返回 Date 对象的分钟 (0 ~ 59)。                    |
| [getUTCMonth()](https://www.runoob.com/jsref/jsref-getutcmonth.html) | 根据世界时从 Date 对象返回月份 (0 ~ 11)。                    |
| [getUTCSeconds()](https://www.runoob.com/jsref/jsref-getutcseconds.html) | 根据世界时返回 Date 对象的秒钟 (0 ~ 59)。                    |
| getYear()                                                    | 已废弃。 请使用 getFullYear() 方法代替。                     |
| [parse()](https://www.runoob.com/jsref/jsref-parse.html)     | 返回1970年1月1日午夜到指定日期（字符串）的毫秒数。           |
| [setDate()](https://www.runoob.com/jsref/jsref-setdate.html) | 设置 Date 对象中月的某一天 (1 ~ 31)。                        |
| [setFullYear()](https://www.runoob.com/jsref/jsref-setfullyear.html) | 设置 Date 对象中的年份（四位数字）。                         |
| [setHours()](https://www.runoob.com/jsref/jsref-sethours.html) | 设置 Date 对象中的小时 (0 ~ 23)。                            |
| [setMilliseconds()](https://www.runoob.com/jsref/jsref-setmilliseconds.html) | 设置 Date 对象中的毫秒 (0 ~ 999)。                           |
| [setMinutes()](https://www.runoob.com/jsref/jsref-setminutes.html) | 设置 Date 对象中的分钟 (0 ~ 59)。                            |
| [setMonth()](https://www.runoob.com/jsref/jsref-setmonth.html) | 设置 Date 对象中月份 (0 ~ 11)。                              |
| [setSeconds()](https://www.runoob.com/jsref/jsref-setseconds.html) | 设置 Date 对象中的秒钟 (0 ~ 59)。                            |
| [setTime()](https://www.runoob.com/jsref/jsref-settime.html) | setTime() 方法以毫秒设置 Date 对象。                         |
| [setUTCDate()](https://www.runoob.com/jsref/jsref-setutcdate.html) | 根据世界时设置 Date 对象中月份的一天 (1 ~ 31)。              |
| [setUTCFullYear()](https://www.runoob.com/jsref/jsref-setutcfullyear.html) | 根据世界时设置 Date 对象中的年份（四位数字）。               |
| [setUTCHours()](https://www.runoob.com/jsref/jsref-setutchours.html) | 根据世界时设置 Date 对象中的小时 (0 ~ 23)。                  |
| [setUTCMilliseconds()](https://www.runoob.com/jsref/jsref-setutcmilliseconds.html) | 根据世界时设置 Date 对象中的毫秒 (0 ~ 999)。                 |
| [setUTCMinutes()](https://www.runoob.com/jsref/jsref-setutcminutes.html) | 根据世界时设置 Date 对象中的分钟 (0 ~ 59)。                  |
| [setUTCMonth()](https://www.runoob.com/jsref/jsref-setutcmonth.html) | 根据世界时设置 Date 对象中的月份 (0 ~ 11)。                  |
| [setUTCSeconds()](https://www.runoob.com/jsref/jsref-setutcseconds.html) | setUTCSeconds() 方法用于根据世界时 (UTC) 设置指定时间的秒字段。 |
| setYear()                                                    | 已废弃。请使用 setFullYear() 方法代替。                      |
| [toDateString()](https://www.runoob.com/jsref/jsref-todatestring.html) | 把 Date 对象的日期部分转换为字符串。                         |
| toGMTString()                                                | 已废弃。请使用 toUTCString() 方法代替。                      |
| [toISOString()](https://www.runoob.com/jsref/jsref-toisostring.html) | 使用 ISO 标准返回字符串的日期格式。                          |
| [toJSON()](https://www.runoob.com/jsref/jsref-tojson.html)   | 以 JSON 数据格式返回日期字符串。                             |
| [toLocaleDateString()](https://www.runoob.com/jsref/jsref-tolocaledatestring.html) | 根据本地时间格式，把 Date 对象的日期部分转换为字符串。       |
| [toLocaleTimeString()](https://www.runoob.com/jsref/jsref-tolocaletimestring.html) | 根据本地时间格式，把 Date 对象的时间部分转换为字符串。       |
| [toLocaleString()](https://www.runoob.com/jsref/jsref-tolocalestring.html) | 根据本地时间格式，把 Date 对象转换为字符串。                 |
| [toString()](https://www.runoob.com/jsref/jsref-tostring-date.html) | 把 Date 对象转换为字符串。                                   |
| [toTimeString()](https://www.runoob.com/jsref/jsref-totimestring.html) | 把 Date 对象的时间部分转换为字符串。                         |
| [toUTCString()](https://www.runoob.com/jsref/jsref-toutcstring.html) | 根据世界时，把 Date 对象转换为字符串。实例：`var today = new Date(); var UTCstring = today.toUTCString();` |
| [UTC()](https://www.runoob.com/jsref/jsref-utc.html)         | 根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数。        |
| [valueOf()](https://www.runoob.com/jsref/jsref-valueof-date.html) | 返回 Date 对象的原始值。                                     |

#### 3.1.2 RegExp

- ECMAScript 通过RegExp 类型支持正则表达式。
- 匹配模式标记
  - g：全局模式，表示查找字符串的全部内容，而不是找到第一个匹配的内容就结束
  -  i：不区分大小写，表示在查找匹配时忽略pattern 和字符串的大小写。
  - m：多行模式，表示查找到一行文本末尾时会继续查找。
  - y：粘附模式，表示只查找从lastIndex 开始及之后的字符串。
  - u：Unicode 模式，启用Unicode 匹配。
  -  s：dotAll 模式，表示元字符.匹配任何字符（包括\n 或\r）。
- **RegExp 实例属性**
  - global：布尔值，表示是否设置了g 标记。
  - ignoreCase：布尔值，表示是否设置了i 标记。
  - unicode：布尔值，表示是否设置了u 标记。
  - sticky：布尔值，表示是否设置了y 标记。
  - lastIndex：整数，表示在源字符串中下一次搜索的开始位置，始终从0 开始。
  - multiline：布尔值，表示是否设置了m 标记。
  - dotAll：布尔值，表示是否设置了s 标记。
  - source：正则表达式的字面量字符串（不是传给构造函数的模式字符串），没有开头和结尾的斜杠。
  - flags：正则表达式的标记字符串。始终以字面量而非传入构造函数的字符串模式形式返回（没有前后斜杠）。
- **RegExp 实例方法**

```js
//exec(),只接收要应用模式的字符串作为参数
//如果找到了匹配项，则返回包含第一个匹配信息的数组；如果没找到匹配项，则返回null
//返回的数组虽然是Array 的实例，但包含两个额外的属性：index 和input。
//index 是字符串中匹配模式的起始位置，input 是要查找的字符串。
let text = "mom and dad and baby";
let pattern = /mom( and dad( and baby)?)?/gi;
let matches = pattern.exec(text);
console.log(matches.index); // 0
console.log(matches.input); // "mom and dad and baby"
console.log(matches[0]); // "mom and dad and baby"
console.log(matches[1]); // " and dad and baby"
console.log(matches[2]); // " and baby"
//如果模式设置了全局标记，则每次调用exec()方法会返回一个匹配的信息
//如果没有设置全局标记，则无论对同一个字符串调用多少次exec()，也只会返回第一个匹配的信息。

//正则表达式的另一个方法是test()，接收一个字符串参数。如果输入的文本与模式匹配，则参数返回true，否则返回false。
let text = "000-00-0000";
let pattern = /\d{3}-\d{2}-\d{4}/;
if (pattern.test(text)) {
	console.log("The pattern was matched.");
}


```

```js
// 字符串拥有一个 match 方法, 可以查询出符合正则要求的字符
var a = words.match(regexp)
console.log(a)

//另一个查找模式的字符串方法是search()。
//。这个方法返回模式第一个匹配的位置索引，如果没找到则返回-1

//replace()替换字符
var phone = '13240392482'
var r = /(\d{3})(\d{4})(\d{4})/
// var a = phone.replace(r, '$1****$3')
var a = phone.replace(r, '$1-$2-$3')
console.log(a)
```

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions

| 字符                                                         | 含义                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`\`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-backslash) | 依照下列规则匹配：在非特殊字符之前的反斜杠表示下一个字符是特殊字符，不能按照字面理解。例如，前面没有 "\" 的 "b" 通常匹配小写字母 "b"，即字符会被作为字面理解，无论它出现在哪里。但如果前面加了 "\"，它将不再匹配任何字符，而是表示一个[字符边界](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#note)。在特殊字符之前的反斜杠表示下一个字符不是特殊字符，应该按照字面理解。详情请参阅下文中的 "转义（Escaping）" 部分。如果你想将字符串传递给 RegExp 构造函数，不要忘记在字符串字面量中反斜杠是转义字符。所以为了在模式中添加一个反斜杠，你需要在字符串字面量中转义它。`/[a-z]\s/i` 和 `new RegExp("[a-z]\\s", "i")` 创建了相同的正则表达式：一个用于搜索后面紧跟着空白字符（`\s` 可看后文）并且在 a-z 范围内的任意字符的表达式。为了通过字符串字面量给 RegExp 构造函数创建包含反斜杠的表达式，你需要在字符串级别和正则表达式级别都对它进行转义。例如 `/[a-z]:\\/i` 和 `new RegExp("[a-z]:\\\\","i")` 会创建相同的表达式，即匹配类似 "C:\" 字符串。 |
| [`^`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-caret) | 匹配输入的开始。如果多行标志被设置为 true，那么也匹配换行符后紧跟的位置。例如，`/^A/` 并不会匹配 "an A" 中的 'A'，但是会匹配 "An E" 中的 'A'。当 '`^`' 作为第一个字符出现在一个字符集合模式时，它将会有不同的含义。[反向字符集合](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-negated-character-set) 一节有详细介绍和示例。 |
| [`$`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-dollar) | 匹配输入的结束。如果多行标志被设置为 true，那么也匹配换行符前的位置。例如，`/t$/` 并不会匹配 "eater" 中的 't'，但是会匹配 "eat" 中的 't'。 |
| [`*`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-asterisk) | 匹配前一个表达式 0 次或多次。等价于 `{0,}`。例如，`/bo*/` 会匹配 "A ghost boooooed" 中的 'booooo' 和 "A bird warbled" 中的 'b'，但是在 "A goat grunted" 中不会匹配任何内容。 |
| [`+`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-plus) | 匹配前面一个表达式 1 次或者多次。等价于 `{1,}`。例如，`/a+/` 会匹配 "candy" 中的 'a' 和 "caaaaaaandy" 中所有的 'a'，但是在 "cndy" 中不会匹配任何内容。 |
| [`?`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-questionmark) | 匹配前面一个表达式 0 次或者 1 次。等价于 `{0,1}`。例如，`/e?le?/` 匹配 "angel" 中的 'el'、"angle" 中的 'le' 以及 "oslo' 中的 'l'。如果**紧跟在任何量词 \*、 +、? 或 {} 的后面**，将会使量词变为**非贪婪**（匹配尽量少的字符），和缺省使用的**贪婪模式**（匹配尽可能多的字符）正好相反。例如，对 "123abc" 使用 `/\d+/` 将会匹配 "123"，而使用 `/\d+?/` 则只会匹配到 "1"。还用于先行断言中，如本表的 `x(?=y)` 和 `x(?!y)` 条目所述。 |
| [`.`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-dot) | （小数点）默认匹配除换行符之外的任何单个字符。例如，`/.n/` 将会匹配 "nay, an apple is on the tree" 中的 'an' 和 'on'，但是不会匹配 'nay'。如果 `s` ("dotAll") 标志位被设为 true，它也会匹配换行符。 |
| [`(x)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-capturing-parentheses) | 像下面的例子展示的那样，它会匹配 'x' 并且记住匹配项。其中括号被称为*捕获括号*。模式 `/(foo) (bar) \1 \2/` 中的 '`(foo)`' 和 '`(bar)`' 匹配并记住字符串 "foo bar foo bar" 中前两个单词。模式中的 `\1` 和 `\2` 表示第一个和第二个被捕获括号匹配的子字符串，即 `foo` 和 `bar`，匹配了原字符串中的后两个单词。注意 `\1`、`\2`、...、`\n` 是用在正则表达式的匹配环节，详情可以参阅后文的 [\n](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-backreference) 条目。而在正则表达式的替换环节，则要使用像 `$1`、`$2`、...、`$n` 这样的语法，例如，`'bar foo'.replace(/(...) (...)/, '$2 $1')`。`$&` 表示整个用于匹配的原字符串。 |
| [`(?:x)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-non-capturing-parentheses) | 匹配 'x' 但是不记住匹配项。这种括号叫作*非捕获括号*，使得你能够定义与正则表达式运算符一起使用的子表达式。看看这个例子 `/(?:foo){1,2}/`。如果表达式是 `/foo{1,2}/`，`{1,2}` 将只应用于 'foo' 的最后一个字符 'o'。如果使用非捕获括号，则 `{1,2}` 会应用于整个 'foo' 单词。更多信息，可以参阅下文的 [Using parentheses](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#Using_parentheses) 条目。 |
| [`x(?=y)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-lookahead) | 匹配'x'仅仅当'x'后面跟着'y'.这种叫做先行断言。例如，/Jack(?=Sprat)/会匹配到'Jack'仅当它后面跟着'Sprat'。/Jack(?=Sprat\|Frost)/匹配‘Jack’仅当它后面跟着'Sprat'或者是‘Frost’。但是‘Sprat’和‘Frost’都不是匹配结果的一部分。 |
| [`(?<=y)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-lookahead)x | 匹配'x'仅当'x'前面是'y'.这种叫做后行断言。例如，/(?<=Jack)Sprat/会匹配到' Sprat '仅仅当它前面是' Jack '。/(?<=Jack\|Tom)Sprat/匹配‘ Sprat ’仅仅当它前面是'Jack'或者是‘Tom’。但是‘Jack’和‘Tom’都不是匹配结果的一部分。 |
| [`x(?!y)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-negated-look-ahead) | 仅仅当'x'后面不跟着'y'时匹配'x'，这被称为正向否定查找。例如，仅仅当这个数字后面没有跟小数点的时候，/\d+(?!\.)/ 匹配一个数字。正则表达式/\d+(?!\.)/.exec("3.141") 匹配‘141’而不是‘3.141’ |
| `(?!y)x`                                                     | 仅仅当'x'前面不是'y'时匹配'x'，这被称为反向否定查找。例如，仅仅当这个数字前面没有负号的时候，`/(?<!-)\d+/` 匹配一个数字。 `/(?<!-)\d+/.exec('3')` 匹配到 "3". `/(?<!-)\d+/.exec('-3')` 因为这个数字前有负号，所以没有匹配到。 |
| [`x|y`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-or) | 匹配‘x’或者‘y’。例如，/green\|red/匹配“green apple”中的‘green’和“red apple”中的‘red’ |
| [`{n}`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-quantifier) | n 是一个正整数，匹配了前面一个字符刚好出现了 n 次。 比如， /a{2}/ 不会匹配“candy”中的'a',但是会匹配“caandy”中所有的 a，以及“caaandy”中的前两个'a'。 |
| [`{n,}`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-quantifier) | n 是一个正整数，匹配前一个字符至少出现了 n 次。例如，/a{2,}/ 匹配 "aa", "aaaa" 和 "aaaaa" 但是不匹配 "a"。 |
| [`{n,m}`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-quantifier-range) | n 和 m 都是整数。匹配前面的字符至少 n 次，最多 m 次。如果 n 或者 m 的值是 0， 这个值被忽略。例如，/a{1, 3}/ 并不匹配“cndy”中的任意字符，匹配“candy”中的 a，匹配“caandy”中的前两个 a，也匹配“caaaaaaandy”中的前三个 a。注意，当匹配”caaaaaaandy“时，匹配的值是“aaa”，即使原始的字符串中有更多的 a。 |
| [`[xyz\]`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-character-set) | 一个字符集合。匹配方括号中的任意字符，包括[转义序列](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Grammar_and_types)。你可以使用破折号（-）来指定一个字符范围。对于点（.）和星号（*）这样的特殊符号在一个字符集中没有特殊的意义。他们不必进行转义，不过转义也是起作用的。 例如，[abcd] 和 [a-d] 是一样的。他们都匹配"brisket"中的‘b’,也都匹配“city”中的‘c’。/[a-z.]+/ 和/[\w.]+/与字符串“test.i.ng”匹配。 |
| [`[^xyz\]`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-negated-character-set) | 一个反向字符集。也就是说， 它匹配任何没有包含在方括号中的字符。你可以使用破折号（-）来指定一个字符范围。任何普通字符在这里都是起作用的。例如，[^abc] 和 [^a-c] 是一样的。他们匹配"brisket"中的‘r’，也匹配“chop”中的‘h’。 |
| [`[\b\]`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-backspace) | 匹配一个退格 (U+0008)。（不要和\b混淆了。）                  |
| [`\b`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-word-boundary) | 匹配一个词的边界。一个词的边界就是一个词不被另外一个“字”字符跟随的位置或者前面跟其他“字”字符的位置，例如在字母和空格之间。注意，匹配中不包括匹配的字边界。换句话说，一个匹配的词的边界的内容的长度是 0。（不要和 [\b] 混淆了）使用"moon"举例： /\bm/匹配“moon”中的‘m’； /oo\b/并不匹配"moon"中的'oo'，因为'oo'被一个“字”字符'n'紧跟着。 /oon\b/匹配"moon"中的'oon'，因为'oon'是这个字符串的结束部分。这样他没有被一个“字”字符紧跟着。 /\w\b\w/将不能匹配任何字符串，因为在一个单词中间的字符永远也不可能同时满足没有“字”字符跟随和有“字”字符跟随两种情况。**备注：** JavaScript 的正则表达式引擎将[特定的字符集](https://www.ecma-international.org/ecma-262/5.1/#sec-15.10.2.6)定义为“字”字符。不在该集合中的任何字符都被认为是一个断词。这组字符相当有限：它只包括大写和小写的罗马字母，十进制数字和下划线字符。不幸的是，重要的字符，例如“é”或“ü”，被视为断词。 |
| [`\B`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-non-word-boundary) | 匹配一个非单词边界。匹配如下几种情况：字符串第一个字符为非“字”字符字符串最后一个字符为非“字”字符两个单词字符之间两个非单词字符之间空字符串例如，/\B../匹配"noonday"中的'oo', 而/y\B../匹配"possibly yesterday"中的’yes‘ |
| [`\c*X*`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-control) | 当 X 是处于 A 到 Z 之间的字符的时候，匹配字符串中的一个控制符。例如，`/\cM/` 匹配字符串中的 control-M (U+000D)。 |
| [`\d`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-digit) | 匹配一个数字`。``等价于 [0-9]`。例如， `/\d/` 或者 `/[0-9]/` 匹配"B2 is the suite number."中的'2'。 |
| [`\D`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-non-digit) | 匹配一个非数字字符`。``等价于 [^0-9]`。例如， `/\D/` 或者 `/[^0-9]/` 匹配"B2 is the suite number."中的'B' 。 |
| [`\f`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-form-feed) | 匹配一个换页符 (U+000C)。                                    |
| [`\n`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-line-feed) | 匹配一个换行符 (U+000A)。                                    |
| [`\r`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-carriage-return) | 匹配一个回车符 (U+000D)。                                    |
| [`\s`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-white-space) | 匹配一个空白字符，包括空格、制表符、换页符和换行符。等价于 [ \f\n\r\t\v\u00a0\u1680\u180e\u2000-\u200a\u2028\u2029\u202f\u205f\u3000\ufeff]。例如，`/\s\w*/` 匹配"foo bar."中的' bar'。经测试，\s不匹配"[\u180e](https://unicode-table.com/cn/180E/)"，在当前版本 Chrome(v80.0.3987.122) 和 Firefox(76.0.1) 控制台输入/\s/.test("\u180e") 均返回 false。 |
| [`\S`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-non-white-space) | 匹配一个非空白字符。等价于 `[^ `\f\n\r\t\v\u00a0\u1680\u180e\u2000-\u200a\u2028\u2029\u202f\u205f\u3000\ufeff`]`。例如，`/\S\w*/` 匹配"foo bar."中的'foo'。 |
| [`\t`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-tab) | 匹配一个水平制表符 (U+0009)。                                |
| [`\v`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-vertical-tab) | 匹配一个垂直制表符 (U+000B)。                                |
| [`\w`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-word) | 匹配一个单字字符（字母、数字或者下划线）。等价于 `[A-Za-z0-9_]`。例如，`/\w/` 匹配 "apple," 中的 'a'，"$5.28,"中的 '5' 和 "3D." 中的 '3'。 |
| [`\W`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-non-word) | 匹配一个非单字字符。等价于 `[^A-Za-z0-9_]`。例如，`/\W/` 或者 `/[^A-Za-z0-9_]/` 匹配 "50%." 中的 '%'。 |
| [`\*n*`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-backreference) | 在正则表达式中，它返回最后的第 n 个子捕获匹配的子字符串 (捕获的数目以左括号计数)。比如 `/apple(,)\sorange\1/` 匹配"apple, orange, cherry, peach."中的'apple, orange,' 。 |
| [`\0`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-null) | 匹配 NULL（U+0000）字符， 不要在这后面跟其它小数，因为 `\0<digits>` 是一个八进制转义序列。 |
| [`\xhh`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-hex-escape) | 匹配一个两位十六进制数（\x00-\xFF）表示的字符。              |
| [`\uhhhh`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions#special-unicode-escape) | 匹配一个四位十六进制数表示的 UTF-16 代码单元。               |
| `\u{hhhh}或\u{hhhhh}`                                        | （仅当设置了 u 标志时）匹配一个十六进制数表示的 Unicode 字符。 |

#### 3.1.3 原始值包装类型

**Boolean 对象**

- Boolean 对象属性

| 属性                                                         | 描述                                  |
| :----------------------------------------------------------- | :------------------------------------ |
| [constructor](https://www.runoob.com/jsref/jsref-constructor-boolean.html) | 返回对创建此对象的 Boolean 函数的引用 |
| [prototype](https://www.runoob.com/jsref/jsref-prototype-boolean.html) | 使您有能力向对象添加属性和方法。      |

- Boolean 对象方法

| 方法                                                         | 描述                               |
| :----------------------------------------------------------- | :--------------------------------- |
| [toString()](https://www.runoob.com/jsref/jsref-tostring-boolean.html) | 把布尔值转换为字符串，并返回结果。 |
| [valueOf()](https://www.runoob.com/jsref/jsref-valueof-boolean.html) | 返回 Boolean 对象的原始值。        |

**Number对象**

- Number 对象属性

| 属性                                                         | 描述                                   |
| :----------------------------------------------------------- | :------------------------------------- |
| [constructor](https://www.runoob.com/jsref/jsref-constructor-number.html) | 返回对创建此对象的 Number 函数的引用。 |
| [MAX_VALUE](https://www.runoob.com/jsref/jsref-max-value.html) | 可表示的最大的数。                     |
| [MIN_VALUE](https://www.runoob.com/jsref/jsref-min-value.html) | 可表示的最小的数。                     |
| [NEGATIVE_INFINITY](https://www.runoob.com/jsref/jsref-negative-infinity.html) | 负无穷大，溢出时返回该值。             |
| [NaN](https://www.runoob.com/jsref/jsref-number-nan.html)    | 非数字值。                             |
| [POSITIVE_INFINITY](https://www.runoob.com/jsref/jsref-positive-infinity.html) | 正无穷大，溢出时返回该值。             |
| [prototype](https://www.runoob.com/jsref/jsref-prototype-num.html) | 允许您可以向对象添加属性和方法。       |

- Number 对象方法

| 方法                                                         | 描述                                                 |
| :----------------------------------------------------------- | :--------------------------------------------------- |
| [isFinite](https://www.runoob.com/jsref/jsref-isfinite-number.html) | 检测指定参数是否为无穷大。                           |
| [toExponential(x)](https://www.runoob.com/jsref/jsref-toexponential.html) | 把对象的值转换为指数计数法。                         |
| [toFixed(x)](https://www.runoob.com/jsref/jsref-tofixed.html) | 把数字转换为字符串，结果的小数点后有指定位数的数字。 |
| [toPrecision(x)](https://www.runoob.com/jsref/jsref-toprecision.html) | 把数字格式化为指定的长度。                           |
| [toString()](https://www.runoob.com/jsref/jsref-tostring-number.html) | 把数字转换为字符串，使用指定的基数。                 |
| [valueOf()](https://www.runoob.com/jsref/jsref-valueof-number.html) | 返回一个 Number 对象的基本数字值。                   |

- ES6 新增 Number 属性
  - EPSILON: 表示 1 和比最接近 1 且大于 1 的最小 Number 之间的差别
  - MIN_SAFE_INTEGER: 表示在 JavaScript中最小的安全的 integer 型数字 (`-(253 - 1)`)。
  - MAX_SAFE_INTEGER: 表示在 JavaScript 中最大的安全整数（`253 - 1`）。

**String**

- String 对象属性

| 属性                                                         | 描述                       |
| :----------------------------------------------------------- | :------------------------- |
| [constructor](https://www.runoob.com/jsref/jsref-constructor-string.html) | 对创建该对象的函数的引用   |
| [length](https://www.runoob.com/jsref/jsref-length-string.html) | 字符串的长度               |
| [prototype](https://www.runoob.com/jsref/jsref-prototype-string.html) | 允许您向对象添加属性和方法 |

- String 对象方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [charAt()](https://www.runoob.com/jsref/jsref-charat.html)   | 返回在指定位置的字符。                                       |
| [charCodeAt()](https://www.runoob.com/jsref/jsref-charcodeat.html) | 返回在指定的位置的字符的 Unicode 编码。                      |
| [concat()](https://www.runoob.com/jsref/jsref-concat-string.html) | 连接两个或更多字符串，并返回新的字符串。                     |
| [endsWith()](https://www.runoob.com/jsref/jsref-endswith.html) | 判断当前字符串是否是以指定的子字符串结尾的（区分大小写）。   |
| [fromCharCode()](https://www.runoob.com/jsref/jsref-fromcharcode.html) | 将 Unicode 编码转为字符。                                    |
| [indexOf()](https://www.runoob.com/jsref/jsref-indexof.html) | 返回某个指定的字符串值在字符串中首次出现的位置。             |
| [includes()](https://www.runoob.com/jsref/jsref-string-includes.html) | 查找字符串中是否包含指定的子字符串。                         |
| [lastIndexOf()](https://www.runoob.com/jsref/jsref-lastindexof.html) | 从后向前搜索字符串，并从起始位置（0）开始计算返回字符串最后出现的位置。 |
| [match()](https://www.runoob.com/jsref/jsref-match.html)     | 查找找到一个或多个正则表达式的匹配。                         |
| [repeat()](https://www.runoob.com/jsref/jsref-repeat.html)   | 复制字符串指定次数，并将它们连接在一起返回。                 |
| [replace()](https://www.runoob.com/jsref/jsref-replace.html) | 在字符串中查找匹配的子串，并替换与正则表达式匹配的子串。     |
| [replaceAll()](https://www.runoob.com/jsref/jsref-replaceall.html) | 在字符串中查找匹配的子串，并替换与正则表达式匹配的所有子串。 |
| [search()](https://www.runoob.com/jsref/jsref-search.html)   | 查找与正则表达式相匹配的值。                                 |
| [slice()](https://www.runoob.com/jsref/jsref-slice-string.html) | 提取字符串的片断，并在新的字符串中返回被提取的部分。         |
| [split()](https://www.runoob.com/jsref/jsref-split.html)     | 把字符串分割为字符串数组。                                   |
| [startsWith()](https://www.runoob.com/jsref/jsref-startswith.html) | 查看字符串是否以指定的子字符串开头。                         |
| [substr()](https://www.runoob.com/jsref/jsref-substr.html)   | 从起始索引号提取字符串中指定数目的字符。                     |
| [substring()](https://www.runoob.com/jsref/jsref-substring.html) | 提取字符串中两个指定的索引号之间的字符。                     |
| [toLowerCase()](https://www.runoob.com/jsref/jsref-tolowercase.html) | 把字符串转换为小写。                                         |
| [toUpperCase()](https://www.runoob.com/jsref/jsref-touppercase.html) | 把字符串转换为大写。                                         |
| [trim()](https://www.runoob.com/jsref/jsref-trim.html)       | 去除字符串两边的空白。                                       |
| [toLocaleLowerCase()](https://www.runoob.com/jsref/jsref-tolocalelowercase.html) | 根据本地主机的语言环境把字符串转换为小写。                   |
| [toLocaleUpperCase()](https://www.runoob.com/jsref/jsref-tolocaleuppercase.html) | 根据本地主机的语言环境把字符串转换为大写。                   |
| [valueOf()](https://www.runoob.com/jsref/jsref-valueof-string.html) | 返回某个字符串对象的原始值。                                 |
| [toString()](https://www.runoob.com/jsref/jsref-tostring.html) | 返回一个字符串。                                             |

- String HTML 包装方法

| 方法                                                         | 描述                         |
| :----------------------------------------------------------- | :--------------------------- |
| [anchor()](https://www.runoob.com/jsref/jsref-anchor.html)   | 创建 HTML 锚。               |
| [big()](https://www.runoob.com/jsref/jsref-big.html)         | 用大号字体显示字符串。       |
| [blink()](https://www.runoob.com/jsref/jsref-blink.html)     | 显示闪动字符串。             |
| [bold()](https://www.runoob.com/jsref/jsref-bold.html)       | 使用粗体显示字符串。         |
| [fixed()](https://www.runoob.com/jsref/jsref-fixed.html)     | 以打字机文本显示字符串。     |
| [fontcolor()](https://www.runoob.com/jsref/jsref-fontcolor.html) | 使用指定的颜色来显示字符串。 |
| [fontsize()](https://www.runoob.com/jsref/jsref-fontsize.html) | 使用指定的尺寸来显示字符串。 |
| [italics()](https://www.runoob.com/jsref/jsref-italics.html) | 使用斜体显示字符串。         |
| [link()](https://www.runoob.com/jsref/jsref-link.html)       | 将字符串显示为链接。         |
| [small()](https://www.runoob.com/jsref/jsref-small.html)     | 使用小字号来显示字符串。     |
| [strike()](https://www.runoob.com/jsref/jsref-strike.html)   | 用于显示加删除线的字符串。   |
| [sub()](https://www.runoob.com/jsref/jsref-sub.html)         | 把字符串显示为下标。         |
| [sup()](https://www.runoob.com/jsref/jsref-sup.html)         | 把字符串显示为上标。         |

#### 3.1.4 单例内置对象

**Math**

- Math 对象属性

| 属性                                                       | 描述                                                    |
| :--------------------------------------------------------- | :------------------------------------------------------ |
| [E](https://www.runoob.com/jsref/jsref-e.html)             | 返回算术常量 e，即自然对数的底数（约等于2.718）。       |
| [LN2](https://www.runoob.com/jsref/jsref-ln2.html)         | 返回 2 的自然对数（约等于0.693）。                      |
| [LN10](https://www.runoob.com/jsref/jsref-ln10.html)       | 返回 10 的自然对数（约等于2.302）。                     |
| [LOG2E](https://www.runoob.com/jsref/jsref-log2e.html)     | 返回以 2 为底的 e 的对数（约等于 1.4426950408889634）。 |
| [LOG10E](https://www.runoob.com/jsref/jsref-log10e.html)   | 返回以 10 为底的 e 的对数（约等于0.434）。              |
| [PI](https://www.runoob.com/jsref/jsref-pi.html)           | 返回圆周率（约等于3.14159）。                           |
| [SQRT1_2](https://www.runoob.com/jsref/jsref-sqrt1-2.html) | 返回 2 的平方根的倒数（约等于 0.707）。                 |
| [SQRT2](https://www.runoob.com/jsref/jsref-sqrt2.html)     | 返回 2 的平方根（约等于 1.414）。                       |

- Math 对象方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [abs(x)](https://www.runoob.com/jsref/jsref-abs.html)        | 返回 x 的绝对值。                                            |
| [acos(x)](https://www.runoob.com/jsref/jsref-acos.html)      | 返回 x 的反余弦值。                                          |
| [asin(x)](https://www.runoob.com/jsref/jsref-asin.html)      | 返回 x 的反正弦值。                                          |
| [atan(x)](https://www.runoob.com/jsref/jsref-atan.html)      | 以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。     |
| [atan2(y,x)](https://www.runoob.com/jsref/jsref-atan2.html)  | 返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。 |
| [ceil(x)](https://www.runoob.com/jsref/jsref-ceil.html)      | 对数进行上舍入。                                             |
| [cos(x)](https://www.runoob.com/jsref/jsref-cos.html)        | 返回数的余弦。                                               |
| [exp(x)](https://www.runoob.com/jsref/jsref-exp.html)        | 返回 Ex 的指数。                                             |
| [floor(x)](https://www.runoob.com/jsref/jsref-floor.html)    | 对 x 进行下舍入。                                            |
| [log(x)](https://www.runoob.com/jsref/jsref-log.html)        | 返回数的自然对数（底为e）。                                  |
| [max(x,y,z,...,n)](https://www.runoob.com/jsref/jsref-max.html) | 返回 x,y,z,...,n 中的最高值。                                |
| [min(x,y,z,...,n)](https://www.runoob.com/jsref/jsref-min.html) | 返回 x,y,z,...,n中的最低值。                                 |
| [pow(x,y)](https://www.runoob.com/jsref/jsref-pow.html)      | 返回 x 的 y 次幂。                                           |
| [random()](https://www.runoob.com/jsref/jsref-random.html)   | 返回 0 ~ 1 之间的随机数。                                    |
| [round(x)](https://www.runoob.com/jsref/jsref-round.html)    | 四舍五入。                                                   |
| [sin(x)](https://www.runoob.com/jsref/jsref-sin.html)        | 返回数的正弦。                                               |
| [sqrt(x)](https://www.runoob.com/jsref/jsref-sqrt.html)      | 返回数的平方根。                                             |
| [tan(x)](https://www.runoob.com/jsref/jsref-tan.html)        | 返回角的正切。                                               |

**JavaScript全局**

- JavaScript 全局属性

| 属性                                                         | 描述                     |
| :----------------------------------------------------------- | :----------------------- |
| [Infinity](https://www.runoob.com/jsref/jsref-infinity.html) | 代表正的无穷大的数值。   |
| [NaN](https://www.runoob.com/jsref/jsref-nan.html)           | 指示某个值是不是数字值。 |
| [undefined](https://www.runoob.com/jsref/jsref-undefined.html) | 指示未定义的值。         |

- JavaScript 全局函数

| 函数                                                         | 描述                                               |
| :----------------------------------------------------------- | :------------------------------------------------- |
| [decodeURI()](https://www.runoob.com/jsref/jsref-decodeuri.html) | 解码某个编码的 URI。                               |
| [decodeURIComponent()](https://www.runoob.com/jsref/jsref-decodeuricomponent.html) | 解码一个编码的 URI 组件。                          |
| [encodeURI()](https://www.runoob.com/jsref/jsref-encodeuri.html) | 把字符串编码为 URI。                               |
| [encodeURIComponent()](https://www.runoob.com/jsref/jsref-encodeuricomponent.html) | 把字符串编码为 URI 组件。                          |
| [escape()](https://www.runoob.com/jsref/jsref-escape.html)   | 对字符串进行编码。                                 |
| [eval()](https://www.runoob.com/jsref/jsref-eval.html)       | 计算 JavaScript 字符串，并把它作为脚本代码来执行。 |
| [isFinite()](https://www.runoob.com/jsref/jsref-isfinite.html) | 检查某个值是否为有穷大的数。                       |
| [isNaN()](https://www.runoob.com/jsref/jsref-isnan.html)     | 检查某个值是否是数字。                             |
| [Number()](https://www.runoob.com/jsref/jsref-number.html)   | 把对象的值转换为数字。                             |
| [parseFloat()](https://www.runoob.com/jsref/jsref-parsefloat.html) | 解析一个字符串并返回一个浮点数。                   |
| [parseInt()](https://www.runoob.com/jsref/jsref-parseint.html) | 解析一个字符串并返回一个整数。                     |
| [String()](https://www.runoob.com/jsref/jsref-string.html)   | 把对象的值转换为字符串。                           |
| [unescape()](https://www.runoob.com/jsref/jsref-unescape.html) | 对由 escape() 编码的字符串进行解码。               |

**Error**

- Error 对象属性

| 属性                                                         | 描述                           |
| :----------------------------------------------------------- | :----------------------------- |
| [name](https://www.runoob.com/jsref/prop-error-name.html)    | 设置或返回一个错误名           |
| [message](https://www.runoob.com/jsref/prop-error-message.html) | 设置或返回一个错误信息(字符串) |



### 3.2 集合引用类型

#### 3.2.1 Object

```js
//显式地创建Object 的实例有两种方式。
//第一种是使用new 操作符和Object 构造函数
let person = new Object();
person.name = "Nicholas";
person.age = 29;
//另一种方式是使用对象字面量（object literal）表示法。
let person = {
    name: "Nicholas",
    age: 29
};

//注意 在使用对象字面量表示法定义对象时，并不会实际调用Object 构造函数。

//对象字面量已经成为给函数传递大量可选参数的主要方式
//。最好的方式是对必选参数使用命名参数，再通过一个对象字面量来封装多个可选参数
function displayInfo(args) {
    let output = "";
    if (typeof args.name == "string"){
        output += "Name: " + args.name + "\n";
    }
    if (typeof args.age == "number") {
        output += "Age: " + args.age + "\n";
    }
    alert(output);
}
displayInfo({
    name: "Nicholas",
    age: 29
});
displayInfo({
	name: "Greg"
});

//对象的属性可以通过点语法与中括号语法来访问
//使用中括号时，要在括号内使用属性名的字符串形式，优势在于可以通过变量访问属性
//通常，点语法是首选的属性存取方式，除非访问属性时必须使用变量。
```

#### 3.2.2 Array

> ECMAScript 数组也是一组有序的数据，数组中每个槽位可以存储任意类型的数据。数组也是动态大小的，会随着数据添加而自动增长。

**创建数组**

```js
//1.构造函数
let colors = new Array();
let colors = new Array(3); // 创建一个包含3 个元素的数组
let names = new Array("Greg"); // 创建一个只包含一个元素，即字符串"Greg"的数组
let colors = Array(3); //可以省略new

//2.数组字面量
let colors = ["red", "blue", "green"]; // 创建一个包含3 个元素的数组

//3.Array.from()  【ES6】 用于将类数组结构转换为数组实例
//Array.from()的第一个参数是一个类数组对象，即任何可迭代的结构，或者有一个length 属性和可索引元素的结构
// 字符串会被拆分为单字符数组
console.log(Array.from("Matt")); // ["M", "a", "t", "t"]
// Array.from()对现有数组执行浅复制
const a1 = [1, 2, 3, 4];
const a2 = Array.from(a1); 
console.log(a1); // [1, 2, 3, 4]
//Array.from()还接收第二个可选的映射函数参数。这个函数可以直接增强新数组的值
//还可以接收第三个可选参数，用于指定映射函数中this 的值。但这个重写的this 值在箭头函数中不适用。
const a1 = [1, 2, 3, 4];
const a2 = Array.from(a1, x => x**2);
const a3 = Array.from(a1, function(x) {return x**this.exponent}, {exponent: 2});
console.log(a2); // [1, 4, 9, 16]
console.log(a3); // [1, 4, 9, 16]

//Array.of()  【ES6】 把一组参数转换为数组
console.log(Array.of(1, 2, 3, 4)); // [1, 2, 3, 4]
console.log(Array.of(undefined)); // [undefined]
```

**数组空位**

- ES6将空位定义为值为undefined的元素，而ES6之前会忽略空位，但具体的行为也会因方法而异
- **注意** 由于行为不一致和存在性能隐患，因此实践中要避免使用数组空位。如果确实需要空位，则可以显式地用undefined 值代替。

```js
//使用数组字面量初始化数组时，可以使用一串逗号来创建空位（hole）
const options = [,,,,,]; // 创建包含5 个元素的数组
console.log(options.length); // 5
console.log(options); // [,,,,,]
```

**数组索引**

- 如果索引小于数组包含的元素数，则返回存储在相应位置的元素
- 如果索引大于数组包含的元素数，则数组长度会自动扩展到该索引值加1，扩展的元素值为undefined
- **注意** 数组最多可以包含4 294 967 295 个元素，这对于大多数编程任务应该足够了。如果尝试添加更多项，则会导致抛出错误。以这个最大值作为初始值创建数组，可能导致脚本运行时间过长的错误。

**检测数组**

- 一个全局执行上下文： `value instanceof Array`
- 若干个全局上下文： `Array.isArray(value)`

**迭代器方法**

- `keys()`返回数组索引的迭代器
- `values()`返回数组元素的迭代器
- `entries()`返回索引/值对的迭代器

```js
const a = ["foo", "bar", "baz", "qux"];
// 因为这些方法都返回迭代器，所以可以将它们的内容
// 通过Array.from()直接转换为数组实例
const aKeys = Array.from(a.keys());
const aValues = Array.from(a.values());
const aEntries = Array.from(a.entries());
console.log(aKeys); // [0, 1, 2, 3]
console.log(aValues); // ["foo", "bar", "baz", "qux"]
console.log(aEntries); // [[0, "foo"], [1, "bar"], [2, "baz"], [3, "qux"]]

//使用ES6 的解构可以非常容易地在循环中拆分键/值对
const a = ["foo", "bar", "baz", "qux"];
for (const [idx, element] of a.entries()) {
    alert(idx);
    alert(element);
}
```

**复制和填充**

- 批量复制 `copyWithin(starIndex,endIndex)`
- 填充数组 `fill(insertIndex,starIndex,endIndex)`
- 都是包含startIndex，不包含endIndex
- 静默忽略超出数组边界、零长度及方向相反的索引范围
- 负值索引从数组末尾开始计算

**转换方法**

- `valueOf()`返回的还是数组本身
- `toString()`返回由数组中每个值的等效字符串拼接而成的一个逗号分隔的字符串
- `toLocaleString()`可能返回跟toString()和valueOf()相同的结果，但也不一定。与另外两个方法唯一的区别是，为了得到最终的字符串，会调用数组每个值的toLocaleString()方法

**栈方法**

- `push()`接收任意数量的参数，并将它们添加到数组末尾，返回数组的最新长度
- `pop()`删除数组的最后一项，同时减少数组的length 值，返回被删除的项。

**队列方法**

- `shift()`删除数组的第一项并返回它，然后数组长度减1
- `shift()`和`push()`可以模拟队列
- `unshift()`在数组开头添加任意多个值，然后返回新的数组长度
- `unshift()`和`pop()`可以反向模拟队列

**排序**

- `reverse()`将数组元素反向排列
- `sort()` sort()会在每一项上调用String()转型函数，然后比较字符串来决定顺序。还可以接收一个比较函数，用于判断哪个值应该排在前面
- **注意** reverse()和sort()都返回调用它们的数组的引用。

**操作方法**

- `concat`首先会创建一个当前数组的副本，然后再把它的参数添加到副本末尾，最后返回这个新构建的数组
- `slice()`接收一个或两个参数：返回元素的开始索引和结束索引，返回操作后的数组
- `splice()`，参数：起始位置，删除数量，增加的元素

**搜索和位置方法**

- `indexOf()` / `lastIndexOf()`，返回匹配项位置，未找到则返回-1
- `includes()`【ES7】，返回布尔值
- `find()`返回第一个匹配的元素
- `findIndex()`返回第一个匹配元素的索引

**迭代方法**

- `every()`：对数组每一项都运行传入的函数，如果对每一项函数都返回true，则这个方法返回true。
-  `filter()`：对数组每一项都运行传入的函数，函数返回true 的项会组成数组之后返回。
-  `forEach()`：对数组每一项都运行传入的函数，没有返回值。
-  `map()`：对数组每一项都运行传入的函数，返回由每次函数调用的结果构成的数组。
-  `some()`：对数组每一项都运行传入的函数，如果有一项函数返回true，则这个方法返回true。

**归并方法**

- `reduce()`方法从数组第一项开始遍历到最后一项。
- `reduceRight()`从最后一项开始遍历至第一项。

| 属性                                                         | 描述                             |
| :----------------------------------------------------------- | :------------------------------- |
| [constructor](https://www.runoob.com/jsref/jsref-constructor-array.html) | 返回创建数组对象的原型函数。     |
| [length](https://www.runoob.com/jsref/jsref-length-array.html) | 设置或返回数组元素的个数。       |
| [prototype](https://www.runoob.com/jsref/jsref-prototype-array.html) | 允许你向数组对象添加属性或方法。 |

| 方法                                                         | 描述                                                 |
| :----------------------------------------------------------- | :--------------------------------------------------- |
| [concat()](https://www.runoob.com/jsref/jsref-concat-array.html) | 连接两个或更多的数组，并返回结果。                   |
| [copyWithin()](https://www.runoob.com/jsref/jsref-copywithin.html) | 从数组的指定位置拷贝元素到数组的另一个指定位置中。   |
| [entries()](https://www.runoob.com/jsref/jsref-entries.html) | 返回数组的可迭代对象。                               |
| [every()](https://www.runoob.com/jsref/jsref-every.html)     | 检测数值元素的每个元素是否都符合条件。               |
| [fill()](https://www.runoob.com/jsref/jsref-fill.html)       | 使用一个固定值来填充数组。                           |
| [filter()](https://www.runoob.com/jsref/jsref-filter.html)   | 检测数值元素，并返回符合条件所有元素的数组。         |
| [find()](https://www.runoob.com/jsref/jsref-find.html)       | 返回符合传入测试（函数）条件的数组元素。             |
| [findIndex()](https://www.runoob.com/jsref/jsref-findindex.html) | 返回符合传入测试（函数）条件的数组元素索引。         |
| [forEach()](https://www.runoob.com/jsref/jsref-foreach.html) | 数组每个元素都执行一次回调函数。                     |
| [from()](https://www.runoob.com/jsref/jsref-from.html)       | 通过给定的对象中创建一个数组。                       |
| [includes()](https://www.runoob.com/jsref/jsref-includes.html) | 判断一个数组是否包含一个指定的值。                   |
| [indexOf()](https://www.runoob.com/jsref/jsref-indexof-array.html) | 搜索数组中的元素，并返回它所在的位置。               |
| [isArray()](https://www.runoob.com/jsref/jsref-isarray.html) | 判断对象是否为数组。                                 |
| [join()](https://www.runoob.com/jsref/jsref-join.html)       | 把数组的所有元素放入一个字符串。                     |
| [keys()](https://www.runoob.com/jsref/jsref-keys.html)       | 返回数组的可迭代对象，包含原始数组的键(key)。        |
| [lastIndexOf()](https://www.runoob.com/jsref/jsref-lastindexof-array.html) | 搜索数组中的元素，并返回它最后出现的位置。           |
| [map()](https://www.runoob.com/jsref/jsref-map.html)         | 通过指定函数处理数组的每个元素，并返回处理后的数组。 |
| [pop()](https://www.runoob.com/jsref/jsref-pop.html)         | 删除数组的最后一个元素并返回删除的元素。             |
| [push()](https://www.runoob.com/jsref/jsref-push.html)       | 向数组的末尾添加一个或更多元素，并返回新的长度。     |
| [reduce()](https://www.runoob.com/jsref/jsref-reduce.html)   | 将数组元素计算为一个值（从左到右）。                 |
| [reduceRight()](https://www.runoob.com/jsref/jsref-reduceright.html) | 将数组元素计算为一个值（从右到左）。                 |
| [reverse()](https://www.runoob.com/jsref/jsref-reverse.html) | 反转数组的元素顺序。                                 |
| [shift()](https://www.runoob.com/jsref/jsref-shift.html)     | 删除并返回数组的第一个元素。                         |
| [slice()](https://www.runoob.com/jsref/jsref-slice-array.html) | 选取数组的一部分，并返回一个新数组。                 |
| [some()](https://www.runoob.com/jsref/jsref-some.html)       | 检测数组元素中是否有元素符合指定条件。               |
| [sort()](https://www.runoob.com/jsref/jsref-sort.html)       | 对数组的元素进行排序。                               |
| [splice()](https://www.runoob.com/jsref/jsref-splice.html)   | 从数组中添加或删除元素。                             |
| [toString()](https://www.runoob.com/jsref/jsref-tostring-array.html) | 把数组转换为字符串，并返回结果。                     |
| [unshift()](https://www.runoob.com/jsref/jsref-unshift.html) | 向数组的开头添加一个或更多元素，并返回新的长度。     |
| [valueOf()](https://www.runoob.com/jsref/jsref-valueof-array.html) | 返回数组对象的原始值。                               |

#### 3.2.3 Map【ES6】【...】

```js

```

#### 3.2.4 Set【ES6】【...】

```js

```



## 4 迭代器与生成器【...】



## 5 对象

- ECMA-262 将对象定义为一组属性的无序集合
- 对象就是一组没有特定顺序的值。对象的每个属性或方法都由一个名称来标识，这个名称映射到一个值。
- 可以把ECMAScript 的对象想象成一张散列表，其中的内容就是一组名/值对，值可以是数据或者函数。

### 5.1 理解对象

#### 5.1.1 创建Object新实例

```js
//创建Object新实例
let person = new Object();
person.name = "Nicholas";
person.age = 29;
person.job = "Software Engineer";
person.sayName = function() {
	console.log(this.name);
};
```

#### 5.1.2 对象字面量

```js
//对象字面量
//字面量(literal)用于表达源代码中一个值的表示法(notation)
let person = {
    name: "Nicholas",
    age: 29,
    job: "Software Engineer",
    sayName() {
        console.log(this.name);
    }
};
```

#### 5.1.3 数据属性

- `[[Configurable]]`：表示属性是否可以通过delete 删除并重新定义，是否可以修改它的特性，以及是否可以把它改为访问器属性。默认情况下，所有直接定义在对象上的属性的这个特性都是true，如前面的例子所示。
- `[[Enumerable]]`：表示属性是否可以通过for-in 循环返回。默认情况下，所有直接定义在对象上的属性的这个特性都是true，如前面的例子所示。
- `[[Writable]]`：表示属性的值是否可以被修改。默认情况下，所有直接定义在对象上的属性的这个特性都是true，如前面的例子所示。
- `[[Value]]`：包含属性实际的值。这就是前面提到的那个读取和写入属性值的位置。这个特性的默认值为undefined。
- 将属性显式添加到对象之后，`[[Configurable]]`、`[[Enumerable]]`和`[[Writable]]`都会被设置为true，而`[[Value]]`特性会被设置为指定的值。

```js
//数据属性
//要修改属性的默认特性，就必须使用Object.defineProperty()方法
//这个方法接收3 个参数：要给其添加属性的对象、属性的名称和一个描述符对象
let person = {};
Object.defineProperty(person, "name", {
	writable: false,
	value: "Nicholas"
});
console.log(person.name); // "Nicholas"
person.name = "Greg";
console.log(person.name); // "Nicholas"
//在非严格模式下尝试给这个属性重新赋值会被忽略。在严格模式下，尝试修改只读属性的值会抛出错误
```

#### 5.1.4 访问器属性

- `[[Configurable]]`：表示属性是否可以通过delete 删除并重新定义，是否可以修改它的特性，以及是否可以把它改为访问器属性。默认情况下，所有直接定义在对象上的属性的这个特性都是true，如前面的例子所示。
- `[[Enumerable]]`：表示属性是否可以通过for-in 循环返回。默认情况下，所有直接定义在对象上的属性的这个特性都是true，如前面的例子所示。
- `[[Get]]`：获取函数，在读取属性时调用。默认值为undefined。
- `[[Set]]`：设置函数，在写入属性时调用。默认值为undefined。

```js
//访问器属性:[[Configurable]]、[[Enumerable]]默认为true,[[Get]]、[[Set]]默认为undefined
// 定义一个对象，包含伪私有成员year_和公共成员edition
//year_中的下划线常用来表示该属性并不希望在对象方法的外部被访问
//另一个属性year 被定义为一个访问器属性，其中获取函数简单地返回year_的值，而设置函数会做一些计算以决定正确的版本（edition）。因
let book = {
	year_: 2017,
	edition: 1
};
Object.defineProperty(book, "year", {
    get() {
    	return this.year_;
    },
    set(newValue) {
        if (newValue > 2017) {
            this.year_ = newValue;
            this.edition += newValue - 2017;
        }
    }
});
book.year = 2018;
console.log(book.edition); // 2
```

#### 5.1.5 定义多个属性

```js
//定义多个属性
//Object.define-Properties()
let book = {};
Object.defineProperties(book, {
    year_: {
    	value: 2017
    },
    edition: {
    	value: 1
    }
}
```

#### 5.1.6 读取属性的特性

```js                        
//读取属性的特性
//Object.getOwnPropertyDescriptor()
//这个方法接收两个参数：属性所在的对象和要取得其描述符的属性名
//返回值是一个对象，对于访问器属性包含
//configurable、enumerable、get 和set 属性，对于数据属性包含configurable、numerable、writable 和value 属性。
//ECMAScript 2017 新增了Object.getOwnPropertyDescriptors()静态方法。这个方法实际上会在每个自有属性上调用Object.getOwnPropertyDescriptor()并在一个新对象中返回它们
```

#### 5.1.7 合并对象

```js                        
//合并对象
//ECMAScript 6 专门为合并对象提供了Object.assign()方法。这个方法接收一个目标对象和一个或多个源对象作为参数，然后将每个源对象中可枚举（Object.propertyIsEnumerable()返回true）和自有（Object.hasOwnProperty()返回true）属性复制到目标对象            
let dest, src, result;
/*简单复制*/
dest = {};
src = { id: 'src' };
result = Object.assign(dest, src);
// Object.assign 修改目标对象
// 也会返回修改后的目标对象
console.log(dest === result); // true
console.log(dest !== src); // true
console.log(result); // { id: src }
console.log(dest); // { id: src }       

//对象标识及相等判定
// === 与 isObject()
```

#### 5.1.8 增强的对象语法

（1）属性简写

```js
//增强的对象语法
//1.属性简写
//在给对象添加变量的时候，开发者经常会发现属性名和变量名是一样的
let name = 'Matt';
let person = {
	name: name
};
console.log(person); // { name: 'Matt' }
//等价于
let name = 'Matt';
let person = {
	name
};
console.log(person); // { name: 'Matt' }
```

（2）可计算属性

```js
//2.可计算属性
//可计算属性表达式中抛出任何错误都会中断对象创建
//如果表达式抛出错误，那么之前完成的计算是不能回滚的。
const nameKey = 'name';
const ageKey = 'age';
const jobKey = 'job';
let person = {
	[nameKey]: 'Matt',
	[ageKey]: 27,
	[jobKey]: 'Software engineer'
};
console.log(person); // { name: 'Matt', age: 27, job: 'Software engineer' }
```

（3）简写方法名

```js
//3.简写方法名
//sayName : function(...){...}简写为sayName(...){...}
//即，可省略  :function
let person = {
    sayName(name) {
    	console.log(`My name is ${name}`);
    }
};
person.sayName('Matt'); // My name is Matt	
```

（4）对象解构

```js
//4.对象解构
let person = {
    name: 'Matt',
    age: 27
};
let { name, age } = person;
console.log(name); // Matt
console.log(age); // 27

//别名
let {name:pname,age:page} = person;
console.log(pname);
console.log(page);

//解构并不要求变量必须在解构表达式中声明。不过，如果是给事先声明的变量赋值，则赋值表达式必须包含在一对括号中
let personName, personAge;
let person = {
    name: 'Matt',
    age: 27
};
({name: personName, age: personAge} = person);
console.log(personName, personAge); // Matt, 27
```

#### 5.1.9 在函数参数中使用解构赋值

```js
//在函数参数中使用解构赋值
let person = {
    name: 'Matt',
    age: 27
};
function printPerson(foo, {name, age}, bar) {
    console.log(arguments);
    console.log(name, age);
}
function printPerson2(foo, {name: personName, age: personAge}, bar) {
    console.log(arguments);
    console.log(personName, personAge);
}
printPerson('1st', person, '2nd');
// ['1st', { name: 'Matt', age: 27 }, '2nd']
// 'Matt', 27
printPerson2('1st', person, '2nd');
// ['1st', { name: 'Matt', age: 27 }, '2nd']
// 'Matt', 27
```

#### 5.1.10 常用对象静态方法

[MDN-object静态方法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)

```js
'use strict'
//使对象无法增加属性
Object.preventExtensions()
//使对象无法增、删属性
Object.seal()
//使对象无法增、删、改属性
Object.freeze()
//通过复制一个或多个对象来创建一个新的对象。
Object.assign()
...
```

### 5.2 创建对象

#### 5.2.1 工厂模式

```js
//工厂模式是一种众所周知的设计模式，广泛应用于软件工程领域，用于抽象创建特定对象的过程。
function createPerson(name, age, job) {
    let o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayName = function() {
    	console.log(this.name);
    };
    return o;
}
let person1 = createPerson("Nicholas", 29, "Software Engineer");
let person2 = createPerson("Greg", 27, "Doctor");
//这种工厂模式虽然可以解决创建多个类似对象的问题，但没有解决对象标识问题（即新创建的对象是什么类型
//其定义的方法会在每个实例上都创建一遍
```

#### 5.2.2 构造函数模式

```js
//按照惯例，构造函数名称的首字母都是要大写的
//定义自定义构造函数可以确保实例被标识为特定类型
//构造函数不一定要写成函数声明的形式。赋值给变量的函数表达式也可以表示构造函数
//例如：let Person = function(name, age, job) {...}
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = function() {
    	console.log(this.name);
	};
}
let person1 = new Person("Nicholas", 29, "Software Engineer");
let person2 = new Person("Greg", 27, "Doctor");
person1.sayName(); // Nicholas
person2.sayName(); // Greg

//构造函数与普通函数唯一的区别就是调用方式不同
// 作为构造函数
let person = new Person("Nicholas", 29, "Software Engineer");
person.sayName(); // "Nicholas"
// 作为函数调用
Person("Greg", 27, "Doctor"); // 添加到window 对象
window.sayName(); // "Greg"
// 在另一个对象的作用域中调用
let o = new Object();
Person.call(o, "Kristen", 25, "Nurse");
o.sayName(); // "Kristen"

//构造函数的主要问题在于，其定义的方法会在每个实例上都创建一遍
console.log(person1.sayName == person2.sayName); // false
//要解决这个问题，可以把函数定义转移到构造函数外部,但是这样虽然解决了相同逻辑的函数重复定义的问题，但全局作用域也因此被搞乱了
```

#### 5.2.3 原型模式

```js
//每个函数都会创建一个prototype 属性，这个属性是一个对象，包含应该由特定引用类型的实例共享的属性和方法。实际上，这个对象就是通过调用构造函数创建的对象的原型
//使用原型对象的好处是，在它上面定义的属性和方法可以被对象实例共享
function Person() {}
Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function() {
	console.log(this.name);
};
let person1 = new Person();
person1.sayName(); // "Nicholas"
let person2 = new Person();
person2.sayName(); // "Nicholas"
console.log(person1.sayName == person2.sayName); // true

//只要创建一个函数，就会按照特定的规则为这个函数创建一个prototype 属性（指向原型对象）
//所有原型对象自动获得一个名为constructor 的属性，指回与之关联的构造函数
```

```js
//判断对象的原型
//Object.isPrototypeOf()
console.log(Person.prototype.isPrototypeOf(person1)); // true
//获得对象的原型
//Object.getPrototypeOf()
console.log(Object.getPrototypeOf(person1) == Person.prototype); // true

//可以向实例的私有特性[[Prototype]]写入一个新值。这样就可以重写一个对象的原型继承关系
//Object.setPrototypeOf()
let biped = {
	numLegs: 2
};
let person = {
	name: 'Matt'
};
Object.setPrototypeOf(person, biped);
console.log(person.name); // Matt
console.log(person.numLegs); // 2
console.log(Object.getPrototypeOf(person) === biped); // true
//Object.setPrototypeOf()可能会严重影响代码性能,不仅是执行Object.setPrototypeOf()语句那么简单，而是会涉及所有访问了那些修改过[[Prototype]]的对象的代码。

//为避免使用Object.setPrototypeOf()可能造成的性能下降，可以通过Object.create()来创建一个新对象，同时为其指定原型
let biped = {
	numLegs: 2
};
let person = Object.create(biped);
person.name = 'Matt';
console.log(person.name); // Matt
console.log(person.numLegs); // 2
console.log(Object.getPrototypeOf(person) === biped); // true
```

```js
//原型和in 操作符
//有两种方式使用in 操作符：单独使用和在for-in 循环中使用
//在for-in 循环中使用in 操作符时，可以通过对象访问且可以被枚举的属性都会返回，包括实例属性和原型属性
//in 操作符会在可以通过对象访问指定属性时返回true，无论该属性是在实例上还是在原型上
function Person() {}
    Person.prototype.name = "Nicholas";
    Person.prototype.age = 29;
    Person.prototype.job = "Software Engineer";
    Person.prototype.sayName = function() {
    	console.log(this.name);
};
let person1 = new Person();
let person2 = new Person();
console.log(person1.hasOwnProperty("name")); // false
console.log("name" in person1); // true
person1.name = "Greg";
console.log(person1.name); // "Greg"，来自实例
console.log(person1.hasOwnProperty("name")); // true
console.log("name" in person1); // true
console.log(person2.name); // "Nicholas"，来自原型
console.log(person2.hasOwnProperty("name")); // false
console.log("name" in person2); // true

//要获得对象上所有可枚举的实例属性，可以使用Object.keys()方法。这个方法接收一个对象作为参数，返回包含该对象所有可枚举属性名称的字符串数组
let p1 = new Person();
p1.name = "Rob";
p1.age = 31;
let p1keys = Object.keys(p1);
console.log(p1keys); // "[name,age]"

//如果想列出所有实例属性，无论是否可以枚举，都可以使用Object.getOwnPropertyNames()
//在ECMAScript 6 新增符号类型之后，相应地出现了增加一个bject.getOwnPropertyNames()的兄弟方法的需求，因为以符号为键的属性没有名称的概念。因此，Object.getOwnProperty-symbols()

//for-in 循环和Object.keys()的枚举顺序是不确定的，取决于JavaScript 引擎，可能因浏览器而异。
//Object.getOwnPropertyNames()、Object.getOwnPropertySymbols()和object.assign()的枚举顺序是确定性的
```

```js
//对象迭代
//Object.values()
//Object.entries()
//符号属性会被忽略
const o = {
    foo: 'bar',
    baz: 1,
    qux: {}
};
console.log(Object.values(o));
// ["bar", 1, {}]
console.log(Object.entries((o)));
// [["foo", "bar"], ["baz", 1], ["qux", {}]]

```

```js
//其他原型语法
function Person() {}
Person.prototype = {
    name: "Nicholas",
    age: 29,
    job: "Software Engineer",
    sayName() {
    	console.log(this.name);
	}
};
// 恢复constructor 属性
Object.defineProperty(Person.prototype, "constructor", {
    enumerable: false,
    value: Person
});
```

```js
//原型的动态性
let friend = new Person();
Person.prototype.sayHi = function() {
	console.log("hi");
};
friend.sayHi(); // "hi"，没问题！

//实例的[[Prototype]]指针是在调用构造函数时自动赋值的
//这个指针即使把原型修改为不同的对象也不会变。重写整个原型会切断最初原型与构造函数的联系
//但实例引用的仍然是最初的原型
//实例只有指向原型的指针，没有指向构造函数的指针
function Person() {}
let friend = new Person();
Person.prototype = {
    constructor: Person,
    name: "Nicholas",
    age: 29,
    job: "Software Engineer",
	sayName() {
		console.log(this.name);
	}
};
friend.sayName(); // 错误
```

```js
//原型的问题
//1.弱化了向构造函数传递初始化参数的能力，会导致所有实例默认都取得相同的属性值
//2.共享特性,不同实例间，包含引用值的属性会共享
function Person() {}
Person.prototype = {
    constructor: Person,
    name: "Nicholas",
    age: 29,
    job: "Software Engineer",
    friends: ["Shelby", "Court"],
    sayName() {
        console.log(this.name);
    }
};
let person1 = new Person();
let person2 = new Person();
person1.friends.push("Van");
console.log(person1.friends); // "Shelby,Court,Van"
console.log(person2.friends); // "Shelby,Court,Van"
console.log(person1.friends === person2.friends); // true
```

### 5.3 继承

> 继承是面向对象编程中讨论最多的话题。很多面向对象语言都支持两种继承：接口继承和实现继承。前者只继承方法签名，后者继承实际的方法。接口继承在ECMAScript 中是不可能的，因为函数没有签名。实现继承是ECMAScript 唯一支持的继承方式，而这主要是通过原型链实现的。

#### 5.3.1 原型链

```js
//ECMA-262 把原型链定义为ECMAScript 的主要继承方式
//其基本思想就是通过原型继承多个引用类型的属性和方法


//1.默认原型
//默认情况下，所有引用类型都继承自Object

//2.原型与继承关系
//instanceof操作符
//isPrototypeOf()

//3.关于方法
//子类有时候需要覆盖父类的方法，或者增加父类没有的方法。为此，这些方法必须在原型赋值之后再添加到原型上
//以对象字面量方式创建原型方法会破坏之前的原型链，因为这相当于重写了原型链

//4.原型链问题
//主要问题出现在原型中包含引用值的时候
//原型中包含的引用值会在所有实例间共享
function SuperType() {
	this.colors = ["red", "blue", "green"];
}
function SubType() {}
// 继承SuperType
SubType.prototype = new SuperType();
let instance1 = new SubType();
instance1.colors.push("black");
console.log(instance1.colors); // "red,blue,green,black"
let instance2 = new SubType();
console.log(instance2.colors); // "red,blue,green,black"

//原型链的第二个问题是，子类型在实例化时不能给父类型的构造函数传参
//无法在不影响所有对象实例的情况下把参数传进父类的构造函数
```

#### 5.3.2 盗用构造函数（对象伪装/经典继承）

```js
//在子类构造函数中调用父类构造函数,解决原型包含引用值导致的继承问题
//使用apply()和call()方法以新创建的对象为上下文执行构造函数
function SuperType() {
	this.colors = ["red", "blue", "green"];
}
function SubType() {
	// 继承SuperType
	SuperType.call(this);
}
let instance1 = new SubType();
instance1.colors.push("black");
console.log(instance1.colors); // "red,blue,green,black"
let instance2 = new SubType();
console.log(instance2.colors); // "red,blue,green"

//1.传递参数
function SuperType(name){
	this.name = name;
}
function SubType() {
	// 继承SuperType 并传参
	SuperType.call(this, "Nicholas");
	// 实例属性
	this.age = 29;
}
let instance = new SubType();
console.log(instance.name); // "Nicholas";
console.log(instance.age); // 29

//2.盗用构造函数的问题
//盗用构造函数的主要缺点，也是使用构造函数模式自定义类型的问题
//必须在构造函数中定义方法，因此函数不能重用
//子类也不能访问父类原型上定义的方法,所有类型只能使用构造函数模式
```

#### 5.3.3 组合继承(伪经典继承)

```js
//基本思路：使用原型链继承原型上的属性和方法，而通过盗用构造函数继承实例属性
//组合继承弥补了原型链和盗用构造函数的不足，是JavaScript 中使用最多的继承模式。而且组合继承也保留了instanceof 操作符和isPrototypeOf()方法识别合成对象的能力。
function SuperType(name){
    this.name = name;
    this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function() {
	console.log(this.name);
};
function SubType(name, age){
    // 继承属性
    SuperType.call(this, name);
    this.age = age;
}
// 继承方法
SubType.prototype = new SuperType();
SubType.prototype.sayAge = function() {
	console.log(this.age);
};
let instance1 = new SubType("Nicholas", 29);
instance1.colors.push("black");
console.log(instance1.colors); // "red,blue,green,black"
instance1.sayName(); // "Nicholas";
instance1.sayAge(); // 29
let instance2 = new SubType("Greg", 27);
console.log(instance2.colors); // "red,blue,green"
instance2.sayName(); // "Greg";
instance2.sayAge(); // 27
```

#### 5.3.4 原型式继承

```js
//原型式继承非常适合不需要单独创建构造函数，但仍然需要在对象间共享信息的场合。但要记住，属性中包含的引用值始终会在相关对象间共享，跟使用原型模式是一样的。
//原型式继承适用于这种情况：你有一个对象，想在它的基础上再创建一个新对象。你需要把这个对象先传给object()，然后再对返回的对象进行适当修改
function object(o) {
    function F() {}
    F.prototype = o;
    return new F();
}
//ECMAScript 5 通过增加Object.create()方法将原型式继承的概念规范化了。这个方法接收两个参数：作为新对象原型的对象，以及给新对象定义额外属性的对象（第二个可选）。在只有一个参数时，Object.create()与这里的object()方法效果相同：
let person = {
    name: "Nicholas",
    friends: ["Shelby", "Court", "Van"]
};
let anotherPerson = Object.create(person);
anotherPerson.name = "Greg";
anotherPerson.friends.push("Rob");
let yetAnotherPerson = Object.create(person);
yetAnotherPerson.name = "Linda";
yetAnotherPerson.friends.push("Barbie");
console.log(person.friends); // "Shelby,Court,Van,Rob,Barbie"
```

#### 5.3.5 寄生式继承

```js
//寄生式继承背后的思路类似于寄生构造函数和工厂模式：创建一个实现继承的函数，以某种方式增强对象，然后返回这个对象。
//寄生式继承同样适合主要关注对象，而不在乎类型和构造函数的场景。object()函数不是寄生式继承所必需的，任何返回新对象的函数都可以在这里使用。
//通过寄生式继承给对象添加函数会导致函数难以重用，与构造函数模式类似。
function object(o) {
    function F() {}
    F.prototype = o;
    return new F();
}
function createAnother(original){
    let clone = object(original); // 通过调用函数创建一个新对象
    clone.sayHi = function() { // 以某种方式增强这个对象
        console.log("hi");
    };
	return clone; // 返回这个对象
}

let person = {
    name: "Nicholas",
    friends: ["Shelby", "Court", "Van"]
};
let anotherPerson = createAnother(person);
anotherPerson.sayHi(); // "hi"
```

#### 5.3.6 寄生式组合继承（引用类型继承的最佳模式）

```js
//组合继承其实也存在效率问题。最主要的效率问题就是父类构造函数始终会被调用两次：一次在是创建子类原型时调用，另一次是在子类构造函数中调用。
//寄生式组合继承通过盗用构造函数继承属性，但使用混合式原型链继承方法。
//使用寄生式继承来继承父类原型，然后将返回的新对象赋值给子类原型
function object(o) {
    function F() {}
    F.prototype = o;
    return new F();
}
function inheritPrototype(subType, superType) {
    // 创建父类的一个副本
    let prototype = object(superType.prototype); 
    // 解决由于重写原型导致默认constructor丢失的问题
    prototype.constructor = subType; 
    // 将新创建的对象赋值给子类的原型
    subType.prototype = prototype; 
}
//创建父类构造函数
function SuperType(name) {
    this.name = name;
    this.colors = ["red", "blue", "green"];
}
//增加父类原型的方法
SuperType.prototype.sayName = function() {
	console.log(this.name);
};
//子类的构造函数
function SubType(name, age) {
	SuperType.call(this, name);
    this.age = age;
}
inheritPrototype(SubType, SuperType);
SubType.prototype.sayAge = function() {
	console.log(this.age);
};
```

### 5.4 类

- 类（class）是ECMAScript 中新的基础性语法糖结构
- 实际上它背后使用的仍然是原型和构造函数的概念

#### 5.4.1 类定义

```js
//定义类也有两种主要方式：类声明和类表达式
// 类声明
class Person {}
// 类表达式
const Animal = class {};

//类定义无声明提升，在被求值前不能被引用
console.log(ClassExpression); // undefined
var ClassExpression = class {};
console.log(ClassExpression); // class {}

console.log(ClassDeclaration); // ReferenceError: ClassDeclaration is not defined
class ClassDeclaration {}
console.log(ClassDeclaration); // class ClassDeclaration {}

//函数受函数作用域限制，而类受块作用域限制
{
    function FunctionDeclaration() {}
    class ClassDeclaration {}
}
console.log(FunctionDeclaration); // FunctionDeclaration() {}
console.log(ClassDeclaration); // ReferenceError: ClassDeclaration is not defined
```

```js
//类的构成
//默认情况下，类定义中的代码都在严格模式下执行
//与函数构造函数一样，多数编程风格都建议类名的首字母要大写，以区别于通过它创建的实例
//在把类表达式赋值给变量后，可以通过name 属性取得类表达式的名称字符串。但不能在类表达式作用域外部访问这个标识符
let Person = class PersonName {
    identify() {
        console.log(Person.name, PersonName.name);
    }
}
let p = new Person();
p.identify(); // PersonName PersonName
console.log(Person.name); // PersonName
console.log(PersonName); // ReferenceError: PersonName is not defined
```

#### 5.4.2 类构造函数

- constructor 关键字用于在类定义块内部创建类的构造函数
- 方法名constructor 会告诉解释器在使用new 操作符创建类的新实例时，应该调用这个函数
- 构造函数的定义不是必需的，不定义构造函数相当于将构造函数定义为空函数

**实例化**

```js
//使用new 操作符实例化Person 的操作等于使用new 调用其构造函数
//使用new 调用类的构造函数会执行如下操作。
//(1) 在内存中创建一个新对象。
//(2) 这个新对象内部的[[Prototype]]指针被赋值为构造函数的prototype 属性。
//(3) 构造函数内部的this 被赋值为这个新对象（即this 指向新对象）。
//(4) 执行构造函数内部的代码（给新对象添加属性）。
//(5) 如果构造函数返回非空对象，则返回该对象；否则，返回刚创建的新对象。
class Person {
    constructor() {
    	console.log('person ctor');
    }
}
let p = new Person(); // person ctor

class Vegetable {
    constructor() {
    	this.color = 'orange';
    }
}
let v = new Vegetable();
console.log(v.color); // orange
--------------------------------------------------
//类实例化时传入的参数会用作构造函数的参数。
class Person {
    constructor(name) {
        console.log(arguments.length);
        this.name = name || null;
    }
}
let p3 = new Person('Jake'); // 1
console.log(p3.name); // Jake
-----------------------------------------------
//类构造函数会在执行之后返回this 对象
//构造函数返回的对象会被用作实例化的对象，如果没有什么引用新创建的this 对象，那么这个对象会被销毁
//如果返回的不是this 对象，而是其他对象，那么这个对象不会通过instanceof 操作符检测出跟类有关联,因为这个对象的原型指针并没有被修改
class Person {
    constructor(override) {
        this.foo = 'foo';
        if (override) {
            return {
            	bar: 'bar'
            };
        }
    }
}
let p1 = new Person(),
p2 = new Person(true);
console.log(p1); // Person{ foo: 'foo' }
console.log(p1 instanceof Person); // true
console.log(p2); // { bar: 'bar' }
console.log(p2 instanceof Person); // false
----------------------------------------------
//类构造函数与构造函数的主要区别是，调用类构造函数必须使用new 操作符
//普通构造函数如果不使用new 调用，那么就会以全局的this（通常是window）作为内部对象。调用类构造函数时如果忘了使用new 则会抛出错误

```

**把类当成特殊函数**

```js
//ECMAScript 中没有正式的类这个类型。
//ECMAScript 类就是一种特殊函数。
class Person {}
console.log(Person); // class Person {}
console.log(typeof Person); // function
-----------------------------------------------
//类标识符有prototype 属性，而这个原型也有一个constructor 属性指向类自身
class Person{}
console.log(Person.prototype); // { constructor: f() }
console.log(Person === Person.prototype.constructor); // true
--------------------------------------------------
//与普通构造函数一样，可以使用instanceof 操作符检查构造函数原型是否存在于实例的原型链中
class Person {}
let p = new Person();
console.log(p instanceof Person); // true
-----------------------------------------------
//在类的上下文中，类本身在使用new 调用时就会被当成构造函数。
//类中定义的constructor 方法不会被当成构造函数
class Person {}
let p1 = new Person();
console.log(p1.constructor === Person); // true
console.log(p1 instanceof Person); // true
console.log(p1 instanceof Person.constructor); // false
//如果在创建实例时直接将类构造函数当成普通构造函数来使用，那么instanceof 操作符的返回值会反转：
let p2 = new Person.constructor();
console.log(p2.constructor === Person); // false
console.log(p2 instanceof Person); // false
console.log(p2 instanceof Person.constructor); // true
--------------------------------------------------
//类是JavaScript 的一等公民，因此可以像其他对象或函数引用一样把类作为参数传递
// 类可以像函数一样在任何地方定义，比如在数组中
let classList = [
    class {
        constructor(id) {
            this.id_ = id;
            console.log(`instance ${this.id_}`);
        }
    }
];
function createInstance(classDefinition, id) {
	return new classDefinition(id);
}
let foo = createInstance(classList[0], 3141); // instance 3141
------------------------------------------
//与立即调用函数表达式相似，类也可以立即实例化
let p = new class Foo {
    constructor(x) {
		console.log(x);
	}
}('bar'); // bar
console.log(p); // Foo {}
```

#### 5.4.3 实例、原型和类成员

> 类的语法可以非常方便地定义应该存在于实例上的成员、应该存在于原型上的成员，以及应该存在于类本身的成员。

**实例成员**

- 每次通过new 调用类标识符时，都会执行类构造函数，在这个函数内部，可以为新创建的实例（this）添加“自有”属性
- 每个实例都对应一个唯一的成员对象，这意味着所有成员都不会在原型上共享

```js
class Person {
    constructor() {
        // 这个例子先使用对象包装类型定义一个字符串
        // 为的是在下面测试两个对象的相等性
        this.name = new String('Jack');
        this.sayName = () => console.log(this.name);
        this.nicknames = ['Jake', 'J-Dog']
    }
}
let p1 = new Person(),
p2 = new Person();
p1.sayName(); // Jack
p2.sayName(); // Jack
console.log(p1.name === p2.name); // false
console.log(p1.sayName === p2.sayName); // false
console.log(p1.nicknames === p2.nicknames); // false
p1.name = p1.nicknames[0];
p2.name = p2.nicknames[1];
p1.sayName(); // Jake
p2.sayName(); // J-Dog	
```

**原型方法与访问器**

- 为了在实例间共享方法，类定义语法把在类块中定义的方法作为原型方法

```js
class Person {
    constructor() {
        // 添加到this 的所有内容都会存在于不同的实例上
        this.locate = () => console.log('instance');
    }
    // 在类块中定义的所有内容都会定义在类的原型上
    locate() {
    	console.log('prototype');
    }
}
let p = new Person();
p.locate(); // instance
Person.prototype.locate(); // prototype	
```

- 类定义也支持获取和设置访问器。

```js
class Person {
    set name(newName) {
    	this.name_ = newName;
    }
    get name() {
    	return this.name_;
    }
}
let p = new Person();
p.name = 'Jake';
console.log(p.name); // Jake
```

**静态类方法**

- 提供给函数使用的方法和属性,就称之为**静态成员**
- 静态方法是使用 static 关键字修饰的方法，又叫类方法，属于类的，但不属于对象，在实例化对象之前可以通过 **类名.方法名** 调用静态方法。
- 静态方法不能在对象上调用，只能在类中调用。
- 静态类成员在类定义中使用static 关键字作为前缀。在静态成员中，this 引用类自身。

```js
class Person {
	constructor() {
    // 添加到this 的所有内容都会存在于不同的实例上
    	this.locate = () => console.log('instance', this);
    }
    // 定义在类的原型对象上
    locate() {
    	console.log('prototype', this);
    }
    // 定义在类本身上
    static locate() {
    	console.log('class', this);
    }
}
let p = new Person();
p.locate(); // instance, Person {}
Person.prototype.locate(); // prototype, {constructor: ... }
Person.locate(); // class, class Person {}
```

**非函数原型和类成员**

- 虽然类定义并不显式支持在原型或类上添加成员数据，但在类定义外部，可以手动添加：

```js
class Person {
    sayName() {
    	console.log(`${Person.greeting} ${this.name}`);
    }
}
// 在类上定义数据成员
Person.greeting = 'My name is';
// 在原型上定义数据成员
Person.prototype.name = 'Jake';
let p = new Person();
p.sayName(); // My name is Jake
```

- **注意** 类定义中之所以没有显式支持添加数据成员，是因为在共享目标（原型和类）上添加可变（可修改）数据成员是一种反模式。一般来说，对象实例应该独自拥有通过this引用的数据。

**迭代器与生成器方法**[...]

- 类定义语法支持在原型和类本身上定义生成器方法

```js
```

#### **5.4.4 继承**

> ECMAScript 6 新增特性中最出色的一个就是原生支持了类继承机制。虽然类继承使用的是新语法，但背后依旧使用的是原型链。

**继承基础**

- ES6 类支持单继承。使用extends 关键字，就可以继承任何拥有[[Construct]]和原型的对象。
- 这意味着不仅可以继承一个类，也可以继承普通的构造函数（保持向后兼容）
- 派生类都会通过原型链访问到类和原型上定义的方法。
- **注意** extends 关键字也可以在类表达式中使用，因此let Bar = class extends Foo {}是有效的语法。

```js
class Vehicle {}
// 继承类
class Bus extends Vehicle {}
let b = new Bus();
console.log(b instanceof Bus); // true
console.log(b instanceof Vehicle); // true

function Person() {}
// 继承普通构造函数
class Engineer extends Person {}
let e = new Engineer();
console.log(e instanceof Engineer); // true
console.log(e instanceof Person); // true
```

**构造函数、HomeObject 和super()**

- 派生类的方法可以通过super 关键字引用它们的原型。这个关键字只能在派生类中使用，而且仅限于**类构造函数、实例方法和静态方法内部**。
- 在类构造函数中使用super 可以调用父类构造函数。
- 注意 ES6 给类构造函数和静态方法添加了内部特性`[[HomeObject]]`，这个特性是一个指针，指向定义该方法的对象。这个指针是自动赋值的，而且只能在JavaScript 引擎内部访问。super 始终会定义为`[[HomeObject]]`的原型。

```js
class Vehicle {
    constructor() {
        this.hasEngine = true;
    }
}
class Bus extends Vehicle {
    constructor() {
        // 不要在调用super()之前引用this，否则会抛出ReferenceError
        super(); // 相当于super.constructor()
        console.log(this instanceof Vehicle); // true
        console.log(this); // Bus { hasEngine: true }
    }
}
new Bus();

//super 只能在派生类构造函数和静态方法中使用。
class Vehicle {
    constructor() {
        super();
        // SyntaxError: 'super' keyword unexpected
    }
}

//不能单独引用super 关键字，要么用它调用构造函数，要么用它引用静态方法。
class Vehicle {}
class Bus extends Vehicle {
    constructor() {
        console.log(super);
        // SyntaxError: 'super' keyword unexpected here
    }
}

//调用super()会调用父类构造函数，并将返回的实例赋值给this。
class Vehicle {}
class Bus extends Vehicle {
    constructor() {
        super();
        console.log(this instanceof Vehicle);
    }
}
new Bus(); // true

//super()的行为如同调用构造函数，如果需要给父类构造函数传参，则需要手动传入。
class Vehicle {
    constructor(licensePlate) {
    	this.licensePlate = licensePlate;
    }
}
class Bus extends Vehicle {
    constructor(licensePlate) {
    	super(licensePlate);
    }
}
console.log(new Bus('1337H4X')); // Bus { licensePlate: '1337H4X' }

//如果没有定义类构造函数，在实例化派生类时会调用super()，而且会传入所有传给派生类的参数
class Vehicle {
    constructor(licensePlate) {
    	this.licensePlate = licensePlate;
    }
}
class Bus extends Vehicle {}
console.log(new Bus('1337H4X')); // Bus { licensePlate: '1337H4X' }

//在类构造函数中，不能在调用super()之前引用this。
class Vehicle {}
class Bus extends Vehicle {
    constructor() {
    	console.log(this);
    }
}
new Bus();
// ReferenceError: Must call super constructor in derived class
// before accessing 'this' or returning from derived constructor

//如果在派生类中显式定义了构造函数，则要么必须在其中调用super()，要么必须在其中返回一个对象。
class Vehicle {}
class Car extends Vehicle {}
class Bus extends Vehicle {
    constructor() {
    	super();
	}
}
class Van extends Vehicle {
    constructor() {
    	return {};
    }
}
console.log(new Car()); // Car {}
console.log(new Bus()); // Bus {}
console.log(new Van()); // {}
```

**抽象基类**

- 有时候可能需要定义这样一个类，它可供其他类继承，但本身不会被实例化。
- 通过在实例化时检测new.target 是不是抽象基类，可以阻止对抽象基类的实例化

```js
// 抽象基类
class Vehicle {
    constructor() {
        console.log(new.target);
        if (new.target === Vehicle) {
    		throw new Error('Vehicle cannot be directly instantiated');
        }
	}
}
// 派生类
class Bus extends Vehicle {}
new Bus(); // class Bus {}
new Vehicle(); // class Vehicle {}
// Error: Vehicle cannot be directly instantiated
```

- 通过在抽象基类构造函数中进行检查，可以要求派生类必须定义某个方法

```js
// 抽象基类
class Vehicle {
    constructor() {
        if (new.target === Vehicle) {
            throw new Error('Vehicle cannot be directly instantiated');
        }
        if (!this.foo) {
            throw new Error('Inheriting class must define foo()');
        }
        console.log('success!');
	}
}
// 派生类
class Bus extends Vehicle {
	foo() {}
}
// 派生类
class Van extends Vehicle {}
new Bus(); // success!
new Van(); // Error: Inheriting class must define foo()
```

**继承内置类型**

- ES6 类为继承内置引用类型提供了顺畅的机制，开发者可以方便地扩展内置类型
- 有些内置类型的方法会返回新实例。默认情况下，返回实例的类型与原始实例的类型是一致的
- 如果想覆盖这个默认行为，则可以覆盖Symbol.species 访问器，这个访问器决定在创建返回的实例时使用的类

**类混入**

- ES6 没有显式支持多类继承，但通过现有特性可以轻松地模拟这种行为。
- **注意** Object.assign()方法是为了混入对象行为而设计的。只有在需要混入类的行为时才有必要自己实现混入表达式。如果只是需要混入多个对象的属性，那么使用Object.assign()就可以了。

```js
class Vehicle {}
function getParentClass() {
    console.log('evaluated expression');
    return Vehicle;
}
class Bus extends getParentClass() {}
// 可求值的表达式
```

- **注意** 很多JavaScript 框架（特别是React）已经抛弃混入模式，转向了组合模式（把方法提取到独立的类和辅助对象中，然后把它们组合起来，但不使用继承）。这反映了那个众所周知的软件设计原则：“组合胜过继承（composition over inheritance）。”这个设计原则被很多人遵循，在代码设计中能提供极大的灵活性。



## 6 函数

### 6.1 箭头函数

```js
(...)=>{...}

//只有一个参数可以省略括号
x => {...}
//只包含一条语句，可以省略括号和return
(...) => x
//如果返回值是对象类型，因为对象用{}，在语法糖之后会被识别为函数的{}，因此不需要用小括号包围，防止歧义
(...) => ({key:value})
```

- ECMAScript 6 新增了使用胖箭头（=>）语法定义函数表达式的能力。
- 箭头函数不能使用arguments、super 和new.target，也不能用作构造函数。
- 箭头函数也没有prototype 属性。
- 在箭头函数中，this 引用的是定义箭头函数的上下文，是因为箭头函数中的this 会保留定义该函数时的上下文

### 6.2 函数名

- 因为函数名就是指向函数的指针，所以它们跟其他包含对象指针的变量具有相同的行为。这意味着一个函数可以有多个名称
- ECMAScript 6 的所有函数对象都会暴露一个只读的name 属性，其中包含关于函数的信息。多数情况下，这个属性中保存的就是一个函数标识符，或者说是一个字符串化的变量名。即使函数没有名称，也会如实显示成空字符串。如果它是使用Function 构造函数创建的，则会标识成"anonymous"

### 6.3 理解参数

- ECMAScript 函数既不关心传入的参数个数，也不关心这些参数的数据类型,
- ECMAScript 函数不存在验证命名参数的机制
- ECMAScript 函数的参数在内部表现为一个数组
- 在使用function 关键字定义（非箭头）函数时，可以在函数内部访问arguments 对象，从中取得传进来的每个参数值
- 如果函数是使用箭头语法定义的，那么传给函数的参数将不能使用arguments 关键字访问，而只能通过定义的命名参数访问。
- 虽然箭头函数中没有arguments 对象，但可以在包装函数中把它提供给箭头函数

### 6.4 关于重载

- ECMAScript 函数没有签名，因为参数是由包含零个或多个值的数组表示的。没有函数签名，自然也就没有重载。
- 可以通过检查参数的类型和数量，然后分别执行不同的逻辑来模拟函数重载。

### 6.5 默认参数

- 在ECMAScript5.1 及以前，实现默认参数的一种常用方式就是检测某个参数是否等于undefined，如果是则意味着没有传这个参数，那就给它赋一个值：
- ECMAScript 6 之后支持显式定义默认参数

```js
function fn(name='hello',...){...}
```

- 在使用默认参数时，arguments 对象的值不反映参数的默认值，只反映传给函数的参数。当然，跟ES5 严格模式一样，修改命名参数也不会影响arguments 对象，它始终以调用函数时传入的值为准：

```js
function makeKing(name = 'Henry') {
    name = 'Louis';
    return `King ${arguments[0]}`;
}
console.log(makeKing()); // 'King undefined'
console.log(makeKing('Louis')); // 'King Louis'
```

**默认参数作用域与暂时性死区**

- 参数是按顺序初始化的，后定义默认值的参数可以引用先定义的参数。

```js
function fn(name='hello',name2=name){...}
```

- 参数初始化顺序遵循“暂时性死区”规则，即前面定义的参数不能引用后面定义的。

```js
function fn(name=name2,name2='hello'){...}//报错
```

- 参数也存在于自己的作用域中，它们不能引用函数体的作用域

```js
function fn(name=name2){var name2 = 'hello'}//报错
```

### 6.6 参数的扩展与收集

#### 6.6.1 扩展参数

对可迭代对象应用 `扩展操作符` （...），并将其作为一个参数传入，可以将可迭代对象拆分，并将迭代返回的每个值单独传入。

```js
let values = [1, 2, 3, 4];
function getSum() {
    let sum = 0;
    for (let i = 0; i < arguments.length; ++i) {
    sum += arguments[i];
    }
    return sum;
}
console.log(getSum.apply(null, values)); //旧版写法 10
console.log(getSum(...values)); // ES6写法 10
```

#### 6.6.2 收集参数

在构思函数定义时，可以使用扩展操作符把不同长度的独立参数组合为一个**数组**。这有点类似arguments 对象的构造机制，只不过收集参数的结果会得到一个Array 实例。

```js
function getSum(...values) {
    // 顺序累加values 中的所有值
    // 初始值的总和为0
    return values.reduce((x, y) => x + y, 0);
}
console.log(getSum(1,2,3)); // 6`
```

### 6.7 函数声明与函数表达式

- JavaScript 引擎在任何代码执行之前，会先读取函数声明，并在执行上下文中生成函数定义。而函数表达式必须等到代码执行到它那一行，才会在执行上下文中生成函数定义。

- 除了函数什么时候真正有定义这个区别之外，这两种语法是等价的。

### 6.8 函数作为值

- 因为函数名在ECMAScript 中就是变量，所以函数可以用在任何可以使用变量的地方。
- 这意味着不仅可以把函数作为参数传给另一个函数，而且还可以在一个函数中返回另一个函数。

### 6.9 函数内部

在ECMAScript 5 中，函数内部存在两个特殊的对象：arguments 和this。ECMAScript 6 又新增了new.target 属性。

#### 6.9.1 arguments

- arguments 是一个类数组对象，包含调用函数时传入的所有参数
- 只有以function 关键字定义函数（相对于使用箭头语法创建函数）时才会有
- arguments 对象其实还有一个callee 属性，是一个指向arguments 对象所在函数的指针
- 在严格模式下访问arguments.callee 会报错

#### 6.9.2 this

- 另一个特殊的对象是this，它在标准函数和箭头函数中有不同的行为。
- 在标准函数中，this 引用的是把函数当成方法调用的上下文对象，这时候通常称其为this 值（在网页的全局上下文中调用函数时，this 指向windows）
- this 到底引用哪个对象必须到函数被调用时才能确定

```js
window.color = 'red';
let o = {
	color: 'blue'
};
function sayColor() {
	console.log(this.color);
}
sayColor(); // 'red'
o.sayColor = sayColor;
o.sayColor(); // 'blue'
```

- 在箭头函数中，this 引用的是定义箭头函数的上下文，是因为箭头函数中的this 会保留定义该函数时的上下文

```js
window.color = 'red';
let o = {
	color: 'blue'
};
let sayColor = () => console.log(this.color);
sayColor(); // 'red'
o.sayColor = sayColor;
o.sayColor(); // 'red' this 引用的都是window 对象，因为这个箭头函数是在window 上下文中定义的
```

- 函数名只是保存指针的变量。因此全局定义的sayColor()函数和o.sayColor()
  是同一个函数，只不过执行的上下文不同

#### 6.9.3 caller

- ECMAScript 5 也会给函数对象上添加一个属性：caller。
- 这个属性引用的是调用当前函数的函数，或者如果是在全局作用域中调用的则为null。

```js
function outer() {
	inner();
}
function inner() {
	console.log(inner.caller);
}
outer();//以上代码会显示outer()函数的源代码
```

- ECMAScript 5 也定义了arguments.caller，但在严格模式下访问它会报错，在非严格模式下则始终是undefined。
- 这是为了分清arguments.caller和函数的caller 而故意为之的。而作为对这门语言的安全防护，这些改动也让第三方代码无法检测同一上下文中运行的其他代码。
- 严格模式下还有一个限制，就是不能给函数的caller 属性赋值，否则会导致错误。

#### 6.9.4 new.target

- ECMAScript 中的函数始终可以作为构造函数实例化一个新对象，也可以作为普通函数被调用。
- ECMAScript 6 新增了检测函数是否使用new 关键字调用的new.target 属性。
- 如如果函数是正常调用的,则new.target 的值是undefined；如果是使用new 关键字调用的，则new.target 将引用被调用的构造函数。

```js
function King() {
    if (!new.target) {
        throw 'King must be instantiated using "new"'
    }
    console.log('King instantiated using "new"');
}
new King(); // King instantiated using "new"
King(); // Error: King must be instantiated using "new"
```

### 6.10 函数属性与方法

- ECMAScript 中的函数是对象，因此有属性和方法。每个函数都有两个属性：`length`和`prototype`
- `length `属性保存函数定义的命名参数的个数

```js
function sayName(name) {
	console.log(name);
}
function sum(num1, num2) {
	return num1 + num2;
}
function sayHi() {
	console.log("hi");
}
console.log(sayName.length); // 1
console.log(sum.length); // 2
console.log(sayHi.length); // 0
```

- prototype 是保存引用类型所有实例方法的地方，这意味着toString()、valueOf()等方法实际上都保存在prototype 上，进而由所有实例共享。
- 在ECMAScript 5中，prototype 属性是不可枚举的，因此使用for-in 循环不会返回这个属性。
- apply()方法接收两个参数：函数内this 的值和一个参数数组。第二个参数可以是Array 的实例，但也可以是arguments 对象

```js
//在这个例子中，callSum1()会调用sum()函数，将this 作为函数体内的this 值（这里等于window，因为是在全局作用域中调用的）传入，同时还传入了arguments 对象。callSum2()也会调用sum()函数，但会传入参数的数组。这两个函数都会执行并返回正确的结果。
function sum(num1, num2) {
	return num1 + num2;
}
function callSum1(num1, num2) {
	return sum.apply(this, arguments); // 传入arguments 对象
}
function callSum2(num1, num2) {
	return sum.apply(this, [num1, num2]); // 传入数组
}
console.log(callSum1(10, 10)); // 20
console.log(callSum2(10, 10)); // 20
```

- 在严格模式下，调用函数时如果没有指定上下文对象，则this 值不会指向window。除非使用apply()或call()把函数指定给一个对象，否则this 的值会变成undefined。
- call()方法与apply()的作用一样，只是传参的形式不同。第一个参数跟apply()一样，也是this值，而剩下的要传给被调用函数的参数则是逐个传递的。

```js
function sum(num1, num2) {
	return num1 + num2;
}
function callSum(num1, num2) {
	return sum.call(this, num1, num2);
}
console.log(callSum(10, 10)); // 20
```

- 使用call()或apply()的好处是可以将任意对象设置为任意函数的作用域，这样对象可以不用关心方法。

```js
window.color = 'red';
let o = {
	color: 'blue'
};
function sayColor() {
	console.log(this.color);
}
sayColor(); // red
sayColor.call(this); // red
sayColor.call(window); // red
sayColor.call(o); // blue 把函数的执行上下文即this 切换为对象o
```

- ECMAScript 5 出于同样的目的定义了一个新方法：bind()。bind()方法会创建一个新的函数实例，其this 值会被绑定到传给bind()的对象。

```js
window.color = 'red';
var o = {
	color: 'blue'
};
function sayColor() {
	console.log(this.color);
}
let objectSayColor = sayColor.bind(o);
objectSayColor(); // blue
```

- 对函数而言，继承的方法toLocaleString()和toString()始终返回函数的代码。返回代码的具体格式因浏览器而异。
- 继承的方法valueOf()返回函数本身。

### 6.11 函数表达式

- 定义函数有两种方式：函数声明和函数表达式

```js
//函数声明的关键特点是函数声明提升，即函数声明会在代码执行之前获得定义。这意味着函数声明可以出现在调用它的代码之后
function functionName(arg0, arg1, arg2) {...}

//函数表达式看起来就像一个普通的变量定义和赋值，即创建一个函数再把它赋值给一个变量functionName,需要先赋值再使用
//这样创建的函数叫作匿名函数
//未赋值给其他变量的匿名函数的name 属性是空字
符串
let functionName = function(arg0, arg1, arg2) {...};
```

### 6.12 递归

- 递归函数通常的形式是一个函数通过名称调用自己

```js
//递归阶乘
function factorial(num) {
    if (num <= 1) {
        return 1;
    } else {
	return num * factorial(num - 1);
	}
}
```

- 为了任意情况下（另存一个变量名，原变量名赋其他值，且无论是否在严格模式下都能运行），都能继续使用该函数，使用命名函数表达式（named function expression）

```js
const factorial = (function f(num) {
    if (num <= 1) {
    	return 1;
    } else {
    	return num * f(num - 1);
    }
});
```

### 10.13 尾调用优化【？】

- ECMAScript 6 规范新增了一项内存管理优化机制，让JavaScript 引擎在满足条件时可以重用栈帧
- 这项优化非常适合“尾调用”，即外部函数的返回值是一个内部函数的返回值

### 10.14 闭包

- 闭包指的是那些引用了另一个函数作用域中变量的函数，通常是在嵌套函数中实现的
- 函数执行时，每个执行上下文中都会有一个包含其中变量的对象。
- 全局上下文中的叫变量对象，它会在代码执行期间始终存在。
- 而函数局部上下文中的叫活动对象，只在函数执行期间存在。

```js
//在定义compare()函数时，就会为它创建作用域链，预装载全局变量对象，并保存在内部的[[Scope]]中。
function compare(value1, value2) {
    if (value1 < value2) {
    	return -1;
    } else if (value1 > value2) {
    	return 1;
    } else {
   		return 0;
    }
}
//在调用这个函数时，会创建相应的执行上下文，然后通过复制函数的[[Scope]]来创建其作用域链。
//接着会创建函数的活动对象（用作变量对象）并将其推入作用域链的前端
let result = compare(5, 10);
```

- 作用域链其实是一个包含指针的列表，每个指针分别指向一个变量对象，但物理上并不会包含相应的对象
- 只存储对自己有用的属性 , 最大程度节省内存
- 因为闭包会保留它们包含函数的作用域，所以比其他函数更占用内存。过度使用闭包可能导致内存过度占用，因此建议仅在十分必要时使用。V8 等优化的JavaScript 引擎会努力回收被闭包困住的内存，不过我们还是建议在使用闭包时要谨慎。

#### 6.14.1 this对象

- 如果内部函数没有使用箭头函数定义，则this 对象会在运行时绑定到执行函数的上下文; 如果在全局函数中调用，则this 在非严格模式下等于window，在严格模式下等于undefined; 如果作为某个对象的方法调用，则this 等于这个对象
- 箭头函数this指向定义时的上下文
- 严格模式下，在全局中调用函数，this指向undefined

```js
'use strict'
function fn() {
    console.log(this)
}
fn()//undefined
------------------------------
function fn() {
    console.log(this)
}
fn()//window
```

**注意**

```js
window.identity = 'The Window';
let object = {
    identity: 'My Object',
    getIdentityFunc() {
        return function() {
        	return this.identity;
    	};
    }
};
console.log(object.getIdentityFunc()()); // 'The Window'

//this 和arguments 都是不能直接在内部函数中访问的。如果想访问包含作用域中的arguments 对象，则同样需要将其引用先保存到闭包能访问的另一个变量中。

window.identity = 'The Window';
let object = {
    identity: 'My Object',
    getIdentityFunc() {
        let that = this;
        return function() {
        	return that.identity;
        };
    }
};
console.log(object.getIdentityFunc()()); // 'My Object'
```

#### 6.14.2 内存泄漏【？】

### 6.15 立即调用的函数表达式

- 立即调用的匿名函数又被称作立即调用的函数表达式（IIFE，Immediately Invoked Function Expression)，它类似于函数声明，但由于被包含在括号中，所以会被解释为函数表达式

```js
(function() {
// 块级作用域
})();
```

- 使用IIFE 可以模拟块级作用域，即在一个函数表达式内部声明变量，然后立即调用这个函数。ECMAScript 5 尚未支持块级作用域，使用IIFE模拟块级作用域是相当普遍的.
- 在ECMAScript 6 以后，IIFE 就没有那么必要了，因为块级作用域中的变量无须IIFE 就可以实现同样的隔离

### 6.16 私有变量

- 严格来讲，JavaScript 没有私有成员的概念，所有对象属性都公有的。
- 但是有私有变量的概念。任何定义在函数或块中的变量，都可以认为是私有的，因为在这个函数或块的外部无法访问其中的变量。私有变量包括函数参数、局部变量，以及函数内部定义的其他函数。
- 特权方法（privileged method）是能够访问函数私有变量（及私有函数）的公有方法。

```js
//在构造函数中实现特权方法
//这个模式是把所有私有变量和私有函数都定义在构造函数中
//然后，再创建一个能够访问这些私有成员的特权方法。
//定义在构造函数中的特权方法其实是一个闭包，它具有访问构造函数中定义的所有变量和函数的能力
function MyObject() {
	// 私有变量和私有函数
    let privateVariable = 10;
    function privateFunction() {
    	return false;
    }
    // 特权方法
    this.publicMethod = function() {
        privateVariable++;
        return privateFunction();
    };
}
```

#### 6.16.1 静态私有变量

- 特权方法也可以通过使用私有作用域定义私有变量和函数来实现
- 该模式下，私有变量和私有函数是由实例共享的
- 特权方法定义在原型上，所以同样是由实例共享的
- **注意** 使用闭包和私有变量会导致作用域链变长，作用域链越长，则查找变量所需的时间也越多。
- 创建静态私有变量可以利用原型更好地重用代码，只是每个实例没有了自己的私有变量。到底是把私有变量放在实例中，还是作为静态私有变量，都需要根据自己的需求来确定。

```js
(function() {
    // 私有变量和私有函数
    let privateVariable = 10;
    function privateFunction() {
    	return false;
    }
    // 构造函数
    //这里声明MyObject 并没有使
    MyObject = function() {};
    // 公有和特权方法用任何关键字,MyObject 变成了全局变量，可以在这个私有作用域外部被访问.在严格模式下给未声明的变量赋值会导致错误
    MyObject.prototype.publicMethod = function() {
    	privateVariable++;
    return privateFunction();
    };
})();	
```

#### 6.16.2 模块模式

- 单例对象（singleton）就是只有一个实例的对象。
- 按照惯例，JavaScript 是通过对象字面量来创建单例对象的

```js
let singleton = {
	name: value,
    method() {
		// 方法的代码
	}
};
```

- 模块模式是在单例对象基础上加以扩展，使其通过作用域链来关联私有变量和特权方法。

```js
//模块模式使用了匿名函数返回一个对象。
//在匿名函数内部，首先定义私有变量和私有函数。
//之后，创建一个要通过匿名函数返回的对象字面量。这个对象字面量中只包含可以公开访问的属性和方法。
let singleton = function() {
    // 私有变量和私有函数
    let privateVariable = 10;
    function privateFunction() {
    	return false;
	}
    // 特权/公有方法和属性
    return {
        publicProperty: true,
        publicMethod() {
            privateVariable++;
            return privateFunction();
        }
    };
}();
```

- 在模块模式中，单例对象作为一个模块，经过初始化可以包含某些私有的数据，而这些数据又可以通过其暴露的公共方法来访问。以这种方式创建的每个单例对象都是Object 的实例，因为最终单例都由一个对象字面量来表示。
- 单例对象通常是可以全局访问的

#### 6.16.3 模块增强模式

- 另一个利用模块模式的做法是在返回对象之前先对其进行增强。这适合单例对象需要是某个特定类型的实例，但又必须给它添加额外属性或方法的场景。

```js
let singleton = function() {
    // 私有变量和私有函数
    let privateVariable = 10;
    function privateFunction() {
    	return false;
	}
    // 创建对象
    let object = new CustomType();
    // 添加特权/公有属性和方法
    object.publicProperty = true;
    object.publicMethod = function() {
        privateVariable++;
        return privateFunction();
    };
    // 返回对象
    return object;
}();
```



## 7 期约与异步【...】



## 8 DOM

> 当网页被加载时，浏览器会创建页面的文档对象模型（Document Object Model）
>
> Document 对象是 HTML 文档的根节点。
>
> Document 对象使我们可以从脚本中对 HTML 页面中的所有元素进行访问。
>
> **提示：**Document 对象是 Window 对象的一部分，可通过 window.document 属性对其进行访问。

### 8.1 document对象

在 HTML DOM (Document Object Model) 中 , 每一个元素都是 **节点**:

- 文档是一个文档节点。
- 所有的HTML元素都是元素节点。
- 所有 HTML 属性都是属性节点。
- 文本插入到 HTML 元素是文本节点。are text nodes。
- 注释是注释节点。

HTML文档中可以使用以下属性和方法:

| 属性 / 方法                                                  | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [document.activeElement](https://www.runoob.com/jsref/prop-document-activeelement.html) | 返回当前获取焦点元素                                         |
| [document.addEventListener()](https://www.runoob.com/jsref/met-document-addeventlistener.html) | 向文档添加句柄                                               |
| [document.adoptNode(node)](https://www.runoob.com/jsref/met-document-adoptnode.html) | 从另外一个文档返回 adapded 节点到当前文档。                  |
| [document.anchors](https://www.runoob.com/jsref/coll-doc-anchors.html) | 返回对文档中所有 Anchor 对象的引用。                         |
| document.applets                                             | 返回对文档中所有 Applet 对象的引用。**注意:** HTML5 已不支持 <applet> 元素。 |
| [document.baseURI](https://www.runoob.com/jsref/prop-doc-baseuri.html) | 返回文档的绝对基础 URI                                       |
| [document.body](https://www.runoob.com/jsref/prop-doc-body.html) | 返回文档的**body**元素                                       |
| [document.close()](https://www.runoob.com/jsref/met-doc-close.html) | 关闭用 document.open() 方法打开的输出流，并显示选定的数据。  |
| [document.cookie](https://www.runoob.com/jsref/prop-doc-cookie.html) | 设置或返回与当前文档有关的所有 cookie。                      |
| [document.createAttribute()](https://www.runoob.com/jsref/met-document-createattribute.html) | 创建一个属性节点                                             |
| [document.createComment()](https://www.runoob.com/jsref/met-document-createcomment.html) | createComment() 方法可创建注释节点。                         |
| [document.createDocumentFragment()](https://www.runoob.com/jsref/met-document-createdocumentfragment.html) | 创建空的 DocumentFragment 对象，并返回此对象。               |
| [document.createElement()](https://www.runoob.com/jsref/met-document-createelement.html) | 创建元素节点。                                               |
| [document.createTextNode()](https://www.runoob.com/jsref/met-document-createtextnode.html) | 创建文本节点。                                               |
| [document.doctype](https://www.runoob.com/jsref/prop-document-doctype.html) | 返回与文档相关的文档类型声明 (DTD)。                         |
| [document.documentElement](https://www.runoob.com/jsref/prop-document-documentelement.html) | 返回文档的根节点 **Html**                                    |
| [document.documentMode](https://www.runoob.com/jsref/prop-doc-documentmode.html) | 返回用于通过浏览器渲染文档的模式                             |
| [document.documentURI](https://www.runoob.com/jsref/prop-document-documenturi.html) | 设置或返回文档的位置                                         |
| [document.domain](https://www.runoob.com/jsref/prop-doc-domain.html) | 返回当前文档的域名。                                         |
| document.domConfig                                           | **已废弃**。返回 normalizeDocument() 被调用时所使用的配置。  |
| [document.embeds](https://www.runoob.com/jsref/coll-doc-embeds.html) | 返回文档中所有嵌入的内容（embed）集合                        |
| [document.forms](https://www.runoob.com/jsref/coll-doc-forms.html) | 返回对文档中所有 Form 对象引用。                             |
| [document.getElementsByClassName()](https://www.runoob.com/jsref/met-document-getelementsbyclassname.html) | 返回文档中所有指定类名的元素集合，作为 NodeList 对象。       |
| [document.getElementById()](https://www.runoob.com/jsref/met-document-getelementbyid.html) | 返回对拥有指定 id 的第一个对象的引用。                       |
| [document.getElementsByName()](https://www.runoob.com/jsref/met-doc-getelementsbyname.html) | 返回带有指定名称的对象集合。                                 |
| [document.getElementsByTagName()](https://www.runoob.com/jsref/met-document-getelementsbytagname.html) | 返回带有指定标签名的对象集合。                               |
| document.head                                                | 返回文档的head元素                                           |
| [document.images](https://www.runoob.com/jsref/coll-doc-images.html) | 返回对文档中所有 Image 对象引用。                            |
| [document.implementation](https://www.runoob.com/jsref/prop-document-implementation.html) | 返回处理该文档的 DOMImplementation 对象。                    |
| [document.importNode()](https://www.runoob.com/jsref/met-document-importnode.html) | 把一个节点从另一个文档复制到该文档以便应用。                 |
| [document.inputEncoding](https://www.runoob.com/jsref/prop-document-inputencoding.html) | 返回用于文档的编码方式（在解析时）。                         |
| [document.lastModified](https://www.runoob.com/jsref/prop-doc-lastmodified.html) | 返回文档被最后修改的日期和时间。                             |
| [document.links](https://www.runoob.com/jsref/coll-doc-links.html) | 返回对文档中所有 Area 和 Link 对象引用。                     |
| [document.normalize()](https://www.runoob.com/jsref/met-document-normalize.html) | 删除空文本节点，并连接相邻节点                               |
| [document.normalizeDocument()](https://www.runoob.com/jsref/met-document-normalizedocument.html) | 删除空文本节点，并连接相邻节点的                             |
| [document.open()](https://www.runoob.com/jsref/met-doc-open.html) | 打开一个流，以收集来自任何 document.write() 或 document.writeln() 方法的输出。 |
| [document.querySelector()](https://www.runoob.com/jsref/met-document-queryselector.html) | 返回文档中匹配指定的CSS选择器的第一元素                      |
| [document.querySelectorAll()](https://www.runoob.com/jsref/met-document-queryselectorall.html) | document.querySelectorAll() 是 HTML5中引入的新方法，返回文档中匹配的CSS选择器的所有元素节点列表 |
| [document.readyState](https://www.runoob.com/jsref/prop-doc-readystate.html) | 返回文档状态 (载入中……)                                      |
| [document.referrer](https://www.runoob.com/jsref/prop-doc-referrer.html) | 返回载入当前文档的文档的 URL。                               |
| [document.removeEventListener()](https://www.runoob.com/jsref/met-document-removeeventlistener.html) | 移除文档中的事件句柄(由 addEventListener() 方法添加)         |
| [document.renameNode()](https://www.runoob.com/jsref/met-document-renamenode.html) | 重命名元素或者属性节点。                                     |
| [document.scripts](https://www.runoob.com/jsref/coll-doc-scripts.html) | 返回页面中所有脚本的集合。                                   |
| [document.strictErrorChecking](https://www.runoob.com/jsref/prop-document-stricterrorchecking.html) | 设置或返回是否强制进行错误检查。                             |
| [document.title](https://www.runoob.com/jsref/prop-doc-title.html) | 返回当前文档的标题。                                         |
| [document.URL](https://www.runoob.com/jsref/prop-doc-url.html) | 返回文档完整的URL                                            |
| [document.write()](https://www.runoob.com/jsref/met-doc-write.html) | 向文档写 HTML 表达式 或 JavaScript 代码。                    |
| [document.writeln()](https://www.runoob.com/jsref/met-doc-writeln.html) | 等同于 write() 方法，不同的是在每个表达式之后写一个换行符。  |

------

#### 警告 !!!

在 W3C DOM核心，文档对象 继承节点对象的所有属性和方法。

很多属性和方法在文档中是没有意义的。

**HTML 文档对象可以避免使用这些节点对象和属性：**

| 属性 / 方法              | 避免的原因                  |
| :----------------------- | :-------------------------- |
| document.attributes      | 文档没有该属性              |
| document.hasAttributes() | 文档没有该属性              |
| document.nextSibling     | 文档没有下一节点            |
| document.nodeName        | 这个通常是 #document        |
| document.nodeType        | 这个通常是 9(DOCUMENT_NODE) |
| document.nodeValue       | 文档没有一个节点值          |
| document.ownerDocument   | 文档没有主文档              |
| document.ownerElement    | 文档没有自己的节点          |
| document.parentNode      | 文档没有父节点              |
| document.previousSibling | 文档没有兄弟节点            |
| document.textContent     | 文档没有文本节点            |

### 8.2 元素对象

- 在 HTML DOM 中, **元素对象**代表着一个 HTML 元素。
- 元素对象 的 **子节点**可以是, 可以是元素节点，文本节点，注释节点。
- **NodeList 对象** 代表了节点列表，类似于 HTML元素的子节点集合。
- 元素可以有属性。属性属于属性节点

**属性和方法**

| 属性 / 方法                                                  | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [*element*.accessKey](https://www.runoob.com/jsref/prop-html-accesskey.html) | 设置或返回accesskey一个元素                                  |
| [*element*.addEventListener()](https://www.runoob.com/jsref/met-element-addeventlistener.html) | 向指定元素添加事件句柄                                       |
| [*element*.appendChild()](https://www.runoob.com/jsref/met-node-appendchild.html) | 为元素添加一个新的子元素                                     |
| [*element*.attributes](https://www.runoob.com/jsref/prop-node-attributes.html) | 返回一个元素的属性数组                                       |
| [*element*.childNodes](https://www.runoob.com/jsref/prop-node-childnodes.html) | 返回元素的一个子节点的数组                                   |
| [*element*.children](https://www.runoob.com/jsref/prop-element-children.html) | 返回元素的子元素的集合                                       |
| [*element*.classList](https://www.runoob.com/jsref/prop-element-classList.html) | 返回元素的类名，作为 DOMTokenList 对象。                     |
| [*element*.className](https://www.runoob.com/jsref/prop-html-classname.html) | 设置或返回元素的class属性                                    |
| [*element*.clientTop](https://www.runoob.com/jsref/prop-element-clienttop.html) | 表示一个元素的顶部边框的宽度，以像素表示。                   |
| [*element*.clientLeft](https://www.runoob.com/jsref/prop-element-clientleft.html) | 表示一个元素的左边框的宽度，以像素表示。                     |
| [*element*.clientHeight](https://www.runoob.com/jsref/prop-element-clientheight.html) | 在页面上返回内容的可视高度（高度包含内边距（padding），不包含边框（border），外边距（margin）和滚动条） |
| [*element*.clientWidth](https://www.runoob.com/jsref/prop-element-clientwidth.html) | 在页面上返回内容的可视宽度（宽度包含内边距（padding），不包含边框（border），外边距（margin）和滚动条） |
| [*element*.cloneNode()](https://www.runoob.com/jsref/met-node-clonenode.html) | 克隆某个元素                                                 |
| [*element*.compareDocumentPosition()](https://www.runoob.com/jsref/met-node-comparedocumentposition.html) | 比较两个元素的文档位置。                                     |
| [*element*.contentEditable](https://www.runoob.com/jsref/prop-html-contenteditable.html) | 设置或返回元素的内容是否可编辑                               |
| [*element*.dir](https://www.runoob.com/jsref/prop-html-dir.html) | 设置或返回一个元素中的文本方向                               |
| [*element*.firstElementChild](https://www.runoob.com/jsref/prop-element-firstelementchild.html) | 返回元素的第一个子元素                                       |
| [*element*.firstChild](https://www.runoob.com/jsref/prop-node-firstchild.html) | 返回元素的第一个子节点                                       |
| [*element*.focus()](https://www.runoob.com/jsref/met-html-focus.html) | 设置文档或元素获取焦点                                       |
| [*element*.getAttribute()](https://www.runoob.com/jsref/met-element-getattribute.html) | 返回指定元素的属性值                                         |
| [*element*.getAttributeNode()](https://www.runoob.com/jsref/met-element-getattributenode.html) | 返回指定属性节点                                             |
| [*element*.getElementsByTagName()](https://www.runoob.com/jsref/met-element-getelementsbytagname.html) | 返回指定标签名的所有子元素集合。                             |
| [*element*. getElementsByClassName()](https://www.runoob.com/jsref/met-element-getelementsbyclassname.html) | 返回文档中所有指定类名的元素集合，作为 NodeList 对象。       |
| *element*.getFeature()                                       | 返回指定特征的执行APIs对象。                                 |
| *element*.getUserData()                                      | 返回一个元素中关联键值的对象。                               |
| [*element*.hasAttribute()](https://www.runoob.com/jsref/met-element-hasattribute.html) | 如果元素中存在指定的属性返回 true，否则返回false。           |
| [*element*.hasAttributes()](https://www.runoob.com/jsref/met-node-hasattributes.html) | 如果元素有任何属性返回true，否则返回false。                  |
| [*element*.hasChildNodes()](https://www.runoob.com/jsref/met-node-haschildnodes.html) | 返回一个元素是否具有任何子元素                               |
| [*element*.hasFocus()](https://www.runoob.com/jsref/met-document-hasfocus.html) | 返回布尔值，检测文档或元素是否获取焦点                       |
| [*element*.id](https://www.runoob.com/jsref/prop-html-id.html) | 设置或者返回元素的 id。                                      |
| [*element*.innerHTML](https://www.runoob.com/jsref/prop-html-innerhtml.html) | 设置或者返回元素的内容。                                     |
| [*element*.insertBefore()](https://www.runoob.com/jsref/met-node-insertbefore.html) | 现有的子元素之前插入一个新的子元素                           |
| [*element*.isContentEditable](https://www.runoob.com/jsref/prop-html-iscontenteditable.html) | 如果元素内容可编辑返回 true，否则返回false                   |
| [*element*.isDefaultNamespace()](https://www.runoob.com/jsref/met-node-isdefaultnamespace.html) | 如果指定了namespaceURI 返回 true，否则返回 false。           |
| [*element*.isEqualNode()](https://www.runoob.com/jsref/met-node-isequalnode.html) | 检查两个元素是否相等                                         |
| [*element*.isSameNode()](https://www.runoob.com/jsref/met-node-issamenode.html) | 检查两个元素所有有相同节点。                                 |
| [*element*.isSupported()](https://www.runoob.com/jsref/met-node-issupported.html) | 如果在元素中支持指定特征返回 true。                          |
| [*element*.lang](https://www.runoob.com/jsref/prop-html-lang.html) | 设置或者返回一个元素的语言。                                 |
| [*element*.lastChild](https://www.runoob.com/jsref/prop-node-lastchild.html) | 返回最后一个子节点                                           |
| [*element*.lastElementChild](https://www.runoob.com/jsref/prop-element-lastelementchild.html) | 返回指定元素的最后一个子元素                                 |
| [*element*.matches()](https://www.runoob.com/jsref/met-element-matches.html) | 如果元素匹配指定的 CSS 选择器，matches() 方法就返回 true，否则返回 false。 |
| [*element*.namespaceURI](https://www.runoob.com/jsref/prop-node-namespaceuri.html) | 返回命名空间的 URI。                                         |
| [*element*.nextSibling](https://www.runoob.com/jsref/prop-node-nextsibling.html) | 返回该元素紧跟的一个节点                                     |
|                                                              |                                                              |
| [*element*.nextElementSibling](https://www.runoob.com/jsref/prop-element-nextelementsibling.html) | 返回指定元素之后的下一个兄弟元素（相同节点树层中的下一个元素节点）。 |
| [*element*.nodeName](https://www.runoob.com/jsref/prop-node-nodename.html) | 返回元素的标记名（大写）                                     |
| [*element*.nodeType](https://www.runoob.com/jsref/prop-node-nodetype.html) | 返回元素的节点类型                                           |
| [*element*.nodeValue](https://www.runoob.com/jsref/prop-node-nodevalue.html) | 返回元素的节点值                                             |
| [*element*.normalize()](https://www.runoob.com/jsref/met-node-normalize.html) | 使得此成为一个"normal"的形式，其中只有结构（如元素，注释，处理指令，CDATA节和实体引用）隔开Text节点，即元素（包括属性）下面的所有文本节点，既没有相邻的文本节点也没有空的文本节点 |
| [*element*.offsetHeight](https://www.runoob.com/jsref/prop-element-offsetheight.html) | 返回任何一个元素的高度包括边框（border）和内边距（padding），但不包含外边距（margin） |
| [*element*.offsetWidth](https://www.runoob.com/jsref/prop-element-offsetwidth.html) | 返回元素的宽度，包括边框（border）和内边距（padding），但不包含外边距（margin） |
| [*element*.offsetLeft](https://www.runoob.com/jsref/prop-element-offsetleft.html) | 返回当前元素的相对水平偏移位置的偏移容器                     |
| [*element*.offsetParent](https://www.runoob.com/jsref/prop-element-offsetparent.html) | 返回元素的偏移容器                                           |
| [*element*.offsetTop](https://www.runoob.com/jsref/prop-element-offsettop.html) | 返回当前元素的相对垂直偏移位置的偏移容器                     |
| [*element*.ownerDocument](https://www.runoob.com/jsref/prop-node-ownerdocument.html) | 返回元素的根元素（文档对象）                                 |
| [*element*.parentNode](https://www.runoob.com/jsref/prop-node-parentnode.html) | 返回元素的父节点                                             |
| [*element*.previousSibling](https://www.runoob.com/jsref/prop-node-previoussibling.html) | 返回某个元素紧接之前元素                                     |
| [*element*.previousElementSibling](https://www.runoob.com/jsref/prop-element-previouselementsibling.html) | 返回指定元素的前一个兄弟元素（相同节点树层中的前一个元素节点）。 |
| [*element*.querySelector()](https://www.runoob.com/jsref/met-element-queryselector.html) | 返回匹配指定 CSS 选择器元素的第一个子元素                    |
| [document.querySelectorAll()](https://www.runoob.com/jsref/met-document-queryselectorall.html) | 返回匹配指定 CSS 选择器元素的所有子元素节点列表              |
| [*element*.removeAttribute()](https://www.runoob.com/jsref/met-element-removeattribute.html) | 从元素中删除指定的属性                                       |
| [*element*.removeAttributeNode()](https://www.runoob.com/jsref/met-element-removeattributenode.html) | 删除指定属性节点并返回移除后的节点。                         |
| [*element*.removeChild()](https://www.runoob.com/jsref/met-node-removechild.html) | 删除一个子元素                                               |
| [*element*.removeEventListener()](https://www.runoob.com/jsref/met-element-removeeventlistener.html) | 移除由 addEventListener() 方法添加的事件句柄                 |
| [*element*.replaceChild()](https://www.runoob.com/jsref/met-node-replacechild.html) | 替换一个子元素                                               |
| [*element*.scrollHeight](https://www.runoob.com/jsref/prop-element-scrollheight.html) | 返回整个元素的高度（包括带滚动条的隐蔽的地方）               |
| *element*.scrollLeft                                         | 返回当前视图中的实际元素的左边缘和左边缘之间的距离           |
| *element*.scrollTop                                          | 返回当前视图中的实际元素的顶部边缘和顶部边缘之间的距离       |
| *element*.scrollWidth                                        | 返回元素的整个宽度（包括带滚动条的隐蔽的地方）               |
| [*element*.setAttribute()](https://www.runoob.com/jsref/met-element-setattribute.html) | 设置或者改变指定属性并指定值。                               |
| [*element*.setAttributeNode()](https://www.runoob.com/jsref/met-element-setattributenode.html) | 设置或者改变指定属性节点。                                   |
| *element*.setIdAttribute()                                   |                                                              |
| *element*.setIdAttributeNode()                               |                                                              |
| *element*.setUserData()                                      | 在元素中为指定键值关联对象。                                 |
| *element*.style                                              | 设置或返回元素的样式属性                                     |
| [*element*.tabIndex](https://www.runoob.com/jsref/prop-html-tabindex.html) | 设置或返回元素的标签顺序。                                   |
| [*element*.tagName](https://www.runoob.com/jsref/prop-element-tagname.html) | 作为一个字符串返回某个元素的标记名（大写）                   |
| [*element*.textContent](https://www.runoob.com/jsref/prop-node-textcontent.html) | 设置或返回一个节点和它的文本内容                             |
| [*element*.title](https://www.runoob.com/jsref/prop-html-title.html) | 设置或返回元素的title属性                                    |
| *element*.toString()                                         | 一个元素转换成字符串                                         |
| [*nodelist*.item()](https://www.runoob.com/jsref/met-nodelist-item.html) | 返回某个元素基于文档树的索引                                 |
| [*nodelist*.length](https://www.runoob.com/jsref/prop-nodelist-length.html) | 返回节点列表的节点数目。                                     |

### 8.3 属性对象

**Attr 对象**

- 在 HTML DOM 中, **Attr 对象** 代表一个 HTML 属性。

- HTML属性总是属于HTML元素。

**NamedNodeMap 对象**

- 在 HTML DOM 中, the **NamedNodeMap 对象** 表示一个无顺序的节点列表。
- 我们可通过节点名称来访问 NamedNodeMap 中的节点。



| 属性 / 方法                                                  | 描述                                                        |
| :----------------------------------------------------------- | :---------------------------------------------------------- |
| [*attr*.isId](https://www.runoob.com/jsref/prop-attr-isid.html) | 如果属性是 ID 类型，则 isId 属性返回 true，否则返回 false。 |
| [*attr*.name](https://www.runoob.com/jsref/prop-attr-name.html) | 返回属性名称                                                |
| [*attr*.value](https://www.runoob.com/jsref/prop-attr-value.html) | 设置或者返回属性值                                          |
| [*attr*.specified](https://www.runoob.com/jsref/prop-attr-specified.html) | 如果属性被指定返回 true ，否则返回 false                    |
|                                                              |                                                             |
| [*nodemap*.getNamedItem()](https://www.runoob.com/jsref/met-namednodemap-getnameditem.html) | 从节点列表中返回的指定属性节点。                            |
| [*nodemap*.item()](https://www.runoob.com/jsref/met-namednodemap-item.html) | 返回节点列表中处于指定索引号的节点。                        |
| [*nodemap*.length](https://www.runoob.com/jsref/prop-namednodemap-length.html) | 返回节点列表的节点数目。                                    |
| [*nodemap*.removeNamedItem()](https://www.runoob.com/jsref/met-namednodemap-removenameditem.html) | 删除指定属性节点                                            |
| [*nodemap*.setNamedItem()](https://www.runoob.com/jsref/met-namednodemap-setnameditem.html) | 设置指定属性节点(通过名称)                                  |

#### DOM 4 警告 !!!

- 在 W3C DOM 内核中, Attr (属性) 对象继承节点对象的所有属性和方法 。

- 在 DOM 4 中, Attr (属性) 对象不再从节点对象中继承。

**从长远的代码质量来考虑，在属性对象中你需要避免使用节点对象属性和方法:**

| 属性 / 方法            | 避免原因                   |
| :--------------------- | :------------------------- |
| *attr*.appendChild()   | 属性没有子节点             |
| *attr*.attributes      | 属性没有属性               |
| *attr*.baseURI         | 使用 document.baseURI 替代 |
| *attr*.childNodes      | 属性没有子节点             |
| *attr*.cloneNode()     | 使用 attr.value 替代       |
| *attr*.firstChild      | 属性没有子节点             |
| *attr*.hasAttributes() | 属性没有属性               |
| *attr*.hasChildNodes   | 属性没有子节点             |
| *attr*.insertBefore()  | 属性没有子节点             |
| *attr*.isEqualNode()   | 没有意义                   |
| *attr*.isSameNode()    | 没有意义                   |
| *attr*.isSupported()   | 通常为 true                |
| *attr*.lastChild       | 属性没有子节点             |
| *attr*.nextSibling     | 属性没有兄弟节点           |
| *attr*.nodeName        | 使用 *attr*.name 替代      |
| *attr*.nodeType        | 通常为 2 (ATTRIBUTE-NODE)  |
| *attr*.nodeValue       | 使用 *attr*.value 替代     |
| *attr*.normalize()     | 属性没有规范               |
| *attr*.ownerDocument   | 通常为你的 HTML 文档       |
| *attr*.ownerElement    | 你用来访问属性的 HTML 元素 |
| *attr*.parentNode      | 你用来访问属性的 HTML 元素 |
| *attr*.previousSibling | 属性没有兄弟节点           |
| *attr*.removeChild     | 属性没有子节点             |
| *attr*.replaceChild    | 属性没有子节点             |
| *attr*.textContent     | 使用 *attr*.value 替代     |

### 8.4 DOM 事件

#### 鼠标事件

| 属性                                                         | 描述                                   | DOM  |
| :----------------------------------------------------------- | :------------------------------------- | :--- |
| [onclick](https://www.runoob.com/jsref/event-onclick.html)   | 当用户点击某个对象时调用的事件句柄。   | 2    |
| [oncontextmenu](https://www.runoob.com/jsref/event-oncontextmenu.html) | 在用户点击鼠标右键打开上下文菜单时触发 |      |
| [ondblclick](https://www.runoob.com/jsref/event-ondblclick.html) | 当用户双击某个对象时调用的事件句柄。   | 2    |
| [onmousedown](https://www.runoob.com/jsref/event-onmousedown.html) | 鼠标按钮被按下。                       | 2    |
| [onmouseenter](https://www.runoob.com/jsref/event-onmouseenter.html) | 当鼠标指针移动到元素上时触发。         | 2    |
| [onmouseleave](https://www.runoob.com/jsref/event-onmouseleave.html) | 当鼠标指针移出元素时触发               | 2    |
| [onmousemove](https://www.runoob.com/jsref/event-onmousemove.html) | 鼠标被移动。                           | 2    |
| [onmouseover](https://www.runoob.com/jsref/event-onmouseover.html) | 鼠标移到某元素之上。                   | 2    |
| [onmouseout](https://www.runoob.com/jsref/event-onmouseout.html) | 鼠标从某元素移开。                     | 2    |
| [onmouseup](https://www.runoob.com/jsref/event-onmouseup.html) | 鼠标按键被松开。                       | 2    |

#### 键盘事件

| 属性                                                         | 描述                       | DOM  |
| :----------------------------------------------------------- | :------------------------- | :--- |
| [onkeydown](https://www.runoob.com/jsref/event-onkeydown.html) | 某个键盘按键被按下。       | 2    |
| [onkeypress](https://www.runoob.com/jsref/event-onkeypress.html) | 某个键盘按键被按下并松开。 | 2    |
| [onkeyup](https://www.runoob.com/jsref/event-onkeyup.html)   | 某个键盘按键被松开。       | 2    |

#### 框架/对象（Frame/Object）事件

| 属性                                                         | 描述                                                         | DOM  |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :--- |
| [onabort](https://www.runoob.com/jsref/event-onabort.html)   | 图像的加载被中断。 ( <object>)                               | 2    |
| [onbeforeunload](https://www.runoob.com/jsref/event-onbeforeunload.html) | 该事件在即将离开页面（刷新或关闭）时触发                     | 2    |
| [onerror](https://www.runoob.com/jsref/event-onerror.html)   | 在加载文档或图像时发生错误。 ( <object>, <body>和 <frameset>) |      |
| [onhashchange](https://www.runoob.com/jsref/event-onhashchange.html) | 该事件在当前 URL 的锚部分发生修改时触发。                    |      |
| [onload](https://www.runoob.com/jsref/event-onload.html)     | 一张页面或一幅图像完成加载。                                 | 2    |
| [onpageshow](https://www.runoob.com/jsref/event-onpageshow.html) | 该事件在用户访问页面时触发                                   |      |
| [onpagehide](https://www.runoob.com/jsref/event-onpagehide.html) | 该事件在用户离开当前网页跳转到另外一个页面时触发             |      |
| [onresize](https://www.runoob.com/jsref/event-onresize.html) | 窗口或框架被重新调整大小。                                   | 2    |
| [onscroll](https://www.runoob.com/jsref/event-onscroll.html) | 当文档被滚动时发生的事件。                                   | 2    |
| [onunload](https://www.runoob.com/jsref/event-onunload.html) | 用户退出页面。 ( <body> 和 <frameset>)                       | 2    |

#### 表单事件

| 属性                                                         | 描述                                                         | DOM  |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :--- |
| [onblur](https://www.runoob.com/jsref/event-onblur.html)     | 元素失去焦点时触发                                           | 2    |
| [onchange](https://www.runoob.com/jsref/event-onchange.html) | 该事件在表单元素的内容改变时触发( <input>, <keygen>, <select>, 和 <textarea>) | 2    |
| [onfocus](https://www.runoob.com/jsref/event-onfocus.html)   | 元素获取焦点时触发                                           | 2    |
| [onfocusin](https://www.runoob.com/jsref/event-onfocusin.html) | 元素即将获取焦点时触发                                       | 2    |
| [onfocusout](https://www.runoob.com/jsref/event-onfocusout.html) | 元素即将失去焦点时触发                                       | 2    |
| [oninput](https://www.runoob.com/jsref/event-oninput.html)   | 元素获取用户输入时触发                                       | 3    |
| [onreset](https://www.runoob.com/jsref/event-onreset.html)   | 表单重置时触发                                               | 2    |
| [onsearch](https://www.runoob.com/jsref/event-onsearch.html) | 用户向搜索域输入文本时触发 ( <input="search">)               |      |
| [onselect](https://www.runoob.com/jsref/event-onselect.html) | 用户选取文本时触发 ( <input> 和 <textarea>)                  | 2    |
| [onsubmit](https://www.runoob.com/jsref/event-onsubmit.html) | 表单提交时触发                                               | 2    |

#### 剪贴板事件

| 属性                                                       | 描述                           | DOM  |
| :--------------------------------------------------------- | :----------------------------- | :--- |
| [oncopy](https://www.runoob.com/jsref/event-oncopy.html)   | 该事件在用户拷贝元素内容时触发 |      |
| [oncut](https://www.runoob.com/jsref/event-oncut.html)     | 该事件在用户剪切元素内容时触发 |      |
| [onpaste](https://www.runoob.com/jsref/event-onpaste.html) | 该事件在用户粘贴元素内容时触发 |      |

#### 打印事件

| 属性                                                         | 描述                                                 | DOM  |
| :----------------------------------------------------------- | :--------------------------------------------------- | :--- |
| [onafterprint](https://www.runoob.com/jsref/event-onafterprint.html) | 该事件在页面已经开始打印，或者打印窗口已经关闭时触发 |      |
| [onbeforeprint](https://www.runoob.com/jsref/event-onbeforeprint.html) | 该事件在页面即将开始打印时触发                       |      |

#### 拖动事件

| 事件                                                         | 描述                                 | DOM  |
| :----------------------------------------------------------- | :----------------------------------- | :--- |
| [ondrag](https://www.runoob.com/jsref/event-ondrag.html)     | 该事件在元素正在拖动时触发           |      |
| [ondragend](https://www.runoob.com/jsref/event-ondragend.html) | 该事件在用户完成元素的拖动时触发     |      |
| [ondragenter](https://www.runoob.com/jsref/event-ondragenter.html) | 该事件在拖动的元素进入放置目标时触发 |      |
| [ondragleave](https://www.runoob.com/jsref/event-ondragleave.html) | 该事件在拖动元素离开放置目标时触发   |      |
| [ondragover](https://www.runoob.com/jsref/event-ondragover.html) | 该事件在拖动元素在放置目标上时触发   |      |
| [ondragstart](https://www.runoob.com/jsref/event-ondragstart.html) | 该事件在用户开始拖动元素时触发       |      |
| [ondrop](https://www.runoob.com/jsref/event-ondrop.html)     | 该事件在拖动元素放置在目标区域时触发 |      |

#### 多媒体（Media）事件

| 事件                                                         | 描述                                                         | DOM  |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :--- |
| [onabort](https://www.runoob.com/jsref/event-onabort-media.html) | 事件在视频/音频（audio/video）终止加载时触发。               |      |
| [oncanplay](https://www.runoob.com/jsref/event-oncanplay.html) | 事件在用户可以开始播放视频/音频（audio/video）时触发。       |      |
| [oncanplaythrough](https://www.runoob.com/jsref/event-oncanplaythrough.html) | 事件在视频/音频（audio/video）可以正常播放且无需停顿和缓冲时触发。 |      |
| [ondurationchange](https://www.runoob.com/jsref/event-ondurationchange.html) | 事件在视频/音频（audio/video）的时长发生变化时触发。         |      |
| onemptied                                                    | 当期播放列表为空时触发                                       |      |
| [onended](https://www.runoob.com/jsref/event-onended.html)   | 事件在视频/音频（audio/video）播放结束时触发。               |      |
| [onerror](https://www.runoob.com/jsref/event-onerror-media.html) | 事件在视频/音频（audio/video）数据加载期间发生错误时触发。   |      |
| [onloadeddata](https://www.runoob.com/jsref/event-onloadeddata.html) | 事件在浏览器加载视频/音频（audio/video）当前帧时触发触发。   |      |
| [onloadedmetadata](https://www.runoob.com/jsref/event-onloadedmetadata.html) | 事件在指定视频/音频（audio/video）的元数据加载后触发。       |      |
| [onloadstart](https://www.runoob.com/jsref/event-onloadstart.html) | 事件在浏览器开始寻找指定视频/音频（audio/video）触发。       |      |
| [onpause](https://www.runoob.com/jsref/event-onpause.html)   | 事件在视频/音频（audio/video）暂停时触发。                   |      |
| [onplay](https://www.runoob.com/jsref/event-onplay.html)     | 事件在视频/音频（audio/video）开始播放时触发。               |      |
| [onplaying](https://www.runoob.com/jsref/event-onplaying.html) | 事件在视频/音频（audio/video）暂停或者在缓冲后准备重新开始播放时触发。 |      |
| [onprogress](https://www.runoob.com/jsref/event-onprogress.html) | 事件在浏览器下载指定的视频/音频（audio/video）时触发。       |      |
| [onratechange](https://www.runoob.com/jsref/event-onratechange.html) | 事件在视频/音频（audio/video）的播放速度发送改变时触发。     |      |
| [onseeked](https://www.runoob.com/jsref/event-onseeked.html) | 事件在用户重新定位视频/音频（audio/video）的播放位置后触发。 |      |
| [onseeking](https://www.runoob.com/jsref/event-onseeking.html) | 事件在用户开始重新定位视频/音频（audio/video）时触发。       |      |
| [onstalled](https://www.runoob.com/jsref/event-onstalled.html) | 事件在浏览器获取媒体数据，但媒体数据不可用时触发。           |      |
| [onsuspend](https://www.runoob.com/jsref/event-onsuspend.html) | 事件在浏览器读取媒体数据中止时触发。                         |      |
| [ontimeupdate](https://www.runoob.com/jsref/event-ontimeupdate.html) | 事件在当前的播放位置发送改变时触发。                         |      |
| [onvolumechange](https://www.runoob.com/jsref/event-onvolumechange.html) | 事件在音量发生改变时触发。                                   |      |
| [onwaiting](https://www.runoob.com/jsref/event-onwaiting.html) | 事件在视频由于要播放下一帧而需要缓冲时触发。                 |      |

#### 动画事件

| 事件                                                         | 描述                            | DOM  |
| :----------------------------------------------------------- | :------------------------------ | :--- |
| [animationend](https://www.runoob.com/jsref/event-animationend.html) | 该事件在 CSS 动画结束播放时触发 |      |
| [animationiteration](https://www.runoob.com/jsref/event-animationiteration.html) | 该事件在 CSS 动画重复播放时触发 |      |
| [animationstart](https://www.runoob.com/jsref/event-animationstart.html) | 该事件在 CSS 动画开始播放时触发 |      |

#### 过渡事件

| 事件                                                         | 描述                          | DOM  |
| :----------------------------------------------------------- | :---------------------------- | :--- |
| [transitionend](https://www.runoob.com/jsref/event-transitionend.html) | 该事件在 CSS 完成过渡后触发。 |      |

#### 其他事件

| 事件                                                         | 描述                                                         | DOM  |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :--- |
| onmessage                                                    | 该事件通过或者从对象(WebSocket, Web Worker, Event Source 或者子 frame 或父窗口)接收到消息时触发 |      |
| onmousewheel                                                 | 已废弃。 使用 [onwheel](https://www.runoob.com/jsref/event-onwheel.html) 事件替代 |      |
| [ononline](https://www.runoob.com/jsref/event-ononline.html) | 该事件在浏览器开始在线工作时触发。                           |      |
| [onoffline](https://www.runoob.com/jsref/event-onoffline.html) | 该事件在浏览器开始离线工作时触发。                           |      |
| onpopstate                                                   | 该事件在窗口的浏览历史（history 对象）发生改变时触发。       |      |
| [onshow](https://www.runoob.com/jsref/event-onshow.html)     | 该事件当 <menu> 元素在上下文菜单显示时触发                   |      |
| onstorage                                                    | 该事件在 Web Storage(HTML 5 Web 存储)更新时触发              |      |
| [ontoggle](https://www.runoob.com/jsref/event-ontoggle.html) | 该事件在用户打开或关闭 <details> 元素时触发                  |      |
| [onwheel](https://www.runoob.com/jsref/event-onwheel.html)   | 该事件在鼠标滚轮在元素上下滚动时触发                         |      |

#### 事件对象

**常量**

| 静态变量        | 描述                                 | DOM  |
| :-------------- | :----------------------------------- | :--- |
| CAPTURING-PHASE | 当前事件阶段为捕获阶段(1)            | 1    |
| AT-TARGET       | 当前事件是目标阶段,在评估目标事件(1) | 2    |
| BUBBLING-PHASE  | 当前的事件为冒泡阶段 (3)             | 3    |

**属性**

| 属性                                                         | 描述                                           | DOM  |
| :----------------------------------------------------------- | :--------------------------------------------- | :--- |
| [bubbles](https://www.runoob.com/jsref/event-bubbles.html)   | 返回布尔值，指示事件是否是起泡事件类型。       | 2    |
| [cancelable](https://www.runoob.com/jsref/event-cancelable.html) | 返回布尔值，指示事件是否可拥可取消的默认动作。 | 2    |
| [currentTarget](https://www.runoob.com/jsref/event-currenttarget.html) | 返回其事件监听器触发该事件的元素。             | 2    |
| eventPhase                                                   | 返回事件传播的当前阶段。                       | 2    |
| [target](https://www.runoob.com/jsref/event-target.html)     | 返回触发此事件的元素（事件的目标节点）。       | 2    |
| [timeStamp](https://www.runoob.com/jsref/event-timestamp.html) | 返回事件生成的日期和时间。                     | 2    |
| [type](https://www.runoob.com/jsref/event-type.html)         | 返回当前 Event 对象表示的事件的名称。          | 2    |

**方法**

| 方法              | 描述                                     | DOM  |
| :---------------- | :--------------------------------------- | :--- |
| initEvent()       | 初始化新创建的 Event 对象的属性。        | 2    |
| preventDefault()  | 通知浏览器不要执行与事件关联的默认动作。 | 2    |
| stopPropagation() | 不再派发事件。                           | 2    |

#### 目标事件对象

**方法**

| 方法                  | 描述                                                    | DOM  |
| :-------------------- | :------------------------------------------------------ | :--- |
| addEventListener()    | 允许在目标事件中注册监听事件(IE8 = attachEvent())       | 2    |
| dispatchEvent()       | 允许发送事件到监听器上 (IE8 = fireEvent())              | 2    |
| removeEventListener() | 运行一次注册在事件目标上的监听事件(IE8 = detachEvent()) | 2    |

#### 事件监听对象

**方法**

| 方法          | 描述                         | DOM  |
| :------------ | :--------------------------- | :--- |
| handleEvent() | 把任意对象注册为事件处理程序 | 2    |

#### 文档事件对象

**方法**

| 方法          | 描述 | DOM  |
| :------------ | :--- | :--- |
| createEvent() |      | 2    |

#### 鼠标/键盘事件对象

**属性**

| 属性                                                         | 描述                                                         | DOM  |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :--- |
| [altKey](https://www.runoob.com/jsref/event-altkey.html)     | 返回当事件被触发时，"ALT" 是否被按下。                       | 2    |
| [button](https://www.runoob.com/jsref/event-button.html)     | 返回当事件被触发时，哪个鼠标按钮被点击。                     | 2    |
| [clientX](https://www.runoob.com/jsref/event-clientx.html)   | 返回当事件被触发时，鼠标指针的水平坐标。                     | 2    |
| [clientY](https://www.runoob.com/jsref/event-clienty.html)   | 返回当事件被触发时，鼠标指针的垂直坐标。                     | 2    |
| [ctrlKey](https://www.runoob.com/jsref/event-ctrlkey.html)   | 返回当事件被触发时，"CTRL" 键是否被按下。                    | 2    |
| [Location](https://www.runoob.com/jsref/event-key-location.html) | 返回按键在设备上的位置                                       | 3    |
| [charCode](https://www.runoob.com/jsref/event-key-charcode.html) | 返回onkeypress事件触发键值的字母代码。                       | 2    |
| [key](https://www.runoob.com/jsref/event-key-key.html)       | 在按下按键时返回按键的标识符。                               | 3    |
| [keyCode](https://www.runoob.com/jsref/event-key-keycode.html) | 返回onkeypress事件触发的键的值的字符代码，或者 onkeydown 或 onkeyup 事件的键的代码。 | 2    |
| [which](https://www.runoob.com/jsref/event-key-which.html)   | 返回onkeypress事件触发的键的值的字符代码，或者 onkeydown 或 onkeyup 事件的键的代码。 | 2    |
| [metaKey](https://www.runoob.com/jsref/event-metakey.html)   | 返回当事件被触发时，"meta" 键是否被按下。                    | 2    |
| [relatedTarget](https://www.runoob.com/jsref/event-relatedtarget.html) | 返回与事件的目标节点相关的节点。                             | 2    |
| [screenX](https://www.runoob.com/jsref/event-screenx.html)   | 返回当某个事件被触发时，鼠标指针的水平坐标。                 | 2    |
| [screenY](https://www.runoob.com/jsref/event-screeny.html)   | 返回当某个事件被触发时，鼠标指针的垂直坐标。                 | 2    |
| [shiftKey](https://www.runoob.com/jsref/event-shiftkey.html) | 返回当事件被触发时，"SHIFT" 键是否被按下。                   | 2    |

**方法**

| 方法                | 描述                   | W3C  |
| :------------------ | :--------------------- | :--- |
| initMouseEvent()    | 初始化鼠标事件对象的值 | 2    |
| initKeyboardEvent() | 初始化键盘事件对象的值 | 3    |



## 9 BOM

> 浏览器对象模型（**B**rowser **O**bject **M**odel (BOM)）
>
> 由于现代浏览器已经（几乎）实现了 JavaScript 交互性方面的相同方法和属性，因此常被认为是 BOM 的方法和属性。

### 9.1 Window 对象

- 所有浏览器都支持 window 对象。它表示浏览器窗口。
- 所有 JavaScript 全局对象、函数以及变量均自动成为 window 对象的成员。
- 全局变量是 window 对象的属性。
- 全局函数是 window 对象的方法。
- HTML DOM 的 document 也是 window 对象的属性之一

| 方法/属性          | 描述                             |
| :----------------- | :------------------------------- |
| window.innerHeight | 浏览器窗口的内部高度(包括滚动条) |
| window.innerWidth  | 浏览器窗口的内部宽度(包括滚动条) |
| window.open()      | 打开新窗口                       |
| window.close()     | 关闭当前窗口                     |
| window.moveTo()    | 移动当前窗口                     |
| window.resizeTo()  | 调整当前窗口的尺寸               |

### 9.2 Window Screen

**window.screen**对象在编写时可以不使用 window 这个前缀。

| 方法/属性          | 描述                                                   |
| :----------------- | :----------------------------------------------------- |
| screen.availWidth  | 可用的屏幕宽度，以像素计，减去界面特性，比如窗口任务栏 |
| screen.availHeight | 可用的屏幕高度，以像素计，减去界面特性，比如窗口任务栏 |
| screen.colorDepth  | 色彩深度                                               |
| screen.pixelDepth  | 色彩分辨率                                             |

### 9.3 Window Location

**window.location** 对象在编写时可不使用 window 这个前缀

| 方法/属性         | 描述                                     |
| :---------------- | :--------------------------------------- |
| location.hostname | 返回 web 主机的域名                      |
| location.pathname | 返回当前页面的路径和文件名               |
| location.port     | 返回 web 主机的端口 （80 或 443）        |
| location.protocol | 返回所使用的 web 协议（http: 或 https:） |
| location.href     | 返回当前页面的 URL                       |
| location.assign() | 加载新的文档                             |

### 9.4 Window History

**window.history**对象在编写时可不使用 window 这个前缀。

为了保护用户隐私，对 JavaScript 访问该对象的方法做出了限制。

| 方法/属性         | 描述                         |
| :---------------- | :--------------------------- |
| history.back()    | 与在浏览器点击后退按钮相同   |
| history.forward() | 与在浏览器中点击向前按钮相同 |

### 9.5 Window Navigator

**window.navigator** 对象在编写时可不使用 window 这个前缀。

| 方法/属性               | 描述         |
| :---------------------- | :----------- |
| navigator.appCodeName   | 浏览器代号   |
| navigator.appName       | 浏览器名称   |
| navigator.appVersion    | 浏览器版本   |
| navigator.cookieEnabled | 启用Cookies  |
| navigator.platform      | 硬件平台     |
| navigator.userAgent     | 用户代理     |
| navigator.language      | 用户代理语言 |

**警告!!!**

来自 navigator 对象的信息具有误导性，不应该被用于检测浏览器版本，这是因为：

- navigator 数据可被浏览器使用者更改
- 一些浏览器对测试站点会识别错误
- 浏览器无法报告晚于浏览器发布的新操作系统

**浏览器检测**

由于 navigator 可误导浏览器检测，使用对象检测可用来嗅探不同的浏览器。

由于不同的浏览器支持不同的对象，您可以使用对象来检测浏览器。例如，由于只有 Opera 支持属性 "window.opera"，您可以据此识别出 Opera。

例子：if (window.opera) {...some action...}

### 9.5 弹窗

弹窗方法可以不带window对象。

| 方法/属性 | 描述                                           |
| :-------- | :--------------------------------------------- |
| alert()   | 警告框经常用于确保用户可以得到某些信息。       |
| confirm() | 确认框通常用于验证是否接受用户操作。           |
| prompt()  | 提示框经常用于提示用户在进入页面前输入某个值。 |

```js
window.alert("sometext");
window.alert("sometext");
window.prompt("sometext","defaultvalue");
```

### 9.6 计时事件

通过使用 JavaScript，我们有能力做到在一个设定的时间间隔之后来执行代码，而不是在函数被调用后立即执行。我们称之为计时事件。

在 JavaScritp 中使用计时事件是很容易的，两个关键方法是:

- setInterval() - 间隔指定的毫秒数不停地执行指定的代码。
- setTimeout() - 在指定的毫秒数后执行指定代码。

**注意:** setInterval() 和 setTimeout() 是 HTML DOM Window对象的两个方法。

#### 9.6.1 setInterval() 方法

- setInterval() 间隔指定的毫秒数不停地执行指定的代码

- **window.setInterval()** 方法可以不使用 window 前缀，直接使用函数 **setInterval()**。

```js
//开始
window.setInterval("*javascript function*",*milliseconds*);
//停止
window.clearInterval(intervalVariable)
```

#### 9.6.2 setTimeout() 方法

```js
window.setTimeout("javascript function", milliseconds);
window.clearTimeout(timeoutVariable)
```

### 9.7 cookie

Cookie 是一些数据, 存储于你电脑上的文本文件中。

当 web 服务器向浏览器发送 web 页面时，在连接关闭后，服务端不会记录用户的信息。

Cookie 的作用就是用于解决 "如何记录客户端的用户信息":

- 当用户访问 web 页面时，他的名字可以记录在 cookie 中。
- 在用户下一次访问该页面时，可以在 cookie 中读取用户访问记录。

Cookie 以名/值对形式存储，如下所示:

```
username=John Doe
```

当浏览器从服务器上请求 web 页面时， 属于该页面的 cookie 会被添加到该请求中。服务端通过这种方式来获取用户的信息。

**创建Cookie**

```js
document.cookie="username=John Doe; expires=Thu, 18 Dec 2043 12:00:00 GMT; path=/";
```

**读取 Cookie**

```js
//document.cookie 将以字符串的方式返回所有的 cookie，类型格式： cookie1=value; cookie2=value; cookie3=value;
var x = document.cookie;
```

**修改 Cookie**

```js
//旧的 cookie 将被覆盖。
document.cookie="username=John Smith; expires=Thu, 18 Dec 2043 12:00:00 GMT; path=/";
```

**删除 Cookie**

```js
//删除 cookie 非常简单。您只需要设置 expires 参数为以前的时间即可
//删除时不必指定 cookie 的值。
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 GMT";
```

