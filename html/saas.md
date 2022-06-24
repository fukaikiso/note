# Sass 

## 1. sass概述

- Sass (英文全称：Syntactically Awesome Stylesheets) 是一个最初由 Hampton Catlin 设计并由 Natalie Weizenbaum 开发的层叠样式表语言。
- Sass 是一个 CSS 预处理器。
- Sass 是 CSS 扩展语言，可以帮助我们减少 CSS 重复的代码，节省开发时间。
- Sass 完全兼容所有版本的 CSS。
- Sass 扩展了 CSS3，增加了规则、变量、混入、选择器、继承、内置函数等等特性。
- Sass 生成良好格式化的 CSS 代码，易于组织和维护。
- Sass 文件后缀为 **.scss**。

- [Sass中文文档]([Sass教程 Sass中文文档 | Sass中文网](https://www.sass.hk/docs/))

## 2 安装与使用

### 2.1 安装

```shell
//npm 安装
npm install -g sass

//Windows上用包管理器chocolately安装
choco install sass

//mac上用Homebrew安装
brew install sass/sass/sass
```

### 2.2 使用

将.scss文件转为.css文件: 语法：`$ sass [待转换scss文件] [转换后的css文件]`

```shell
sass test.scss test.css
```

监听文件夹，一旦scss文件夹中的.scss文件改变，立即执行编译，并把.css文件存到css文件夹中：

```shell
sass -w scss:css
```

### 2.3 注释

- /**/，可以被编译到css
- //，只能在scss中使用，不编译到css

## 3 基本语法

### 3.1 Sass变量

> 变量用于存储一些信息，它可以重复使用。Sass 变量可以存储以下信息：字符串、数字、颜色值、布尔值、列表、null 值。
>
> Sass 变量使用 **$** 符号：`$variablename: value;`
>
> Sass 变量的作用域只能在当前的层级上有效果
>
> 可以使用 **!global** 关键词来设置变量是全局的：

**scss代码**

```scss
$myFont: Helvetica, sans-serif;
$myColor: red;
$myFontSize: 18px;
$myWidth: 680px;

body {
  font-family: $myFont;
  font-size: $myFontSize;
  color: $myColor;
}

#container {
  width: $myWidth;
}
```

**转换后的css代码**

```css
body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: red;
}

#container {
  width: 680px;
}
```

### 3.2 css功能拓展

> Sass 嵌套 CSS 选择器类似于 HTML 的嵌套规则。

#### 3.2.1 嵌套规则

**scss**

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }
  li {
    display: inline-block;
  }
  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

**css**

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

#### 3.2.2 嵌套属性

**scss**

```scss
font: {
  family: Helvetica, sans-serif;
  size: 18px;
  weight: bold;
}

text: {
  align: center;
  transform: lowercase;
  overflow: hidden;
}
```

**css**

```css
font-family: Helvetica, sans-serif;
font-size: 18px;
font-weight: bold;

text-align: center;
text-transform: lowercase;
text-overflow: hidden;
```

#### 3.2.3 父选择器

**scss**

```scss
//在嵌套 CSS 规则时，有时也需要直接使用嵌套外层的父选择器，例如，当给某个元素设定 hover 样式时，或者当 body 元素有某个 classname 时，可以用 & 代表嵌套规则外层的父选择器。
a {
  font-weight: bold;
  text-decoration: none;
  &:hover { text-decoration: underline; }
  body.firefox & { font-weight: normal; }
}
```

**css**

```css
a {
  font-weight: bold;
  text-decoration: none; }
  a:hover {
    text-decoration: underline; }
  body.firefox a {
    font-weight: normal; }
```

#### 3.2.4 插值语句

**scss**

```scss
//通过 #{} 插值语句可以在选择器或属性名中使用变量：
$name: foo;
$attr: border;
p.#{$name} {
  #{$attr}-color: blue;
}
```

**css**

```css
p.foo {
  border-color: blue; }
```

### 3.3 if

**scss**

```scss
@mixin btn($w, $h) {
  width: $w;
  height: $h;
  border-radius: 5px;
  background-color: red;

  @if ($w>100px and $h>50px) {
    box-shadow: 5px 5px 5px #666;
  } @else {
    box-shadow: 2px 2px 2px #666;
  }
}

.btn1 {
  @include btn(50px, 50px);
}

.btn2 {
  @include btn(150px, 150px);
}
```

**css**

```css
.btn1 {
  width: 50px;
  height: 50px;
  border-radius: 5px;
  background-color: red;
  box-shadow: 2px 2px 2px #666;
}

.btn2 {
  width: 150px;
  height: 150px;
  border-radius: 5px;
  background-color: red;
  box-shadow: 5px 5px 5px #666;
}
```

### 3.4 for

#### 3.4.1 @for...from..to...{...}  (前闭后开区间)

**scss**

```scss
@for $i from 1 to 3 {
    ul {
        li:nth-child(#{$i}) {
            width: 100px + $i*10;
            height: 20px;
        }
    }
}
```

**css**

```css
ul li:nth-child(1) {
  width: 110px;
  height: 20px;
}

ul li:nth-child(2) {
  width: 120px;
  height: 20px;
}
```

#### 3.4.1 @for...from..through...{...}  (闭区间)

**scss**

```scss
@for $i from 1 through 3 {
    ol {
        li:nth-child(#{$i}) {
            width: 100px + $i*10;
            height: 20px;
        }
    }
}
```

**css**

```css
ol li:nth-child(1) {
  width: 110px;
  height: 20px;
}

ol li:nth-child(2) {
  width: 120px;
  height: 20px;
}

ol li:nth-child(3) {
  width: 130px;
  height: 20px;
}
```



## 4 @import与Partials

### 4.1 @import

> 类似 CSS，Sass 支持 **@import** 指令。
>
> @import 指令可以让我们导入其他文件等内容。
>
> CSS @import 指令在每次调用时，都会创建一个额外的 HTTP 请求。但，Sass @import 指令将文件包含在 CSS 中，不需要额外的 HTTP 请求。

Sass @import 指令语法如下：`@import filename;`

**scss**

```scss
//reset.scss
html,
body,
ul,
ol {
  margin: 0;
  padding: 0;
}

//standard.scss
@import "reset";

body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: red;
}
```

**css**

```css
html, body, ul, ol {
  margin: 0;
  padding: 0;
}

body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: red;
}
```

### 4.2 Partials

> 如果你不希望将一个 Sass 的代码文件编译到一个 CSS 文件，你可以在文件名的开头添加一个下划线。这将告诉 Sass 不要将其编译到 CSS 文件。
>
> 但是，在导入语句中我们不需要添加下划线。
>
> **注意：**请不要将带下划线与不带下划线的同名文件放置在同一个目录下，比如，_colors.scss 和 colors.scss 不能同时存在于同一个目录下，否则带下划线的文件将会被忽略。

Sass Partials 语法格式：`_filename;`

**scss**

```scss
//_colors.scss
//不会被编译成_colors.css
$myPink: #EE82EE;
$myBlue: #4169E1;
$myGreen: #8FBC8F;
```

```scss
//导入_colors.scss
@import "colors";

body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: $myBlue;
}
```

## 5 @mixin与@inclue

> @mixin 指令允许我们定义一个可以在整个样式表中重复使用的样式。
>
> @include 指令可以将混入（mixin）引入到文档中。

### 5.1 基本使用

**scss**

```scss
//定义混入
@mixin important-text {
  color: red;
  font-size: 25px;
  font-weight: bold;
  border: 1px solid blue;
}

//使用混入
.danger {
  @include important-text;
  background-color: green;
}
```

**css**

```css
.danger {
  color: red;
  font-size: 25px;
  font-weight: bold;
  border: 1px solid blue;
  background-color: green;
}
```

### 5.2 向混入传参

（1）普通传参

**scss**

```scss
/* 混入接收两个参数 */
@mixin bordered($color, $width) {
  border: $width solid $color;
}

.myArticle {
  @include bordered(blue, 1px);  // 调用混入，并传递两个参数
}

.myNotes {
  @include bordered(red, 2px); // 调用混入，并传递两个参数
}
```

**css**

```css
.myArticle {
  border: 1px solid blue;
}

.myNotes {
  border: 2px solid red;
}
```

（2）传参带默认值

**scss**

```scss
/* 混入接收两个参数 */
@mixin bordered($color: blue, $width: 1px) {
  border: $width solid $color;
}

@mixin sexy-border($color, $width: 1in) {
  border: {
    color: $color;
    width: $width;
    style: dashed;
  }
}
p { @include sexy-border(blue); }
h1 { @include sexy-border(blue, 2in); }
```

**css**

```css
p {
  border-color: blue;
  border-width: 1in;
  border-style: dashed; }

h1 {
  border-color: blue;
  border-width: 2in;
  border-style: dashed;
}
```

（3）可变参数

**scss**

```scss
/* 混入接收若干个个参数 */
@mixin box-shadow($shadows...) {
      -moz-box-shadow: $shadows;
      -webkit-box-shadow: $shadows;
      box-shadow: $shadows;
}

.shadows {
  @include box-shadow(0px 4px 5px #666, 2px 6px 10px #999);
}
```

**css**

```css
.shadows {
  -moz-box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
  -webkit-box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
  box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
}
```

（4）浏览器前缀使用混入

**scss**

```scss
@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}

.myBox {
  @include transform(rotate(20deg));
}
```

**css**

```css
.myBox {
  -webkit-transform: rotate(20deg);
  -ms-transform: rotate(20deg);
  transform: rotate(20deg);
}
```

## 6 @extend与继承

> @extend 指令告诉 Sass 一个选择器的样式从另一选择器继承。
>
> 如果一个样式与另外一个样式几乎相同，只有少量的区别，则使用 @extend 就显得很有用。
>
> 以下 Sass 实例中，我们创建了一个基本的按钮样式 .button-basic，接着我们定义了两个按钮样式 .button-report 与 .button-submit，它们都继承了 .button-basic ，它们主要区别在于背景颜色与字体颜色，其他的样式都是一样的。

### 6.1 extend

**scss**

```scss
.button-basic  {
  border: none;
  padding: 15px 30px;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
}

.button-report  {
  @extend .button-basic;
  background-color: red;
}

.button-submit  {
  @extend .button-basic;
  background-color: green;
  color: white;
}
```

**css**

```css
.button-basic, .button-report, .button-submit {
  border: none;
  padding: 15px 30px;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
}

.button-report  {
  background-color: red;
}

.button-submit  {
  background-color: green;
  color: white;
}
```

****

### 6.2 占位符选择器

**scss**

```scss
//%可以作为占位符，当它们单独使用时，不会被编译到 CSS 文件中，需要配合@extend使用
#context a%extreme {
  color: blue;
  font-weight: bold;
  font-size: 2em;
}

.notice {
  @extend %extreme;
}
```

**css**

```css
#context a.notice {
  color: blue;
  font-weight: bold;
  font-size: 2em; }
```

****



## 7 函数

> Sass 定义了各种类型的函数，这些函数我们可以通过 CSS 语句直接调用。

| 序号 | 函数类别                                                     |
| :--- | :----------------------------------------------------------- |
| 1    | [Sass 字符串相关函数](https://www.runoob.com/sass/sass-string-func.html) |
| 2    | [Sass 数字相关函数](https://www.runoob.com/sass/sass-numeric-func.html) |
| 3    | [Sass 列表(List)相关函数](https://www.runoob.com/sass/sass-list-func.html) |
| 4    | [Sass 映射(Map)相关函数](https://www.runoob.com/sass/sass-map-func.html) |
| 5    | [Sass 选择器相关函数](https://www.runoob.com/sass/sass-selector-func.html) |
| 6    | [Sass Introspection 相关函数](https://www.runoob.com/sass/sass-introspection-func.html) |
| 7    | [Sass 颜色相关函数](https://www.runoob.com/sass/sass-color-func.html) |

