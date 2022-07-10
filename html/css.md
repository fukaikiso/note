# **CSS**

> [MDN参考文档](https://developer.mozilla.org/en-US/docs/Web/CSS)

## 1. 常见问题

### 1.1 幽灵空白节点

> 幽灵空白节点指**HTML5 文档声明**中，内联元素的所有解析和渲染表现就如同每个行框盒子的前面有一个“空白节点”一样。这个“空白节点”永远透明，不占据任何宽度，看不见也无法通过脚本获取。

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        div {
            background-color: red;
        }
    </style>
</head>
<body>
    <h3>幽灵空白节点</h3>
    <p>出现原因：在HTML5文档声明下，内部会有看不见的没有宽度与实体的空白元素</p>
    <p>内联元素默认的vertical-align: baseline</p>
    <br>
    <p>解决方案：</p>
    <div>
        <img src="./img/1.png" alt="">
    </div>
    <br>
    <div>
        <img src="./img/1.png" alt="" style="vertical-align: bottom;">
    </div>
    <br>
    <div style="line-height: 0px;">
        <img src="./img/1.png" alt="">
    </div>
    <br>
    <div style="font-size: 0px;">
        <img src="./img/1.png" alt="">
    </div>
    <br>
    <div>
        <img src="./img/1.png" alt="" style="display: block;">
    </div>
    <br>
</body>
</html>
```

### 1.2 流式布局中外边距塌陷问题

#### （1）相邻元素垂直外边距塌陷

- 当上下相邻的两个块元素相遇时，如果上面的元素有下外边距margin-bottom
- 下面的元素有上外边距margin-top，则他们之间的垂直间距不是margin-bottom与margin-top之和
- 取两个值中的较大者这种现象被称为相邻块元素垂直外边距的合并(也称外边距塌陷)。
- **解决方案**：尽量给只给一个盒子添加margin值

#### （2）嵌套块元素垂直外边距的塌陷

- 对于两个嵌套关系的块元素，如果父元素没有上内边距及边框
- 父元素的上外边距会与子元素的上外边距发生合并
- 合并后的外边距为两者中的较大者
- **解决方法**：
  - 为父元素定义边框
  - 为父元素定义边框上、下内边距（**推荐**）
  - 为父元素设置块级格式化上下文（BFC），`overflow:hidden`
  - ...

### 1.3 内联元素

#### （1）margin

 - margin水平方向有效
 - margin垂直方向无效

#### （2）padding

 - padding水平方向有效
 - padding垂直方向仅视觉上有效，并不影响布局

#### （3）with和height

	- 设置无效
	- 高度可以通过line-height改变

### 1.3 盒子模型

#### （1）标准盒子模型

- `box-sizing:content-box`

- 宽度高度包含`content`

#### （2）怪异盒子模型（CSS3新增）

- `box-sizing:border-box`
- 宽度高度包含`content+border+padding`

### 1.4 块级格式化上下文（BFC）

#### （1）定义

- block formatting content
- 独立的渲染区域，与外部不相关

#### （2）作用

- 避免margin外边距塌陷问题
- 避免float高度坍塌问题

#### （3）形成BFC常见的条件

- 设置浮动，`float : left/right`
- 绝对定位元素，`position : absolute/fixed`
- 设置display，`display : inline-block/table-cell/table-caption/inline-flex`
- 设置overflow, `overflow : hidden/auto/scroll`

#### （4）布局规则

- 内部Box会在垂直方向上一个接一个的放置  
- 垂直方向上的距离由margin决定  
-  bfc的取余不会与float的元素区域重叠  
- 计算bfc的高度时,浮动元素也参与计算  
- bfc就是页面上一个独立的容器, 容器里面的子元素不会影响到外面元素

###   <span id="float">1.5 float高度坍塌问题</span>

> 当父级的子元素浮动，子元素便无法支撑起父级的高度，从而导致父级高度坍塌

（1）父级元素自定义高度：适合于已知子元素高度的情况，例如导航条

（2）**BFC**：任何设置了BFC的元素，与浮动元素相遇时，都可以实现“自动填充”的适应布局。即父元素设置BFC后，子元素浮动，父元素高度会自动填充。适用于子元素位置高度，子元素不超出父级范围的情况

```css
/*触发父级元素BFC*/
overflow : hidden/auto/scroll; 
```

（3）使父元素与子元素成为同层元素：相当于父级元素脱离文档流

```css
/*父元素float*/
float ： left/right;
/*父元素使用定位属性*/
/*父元素脱离文档流，影响父元素的父元素，导致上层元素依然需要解决高度坍塌问题*/
```

（4）**clear清除**

```css
/*
父元素加clearfix类
伪元素after添加至父元素的最后，必须包含content属性
clear：both指该元素前面不允许有浮动对象（兄元素），该属性只适用于块级元素
相当于伪元素移动到浮动元素的下一行，撑开了父元素
*/
.clearfix::after {
    content: "";
    display: block;
    clear: both;
}
```

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			.box{
				border: 5px solid black;
			}
			/* .box::before{
				content: "我是before";
				background: yellowgreen;
				width: 100px;
				height: 100px;
			}
			.box::after{
				content: "我是after";
				background: yellow;
				width: 100px;
				height: 100px;
			} */

			.son1 {
				width: 100px;
				height: 100px;
				float: left;
				background-color: red;
			}

			.son2 {
				width: 200px;
				height: 200px;
				background-color: blue;
				float: left;
				/* clear: both; */
			}
			.son3 {
				width: 150px;
				height: 150px;
				float: right;
				background-color: pink;
			}

			.clearfix::after {
				content: "";
				display: block;
				clear: both;
			}
		</style>
	</head>
	<body>
		<div class="box clearfix">
			<div class="son1"></div>
			<div class="son2"></div>
			<div class="son3"></div>
		</div>
	</body>
</html>
```

### 1.6 居中

#### （1）margin : auto结合position

```css
/*
1.margin:auto不能使内联元素水平居中？
  因为内联元素不独占一行，
  而块级元素独占一行，该设置将该行的剩余空间平均分配给左右外边距，当块级元素设置了width时，左右平均分的空余空间便会显示出来，体现为元素居中

/*
2.为什么margin:auto不能垂直居中？
  因为元素是靠内容撑开，垂直方向上默认没有剩余的空间
*/

/*
3.如何利用margin:auto实现水平垂直居中？
  （1）设置定位，使对边的值一样
  （2）设置元素高度、宽度
   定位使元素撑开，因此margin:auto可以自动分配空余的空间
  ***缺点：必须设置子元素的长宽，否则子元素显示的内容会被撑开
*/
.father {
    background-color: rgba(0, 0, 0, 0.7);
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
}

.son {
    width: 400px;
    height: 250px;
    background-color: #fff;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
}
```

#### （2）position结合transform

```css
.father {
    width: 400px;
    height: 400px;
    background-color: red;
    position: relative;
}
/*transform相对于元素的中心点，而position相对于左上角的点*/
.son {
    width: 100px;
    height: 100px;
    background-color: blue;
    position: absolute;
    top: 50%;
    left: 50%;
    transform : translate(-50%,-50%)
}
```



### 1.7 清除默认样式

#### （1）base

```css
/*base.css*/
* {
    margin:0;
    padding:0
}

li {
    list-style:none
}

img {
    vertical-align:top;
    border:none
}

/*a的文字颜色按实际更改*/
a{
    text-decoration:none;
    color : #333;
}

ul, ol, { 
　　list-style: none；
}

input {
    outline : none;
}

table {
    border-collapse:collapse;
}
table,th, td {
    border: 1px solid black;
}

```

#### （2）common

```css
/*common.css*/
/*版心的宽度按照实际大小*/
.wrapper {
    margin : 0 auto;
    width : 1000px;
}
```

### 1.8 单飞翼布局与双飞翼布局（圣杯局部）

* 单飞翼布局，并用语言描述

```css
.box1 {
    height: 200px;
    display: flex;
}
.box1 .left {
    width: 230px;
    background-color: red;
    flex-shrink: 0;
}
.box1 .right {
    width: 100%;
    background-color: blue;
    flex-grow: 1;
}
```

父子嵌套两个子元素一左一右。父级元素使用`display:flex`且默认不换行，左侧子元素不放大不缩小，右侧子元素可设置放大比例1。

* 双飞翼（圣杯布局）,并用语言描述

```css
.box2 {
    height: 300px;
    display: flex;
}
.box2 .left,.box2 .right {
    width: 230px;
    flex-shrink: 0;
    background-color: green;
}
.box2 .center {
    flex-grow: 1;
    background-color: yellow;
}
```

父元素嵌套三个子元素，父元素使用flex布局，左和右两个元素设置宽度，并且不能缩小，中间元素可以被放大和默认缩小

### 1.9 CSS优化

#### （1）CSS文件大小

css代码增多，文件相对变大。css文件压缩当前代码，减小css文件大小。

https://tool.chinaz.com/Tools/CssFormat.aspx

#### （2）删除未使用的CSS样式

在css样式书写中，没用的css样式，以及没有用的css选择器就删掉。减少不必要的类选择器，可以搭配多种关系型或者结构型一起使用。

#### （3）css文件的使用

* css外部样式，复用性强
* 复用性不强的页面，样式就使用一次的，可以考虑内部样式

#### （4）高效使用css动画样式

css动画渲染，要比js动画逻辑加载快得多。

#### （5）css hank

在不同浏览器中，元素的渲染样式会不同。考虑根据自己的项目，或者公司的要求设置编写固定的css样式重置文件。



## 2 选择器

### 2.1 基础选择器

#### （1）通用选择器

`*`指的是当前页面上所有的标签都应用该样式

```css
* {
	margin : 0;
    padding : 0;
}
```

* 指所有元素，优先级非常低，性能低
* 在练习中常用的使用通配符的场景`*{margin:0;padding:0}`将所有元素的内外边距去除

#### （2）标签选择器

直接使用标签的名字当作选择器使用

```css
div {
    color:red;
}
p {
    color:blue;
}
```

* 优势是快捷，选中所有标签相同的元素渲染
* 劣势是选择太广泛，不利于项目使用
* 优先级权重值1（最低的）

#### （3）id选择器

```css
#text {
    color : red;
}
```

* 先要在标签中加入`id`属性，使用css中的`#id名{}`
* 优势非常直观的找到该元素，优先级非常高，权重100
* 在一般的项目书写中，尽量不是用id选择器，复用性很差

#### （4）类选择器

```css
.center {
    margin : 0 auto;
}
```

* 类选择器需要在标签中加`class`属性，在样式中`.类名{}`
* 类选择器复用性高，在项目中经常使用
* 优先级的权重10

#### （5）群组选择器

```css
.center,#text {
    width : 100px;
}
```

* 多个选择器用逗号链接，使用相同的样式
* 群组选择器不限定选择器必须是同一个类型的

### 2.2 关系型选择器

#### （1）后代和子代

```css
/*后代选择器*/
ul li {
    margin : 0 10px;
}
/*子代选择器*/
div>span {
    color : red;
}
```

* 后代选择器需要在先代选择器后加空格链接后代选择器。后代元素指的是当前标签内嵌套的所有标签
* `祖先选择器 后代选择器{}`
* `父代选择器>子代选择器{}`
* 使用场景，内部结构简单，没有那么多相同标签

#### （2）兄弟选择器和相邻兄弟选择器

```css
/*兄弟选择器*/
div~div {
    margin : 0 10px;
}
/*子代选择器*/
div+div {
    color : red;
}
```

* 兄弟选择器使用`兄选择器~弟选择器{}`
* 只能选中后面的兄弟，不能选中前面的兄弟
* 相邻兄弟选择器，指的是紧紧挨着的兄弟元素
* 相邻兄弟选择器`兄选择器+弟选择器 {}`

### 2.3 伪类选择器

#### （1）鼠标相关

```css
.box {
	width: 150px;
	height: 50px;
	background-color: yellow;
}

/*鼠标悬停 :hover */
.box:hover {
	background-color: red;
}

/*点击激活 :active */
.box:active {
	background-color: blue;
}

/*链接未激活前 :link */
a:link {color: green;}

/*链接激活后 :visited */
a:visited {color: darkorange;}

/*对于a标签 :link>:visited>:hover>`:active` */
```

#### （2）获取焦点

```css
/*获取焦点 :focus */
/* 获取焦点前 */
input+span {
	color: transparent;
}
/* 获取焦点后 */
input:focus+span {
	color: red;
}
input:focus {
	background-color: yellow;
}
```

#### （3）[其他]([CSS 伪类 | 菜鸟教程 (runoob.com)](https://www.runoob.com/css/css-pseudo-classes.html))

| **选择器**        | 示例                | **示例说明**                                  |
| ----------------- | ------------------- | --------------------------------------------- |
| first-child       | p:first-child       | 选择器匹配属于任意元素的第一个子元素的 p 元素 |
| last-child        | p:last-child        | 选择所有p元素的最后一个子元素                 |
| nth-child(n)      | p:nth-child(2)      | 选择所有 p 元素的父元素的第二个子元素         |
| nth-last-child(n) | p:nth-last-child(2) | 选择所有p元素倒数的第二个子元素               |
| checked           | input:checked       | 选择所有选中的表单元素                        |
| :empty            | p:empty             | 选择所有没有子元素的p元素                     |
| [attribute]       | a[href]             | 选择具有href属性的a标签                       |
| ...               |                     |                                               |

- 负方向范围，例如：选择第1~第3个子元素`li:nth-child(-n+3)`
- 正方向范围，例如：选择第3~最后个子元素`li:nth-child(n+3)`
- 限定范围，例如：选择第3~6个子元素`li:nth-child(-n+3):li:nth-child(n+3)`

### 2.4 伪元素选择器

- 伪元素是一个附加至选择器末的关键词，允许你对被选择的元素进行指定部分的修改样式。简单说它不是一个元素，而是元素某个部分的样式。
- 注意：按照规范使用`::`，但是大部分的伪元素也可以使用`:`，尽量使用`::`区别于伪类。

#### （1）::before

```css
/*指的是元素内容最开始的位置插入，ie7以下不支持。*/
div::before {
	/* 必写属性,可以空 */
	content: "我爱你，";
	/* 接下来渲染的都是伪元素的样式 */
	color: red;
	background-color: yellow;
}
```

#### （2）::after

```css
/*指的是元素内容最末尾的位置插入，ie7以下不支持。*/
/* 在元素后 */
div::after {
	content: "♥";
}
```

### 2.5 优先级

#### （1）不同选择器不同样式的渲染规则

当选择器发生冲突，渲染同一个元素的时候。不同样式会同时生效。样式的渲染因为不同所以不产生冲突叠加。

#### （2）相同选择器相同样式

相同选择器，会采用顺序读取原则，后来的会覆盖之前的，但前提是渲染的样式相同值不同的。

#### （3）指定大于继承原则

在css样式中有一些属性是具有继承性的。

https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance

指定当前元素样式要大于继承样式。

（4）选择器不同权值的计算

| 选择器               | 权值  | 权级 |
| -------------------- | ----- | ---- |
| 继承样式             | 无    | 无   |
| * > +                | 0     | 0级  |
| 标签和伪元素         | 0001  | 1级  |
| 伪类、属性，类       | 0010  | 2级  |
| id选择器             | 0100  | 3级  |
| style=“”内联         | 1000  | 4级  |
| !important提升优先级 | 10000 | 5级  |

* 权值大的优先渲染
* 权值跃进，并不是十进制的。组合权值的跃进值，权值累加但不会越级。
* !important提升优先级，出现的场景使用UI框架中与框架样式冲突的自定义样式可以加

### 2.6 穿透

- vue组件编译后，会将 template 中的每个元素加入 [data-v-xxxx] 属性来确保 style scoped 仅本组件的元素而不会污染全局

- 如果需要局部修改第三方组件样式，又不想去除scoped属性造成组件间的样式污染，可以使用`>>>`方式穿透scope。

```css
.rich-content >>> img {
  max-width: 100vw;
}
```

## 3 常见属性

### 3.1 尺寸

**所有CSS 尺寸 (Dimension)属性**

| 属性                                                         | 描述                 |
| :----------------------------------------------------------- | :------------------- |
| [height](https://www.runoob.com/cssref/pr-dim-height.html)   | 设置元素的高度。     |
| [line-height](https://www.runoob.com/cssref/pr-dim-line-height.html) | 设置行高。           |
| [max-height](https://www.runoob.com/cssref/pr-dim-max-height.html) | 设置元素的最大高度。 |
| [max-width](https://www.runoob.com/cssref/pr-dim-max-width.html) | 设置元素的最大宽度。 |
| [min-height](https://www.runoob.com/cssref/pr-dim-min-height.html) | 设置元素的最小高度。 |
| [min-width](https://www.runoob.com/cssref/pr-dim-min-width.html) | 设置元素的最小宽度。 |
| [width](https://www.runoob.com/cssref/pr-dim-width.html)     | 设置元素的宽度。     |

#### （1）宽度和高度属性

* `width`宽度属性
* `height`高度属性
* 以上两个属性的取值，长度单位，还可以是%,但是不能是负值

```css
div {
    width:100px;
    height:200px;
}
```

#### （2）默认的宽度和高度

* 块元素默认宽度是父元素的一行，所以不写也会存在
* 高度是依靠内容撑开的高度
* 内联元素是依靠内容撑开宽度和高度的

### 3.2 边框

 **CSS边框属性**

| 属性                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [border](https://www.runoob.com/cssref/pr-border.html)       | 简写属性，用于把针对四个边的属性设置在一个声明。             |
| [border-style](https://www.runoob.com/cssref/pr-border-style.html) | 用于设置元素所有边框的样式，或者单独地为各边设置边框样式。   |
| [border-width](https://www.runoob.com/cssref/pr-border-width.html) | 简写属性，用于为元素的所有边框设置宽度，或者单独地为各边边框设置宽度。 |
| [border-color](https://www.runoob.com/cssref/pr-border-color.html) | 简写属性，设置元素的所有边框中可见部分的颜色，或为 4 个边分别设置颜色。 |
| [border-bottom](https://www.runoob.com/cssref/pr-border-bottom.html) | 简写属性，用于把下边框的所有属性设置到一个声明中。           |
| [border-bottom-color](https://www.runoob.com/cssref/pr-border-bottom-color.html) | 设置元素的下边框的颜色。                                     |
| [border-bottom-style](https://www.runoob.com/cssref/pr-border-bottom-style.html) | 设置元素的下边框的样式。                                     |
| [border-bottom-width](https://www.runoob.com/cssref/pr-border-bottom-width.html) | 设置元素的下边框的宽度。                                     |
| [border-left](https://www.runoob.com/cssref/pr-border-left.html) | 简写属性，用于把左边框的所有属性设置到一个声明中。           |
| [border-left-color](https://www.runoob.com/cssref/pr-border-left-color.html) | 设置元素的左边框的颜色。                                     |
| [border-left-style](https://www.runoob.com/cssref/pr-border-left-style.html) | 设置元素的左边框的样式。                                     |
| [border-left-width](https://www.runoob.com/cssref/pr-border-left-width.html) | 设置元素的左边框的宽度。                                     |
| [border-right](https://www.runoob.com/cssref/pr-border-right.html) | 简写属性，用于把右边框的所有属性设置到一个声明中。           |
| [border-right-color](https://www.runoob.com/cssref/pr-border-right-color.html) | 设置元素的右边框的颜色。                                     |
| [border-right-style](https://www.runoob.com/cssref/pr-border-right-style.html) | 设置元素的右边框的样式。                                     |
| [border-right-width](https://www.runoob.com/cssref/pr-border-right-width.html) | 设置元素的右边框的宽度。                                     |
| [border-top](https://www.runoob.com/cssref/pr-border-top.html) | 简写属性，用于把上边框的所有属性设置到一个声明中。           |
| [border-top-color](https://www.runoob.com/cssref/pr-border-top-color.html) | 设置元素的上边框的颜色。                                     |
| [border-top-style](https://www.runoob.com/cssref/pr-border-top-style.html) | 设置元素的上边框的样式。                                     |
| [border-top-width](https://www.runoob.com/cssref/pr-border-top-width.html) | 设置元素的上边框的宽度。                                     |
| [border-radius](https://www.runoob.com/cssref/css3-pr-border-radius.html) | 设置圆角的边框。                                             |

**CSS3 新增边框属性**

| 属性                                                         | 说明                                           | CSS  |
| :----------------------------------------------------------- | :--------------------------------------------- | :--- |
| [border-image](https://www.runoob.com/cssref/css3-pr-border-image.html) | 设置所有边框图像的速记属性。                   | 3    |
| [border-radius](https://www.runoob.com/cssref/css3-pr-border-radius.html) | 一个用于设置所有四个边框- *-半径属性的速记属性 | 3    |
| [box-shadow](https://www.runoob.com/cssref/css3-pr-box-shadow.html) | 附加一个或多个下拉框的阴影                     | 3    |

**CSS3 圆角属性**

| 属性                                                         | 描述                                      |
| :----------------------------------------------------------- | :---------------------------------------- |
| [border-radius](https://www.runoob.com/cssref/css3-pr-border-radius.html) | 所有四个边角 border-*-*-radius 属性的缩写 |
| [border-top-left-radius](https://www.runoob.com/cssref/css3-pr-border-top-left-radius.html) | 定义了左上角的弧度                        |
| [border-top-right-radius](https://www.runoob.com/cssref/css3-pr-border-top-right-radius.html) | 定义了右上角的弧度                        |
| [border-bottom-right-radius](https://www.runoob.com/cssref/css3-pr-border-bottom-right-radius.html) | 定义了右下角的弧度                        |
| [border-bottom-left-radius](https://www.runoob.com/cssref/css3-pr-border-bottom-left-radius.html) | 定义了左下角的弧度                        |

#### （1）边框属性

* `border`边框样式,粗细，颜色，边框的样式不存在顺序问题
* 边框样式中其实包含了三个分属性
  * `border-width`线宽
  * `border-style`线的样式
  * `border-color`边框的颜色

```css
/* 粗细，颜色，边框的样式 */
border:3px dotted #FF0000;
```

#### （2）边框方向

* 单独给边框指定方向 `border-{方向}`
  * `border-top`上边框
  * `border-left`左边框
  * `border-right`右边框
  * `border-bottom`下边框

```css
/* 下边框：2像素的虚线边框 */
border-bottom: 2px dashed red;
```

#### （3）三角形

​	1.写三角形需要派出一个块元素（宽高可设）
​	2.是不需要在元素中增加文字内容
​	3.一个元素在网页中形状矩形，可以依靠它的边框

```css
.sjx {
/* 宽高既然都是0是否可以不写 */
	width: 0;
/* 高因为本来也是0可以不写，宽度不写默认父级的100% */
/* 四个边框分别使用不同颜色写 */
	border: 100px solid transparent;
/* 其中一个边是需要颜色的 */
	border-top-color: red;
}
```

#### （4）圆角

- `border-radius`, 取值可以是长度单位，也可以是%
- 圆形需要元素的宽度、高度一致，`border-radius: 50%;`
- 椭圆形，不需要宽高一致，`border-radius: 50%;`
- 胶囊型，`border-radius: 高度的一半;`

### 3.3 内边距

设置元素的内间距`padding`属性，内间距也叫作"内补间"，内间距是存在于盒子内部的。

**内间距会造成整个元素变大，因为它在边界里面所以会将元素撑大**

#### （1）内间距的方向

* `padding-top`内容到元素顶部之间的距离，上内间距
* `padding-bottom`内容到元素底部之间的距离，下内间距
* `padding-left`内容到元素左侧边界之间的距离，左内间距
* `padding-right`内容到元素右侧边界之间的距离，右内间距

#### （2）内间距的简写方式

* `padding:20px`四个方向内间距相同
* `padding:10px 30px`上下内间距 ，左右内间距
* `padding:10px 20px 5px`上内间距，左右内间距有，下内间距
* `padding:5px 10px 15px 20px`上，右，下，左（顺时针）

#### （3）内联元素的内间距

**这里提到的内联元素不包含可替换元素（img）**

* 内联元素左右内间距正常生效
* 上下内间距，会产生“视觉生效”实际没作用还会出现布局样式堆叠

### 3.4 外边距

- `margin`属性可以设置元素（上右下左）四个方向和其它元素的距离。

- 外边距是可以让元素产生移动的。

- 这个利用外边距产生的距离，相当当前这个元素和周围元素产生的额外空间，不属于元素本身的大小。

#### （1）外边距的方向

* `margin-top`元素顶部和其它元素的之间的距离，因为长幼尊卑的问题，移动是自己的位置
* `margin-bottom`元素都是底部与其他元素之间的距离。在块级流式布局中，“一般情况”只会对下级元素（兄弟）产生影响，因此移动将会是相邻的兄弟元素
* `margin-left`元素左侧和其它元素之间的距离，因为长幼尊卑左侧是父级和兄长，因此移动是自己。

* `margin-right`元素右侧与其他元素之间的距离，移动的将是其他元素，不是移动自己。在流式布局内，块级元素右侧并无兄弟。所以即使出现外边距，视觉上也不会有特殊的效果。
* 总结：上、左外边距自己移动，下、右外边距其他（兄弟）元素移动

#### （2）视觉效果

* 四周的空间并不在元素内部，而在元素外部
* `margin`属性渲染渲染元素，不带任何背景色
* 取值是可以取负值的
* 内联元素很特殊，对于不可设置的内联元素（如:span、a、i、b...）是不会被上下的外边距影响的
* 但内联元素，`img`是可替换的内联，`button`、`input`等可以被`margin`完全影响

#### （3）外边距的取值

* 正值和负值都是可以使用的，正值是增加距离，负值是减小、缩减距离。
* `0`距离是紧挨着，负值就会让元素出现叠加、重叠，如果是第一个子元素，会超出父级范围
* `auto`自动，只能在流式布局中使得块级元素左右方向的外边距发生水平居中效果
* 百分比取值，参照的是父级元素的宽度与高度（用的非常少）

#### （4）简写方式

* `margin:10px`四个方向的外边距相同
* `margin:10px 20px` 上下  左右
* `margin:10px 20px 30px ` 上  左右  下
* `margin:10px 20px 30px 50px` 上  右  下 左 （顺时针）
* `margin:auto` 只能让块元素在父级元素中水平居中【小重点因为经常用】也可以写成`margin:0 auto`

#### （5）外边距的重叠【

* 相邻兄弟之间的外边距会发生视觉的重合，取最大值显现，前提是在文档流的流式布局中才会如此显现。
* 在文档流的流式布局中，父级元素的第一个子元素和最后一个子元素，都有和父元素“重叠的边”，导致元素的重合、贴合。因此子元素的上下外边距会带动父元素一起运动。
* 首个和末尾子元素和父元素贴合原因，无法区分边归属于谁。导致父元素被子元素带动。

##### 解决父子重叠问题【要点】

* 给父元素加边框可以将父子的贴合边分开
* 给父元素增加上、下内间距，把第一个和最后一个子元素挤开（推荐）
* 给父级设置块级格式化上下文（BFC）`overflow:hidden`

### 3.5 box

#### （1）box-sizing

- `box-sizing`指定了盒子模型的计算方式和标准
- `box-sizing:content-box`标准盒子模型计算方式，按照`content`(内容)区域作为宽度计算,默认是标准盒子模型
- `box-sizing: border-box`怪异盒模型 你写的宽度中就应该含有`padding`和`border`

#### （2）box-shadow

* `box-shadow`指元素的阴影效果
* 第一个值：必写，阴影的x轴偏移，建议用绝对单位px，可以为负值，阴影的方向不同
* 第二个值：必写，阴影的y轴偏移，建议用绝对单位px，可以为负值，阴影的方向不同
* 第三个值：羽化值，默认为0，羽化值也大虚化程度越强，不允许负值
* 第四个值：阴影扩展半径，默认0，可以为负值（用的较少）
* 第五个值：阴影颜色，使用色值
* 第六个值：内、外阴影，默认`outset`外阴影，内阴影`inset`

### 3.6 隐藏和显示

#### （1）脱离文档流的消失

* `display:none`消失
* 显示回来是元素原有的display属性值，如:`display:block`

####  （2）不脱离文档流占位隐藏

* `visibility: hidden;`隐藏，会保留住原来的位置
* `visibility: visible;`默认不隐藏的属性

#### （3）元素透明

* `opacity: 0;`元素透明度为0时完全看不到
* 0-1之间的值，0透明 1不透明
* 元素透明度，包含元素中的所有内容
* 仍占位置

#### （4）元素缩放

* `transform: scale(0);`
* 仍占位置

### 3.7 溢出

- 当前元素超出了父级元素的范围、空间时，会出现子元素溢出的情况。

* 一般默认情况块级元素没有范围（宽高）,子元素可以随意的增大，它会撑大父元素
* 只有父元素限制范围，并且子元素内容又大于父元素的限制范围才会出现“溢出现象”

#### （1）溢出属性

* `overflow: visible`默认允许溢出
* `overflow: auto`溢出的方向出现拖动条
* `overflow: scroll`双方向都出现拖动条
* `overflow: hidden`溢出隐藏，超出父元素范围的内容全部被裁掉

#### （2）BFC

BFC全称`block formatting context` ，翻译成中文叫做“块级格式化上下文”。（面试题）

简单说，他是一个独立的渲染区域，这个区域与外部不相干了。相当于子元素在父元素内部折腾，但也不会洒出父元素。

* `overflow`属性的三个值会让父元素形成BFC结界`auto`,`scroll`,`hidden`这三个值
* BFC结界一旦形成，就能避免margin的父子边粘连问题
* BFC结界一旦形成，重新计算在父元素内部的浮动子元素所占的高度（子元素一浮动，父元素就会高度坍塌）

### 3.8 背景

**CSS 背景属性**

| Property                                                     | 描述                                         |
| :----------------------------------------------------------- | :------------------------------------------- |
| [background](https://www.runoob.com/cssref/css3-pr-background.html) | 简写属性，作用是将背景属性设置在一个声明中。 |
| [background-attachment](https://www.runoob.com/cssref/pr-background-attachment.html) | 背景图像是否固定或者随着页面的其余部分滚动。 |
| [background-color](https://www.runoob.com/cssref/pr-background-color.html) | 设置元素的背景颜色。                         |
| [background-image](https://www.runoob.com/cssref/pr-background-image.html) | 把图像设置为背景。                           |
| [background-position](https://www.runoob.com/cssref/pr-background-position.html) | 设置背景图像的起始位置。                     |
| [background-repeat](https://www.runoob.com/cssref/pr-background-repeat.html) | 设置背景图像是否及如何重复。                 |

**CSS3新的背景属性**

| 顺序                                                         | 描述                     | CSS  |
| :----------------------------------------------------------- | :----------------------- | :--- |
| [background-clip](https://www.runoob.com/cssref/css3-pr-background-clip.html) | 规定背景的绘制区域。     | 3    |
| [background-origin](https://www.runoob.com/cssref/css3-pr-background-origin.html) | 规定背景图片的定位区域。 | 3    |
| [background-size](https://www.runoob.com/cssref/css3-pr-background-size.html) | 规定背景图片的尺寸。     | 3    |

#### （1）背景图插入

* `background-image:url(路径)`属性和值的语法
* 注意背景图和`img`标签的图片插入是有区别的
  * `img`标签插入的图片在默认情况下直接是图片的本身大小
  * `background-image:url(路径)`方式不能直接使用并且显示图片的，必须要给当前元素设置宽度和高度才能显示背景图

* 图片被平铺到元素中会出现两种情况
  * 图片范围大于元素范围，显示不全
  * 图片范围小于元素范围或出现重复

#### （2）背景渐变

* `background-image`属性可以设置渐变效果
* 渐变在页面中的应用多于美化，应用最多的就是线性渐变
* `background-image:linear-gradient(颜色1,颜色2,颜色3,...)`颜色可以使用任何色值，如：十六进制，英文颜色，rgb()等等
* 颜色的排列方向默认是从上向下，需要改变渐变的角度`background-image:linear-gradient(角度,颜色1,颜色2,...)`角度的值使用`xxdeg`使用度的单位
* 渐变色范围的设定`background-image:linear-gradient(角度,颜色1 起始位置 结束位置,颜色2 起始位置 结束位置,...)`范围的设定需要写在每个颜色色值的后面，值可以使用长度单位或者%

```css
/* 新版浏览器 */
background-image: linear-gradient(90deg,blue 0 100px,#fff 100px 200px,red 200px 300px);
/* 浏览器未更新 */
background-image: linear-gradient(90deg,blue 33%,#fff 33%,#fff 67%,red 67%);
```

#### （3）背景图的重复方式

* 背景图重复原因是因为图片的大小比元素范围小才会出现重复，重复的方向看哪个方向有空余的空间
* 取值
  * `background-repeat: repeat-x;`x轴方向平铺
  * `background-repeat: repeat-y;`y轴方向平铺
  * `background-repeat: no-repeat;`不重复平铺

#### （4）背景图定位

* `background-position` 背景图定位
* 关键词取值（x轴 y轴）
  * `background-position:left bottom`
  * `left`和`right`指x轴定位位置
  * `bottom`和`top` 指y轴定位位置
  * `center`中间位置，既可以是x轴也可以是y轴
  * 两个轴都是中间位置，可以省略只写一个`center`
* 长度单位和百分比取值
  * 使用百分比指元素的宽度（x轴）高度（y轴）
  * 长度单位直接指背景移动的长度位置，单位可以是px、em、rem...，可以为负值

#### （5）精灵图

- CSS Sprite 直译为css精灵图，网页图片处理的一种方式。

- UI会把多个小图标整合到一张图片中，再利用背景图定位，选取到需要的小图标位置展示出来。

- 优势是减少了向服务器的请求次数，进行了css优化

* 确定范围，需要图片的宽高要设定
* 插入需要的精灵图
* 最好加上背景图不重复
* 改变`background-position`参照图片左上角区域的位置，可能需要ps查看
* 一般移动图片，改变定位位置，图片会向左或上移动，注意是负值

```css
/* 精灵图 */
.d8 {
/* 确定显示的区域 */
width: 128px;
height: 128px;
/* 不是必须，方便看范围 */
border: 1px solid black;
/* 背景图加入,默认从左上角开始 */
background-image: url(img/bg/icon/icon.png);
/* 改变定位位置 默认 0 0*/
/* background-position: -128px 0; */
}
.d8:hover {
/* 改变背景图定位的位置 */
background-position: -128px 0;
}
```

#### （6）背景图尺寸

* `background-size`背景图尺寸，没有设置任何尺寸时使用图片本身的大小，宽度高度都是`auto`默认值

* 取值

  * 长度值px，随意设置图片的宽度和高度展示的
  * 百分比，0%~100% 参考的其实是元素宽度和高度

  ```css
  /* 以宽度为标准等比缩放 高度自动适配（对高度有牺牲） */
  background-size: 100% auto;
  /* 以高度为标准等比缩放 宽度自动适配（对宽度有牺牲） */
  background-size: auto 100%;
  ```

  * 关键词的值
    * `background-size: contain;`至少有一张完整的图呈现出来，一定会有多余的空间
    * `background-size: cover;`铺满整个容器，多余的部分会被裁掉

### 3.9 列表

**所有的CSS列表属性**

| 属性                                                         | 描述                                               |
| :----------------------------------------------------------- | :------------------------------------------------- |
| [list-style](https://www.runoob.com/cssref/pr-list-style.html) | 简写属性。用于把所有用于列表的属性设置于一个声明中 |
| [list-style-image](https://www.runoob.com/cssref/pr-list-style-image.html) | 将图像设置为列表项标志。                           |
| [list-style-position](https://www.runoob.com/cssref/pr-list-style-position.html) | 设置列表中列表项标志的位置。                       |
| [list-style-type](https://www.runoob.com/cssref/pr-list-style-type.html) | 设置列表项标志的类型。                             |

### 3.10 cursor

* `cursor: default;`箭头
* `cursor: pointer;`手型
* `cursor: text;`文本(工字型)
* `cursor: crosshair;`十字光标

### 3.11 元素浮动

#### （1）float

- `float`单词的含义是“浮动”的意思，它最初的作用是为制作“文本环绕”

* `float: left`左浮动，是向父级元素的左侧边界靠拢
* `float: right`右浮动，是向父级元素的右侧边界靠拢

#### （2）元素浮动的作用

​		元素浮动到后期，作用就变成了排版。使块级元素能够横向排列。使用浮动让块级元素横向排版产生的布局就不再是流式布局，它们将脱离文档流，变成了浮动布局。因为浮动布局兼容性很好，低版本ie照样兼容。

​		元素浮动之后产生以下结果：

* 父级元素对浮动的子级元素失去"包裹性"【父元素失去子元素撑起的高度，也叫高度坍塌】
* 破坏原来的文档流【子元素可以横向排列，依然在父元素的宽度范围中】
* **元素浮动会让元素“块状化”**【内联元素，含行内块都会变成块级】
* 当子元素浮动后外边距的重叠现象消失【兄弟间的上下重叠，父子间的上下边重叠】

#### （3）float高度塌陷问题

[解决方案](#float)

### 3.12 元素的定位

#### （1）position

* 定位`position`有五种值：静态定位（默认`static`）、相对定位（`relative`）、绝对定位(`absolute`)、固定定位(`fixed`)、粘性定位（新出的`sticky`）。常用的三种:相对定位、绝对定位、固定定位
* 在定位的相关属性使用中，一定需要元素的移动。使用定位的位置移动使用以下四个属性：`top/left/bottom/right`,值为长度单位或者百分比。不用定位属性不能使用以上四个值让元素移动。
  * `top`正值向下移动，负值向上移动
  * `bottom`正值向上移动，负值向下移动
  * `left`正值向右移动，负值向左移动
  * `right`正值向左移动，负值向右移动
* 层级`z-index`，设定一个定位元素，当元素之间发生重叠时，`z-index`的值越大就会覆盖较小的值。简单说`z-index`值越大层级越高。值为整数字没有任何单位，默认`auto`可以为负值。

#### （2）relative

* 相对定位的属性`position:relative`相对自己原有初始位置的定位
* 它可以使用`left/top/bottom/rigth`移动元素
* 当使用`position:relative`并且使用方向移动时会产生元素的重叠，并没有提升层级。想改变堆叠的层级需要`z-index`属性的设置
* 特点，相对定位元素并没有脱离文档流。还可以支撑父元素，原有位置保持，支撑父元素。
* 和外边距移动的区别，外边距移动会影响其他元素的位置，相对定位不会挤开兄弟元素，但会遮盖兄弟元素。在文档流中，使用相对定位不影响父元素

#### （3）绝对定位

* `position: absolute`定义元素的绝对定位
* 当元素具有绝对定位属性的时候，就会脱离文档流
* 也会造成和其它元素的重叠，使用`z-index`调整层叠顺序
* 可以使用`left/top/right/bottom`改变元素的位置
* “默认静默状态”当元素首次具备`position: absolute`但并未移动，当使用外间距移动时还会按照原来的位置进行移动。一旦使用了`left/top/right/bottom`才成为了真正的绝对定位
* 使用绝对定位的元素会参照离自己最近的有“定位属性的”祖先元素(证据是定位属性的存在)，要保证参照父元素定位，父元素必须有定位属性，建议使用不脱离文档流的定位属性`position: relative`最理想

#### （4）固定定位

* `position:fixed`固定定位属性
* 可以使用`left/top/right/bottom`改变元素的位置
* 也会造成和其它元素的重叠，使用`z-index`调整层叠顺序
* 若需要固定且占据文档流位置的效果，需要父级添加宽高
* 使用了`position:fixed`的元素参照定位的元素不再是自己原来的位置或者父元素等等，只参照`html`根元素（浏览器窗口）

```css
/* 遮罩层 */
.mark {
    background-color: rgba(0,0,0,0.7);
    /* 使用固定定位 */
    position: fixed;
    /* 撑满全屏 前提固定定位*/
    top:0;
    bottom: 0;
    left: 0;
    right: 0;
}
```

#### （5）sticky

- `position:fixed`固定定位属性
- 粘性定位的元素是依赖于用户的滚动，在 `position:relative` 与 `position:fixed `定位之间切换

#### （6）水平、垂直居中的方法（元素在正中间）

当一个元素绝对定位后，并且其触发了流体特性，`margin:auto` 就生效了 (高度还是要给的否则高度被撑满)

* 子元素必须绝对定位
* 子元素四个方向的对立方向数值相同（都为0）
* 再给子元素加`margin:auto`可以让子元素在父元素中水平垂直居中

```css
.mark .login {
    width: 400px;
    height: 250px;
    /* 元素在父元素中水平垂直的方法 */
    position: absolute;
    /* 对立方向相同数值 */
    top:0;
    bottom: 0;
    left: 0;
    right: 0;
    /* 子元素给宽高，并绝对定位，四个方向都为0（相同数值），可以在父元素里水平垂直居中 */
    margin: auto;
}
```

### 3.13 文本效果

**CSS字体属性**

| Property                                                     | 描述                                 |
| :----------------------------------------------------------- | :----------------------------------- |
| [font](https://www.runoob.com/cssref/pr-font-font.html)      | 在一个声明中设置所有的字体属性       |
| [font-family](https://www.runoob.com/cssref/pr-font-font-family.html) | 指定文本的字体系列                   |
| [font-size](https://www.runoob.com/cssref/pr-font-font-size.html) | 指定文本的字体大小                   |
| [font-style](https://www.runoob.com/cssref/pr-font-font-style.html) | 指定文本的字体样式                   |
| [font-variant](https://www.runoob.com/cssref/pr-font-font-variant.html) | 以小型大写字体或者正常字体显示文本。 |
| [font-weight](https://www.runoob.com/cssref/pr-font-weight.html) | 指定字体的粗细。                     |

**CSS3 @font-face 规则**

> 使用以前 CSS 的版本，网页设计师不得不使用用户计算机上已经安装的字体。
>
> 使用 **CSS3**，网页设计师可以使用他/她喜欢的任何字体。
>
> 当你发现您要使用的字体文件时，只需简单的将字体文件包含在网站中，它会自动下载给需要的用户。
>
> 您所选择的字体在新的 **CSS3** 版本有关于 **@font-face** 规则描述。
>
> 您"自己的"的字体是在 **CSS3 @font-face** 规则中定义的。

```css
<style> 
@font-face
{
    font-family: myFirstFont;
    src: url(sansation_light.woff);
}
 
div
{
    font-family:myFirstFont;
}
</style>
```

下表列出了所有的字体描述和里面的@font-face规则定义：

| 描述符        | 值                                                           | 描述                                                         |
| :------------ | :----------------------------------------------------------- | :----------------------------------------------------------- |
| font-family   | *name*                                                       | 必需。规定字体的名称。                                       |
| src           | *URL*                                                        | 必需。定义字体文件的 URL。                                   |
| font-stretch  | normal condensed ultra-condensed extra-condensed semi-condensed expanded semi-expanded extra-expanded ultra-expanded | 可选。定义如何拉伸字体。默认是 "normal"。                    |
| font-style    | normal italic oblique                                        | 可选。定义字体的样式。默认是 "normal"。                      |
| font-weight   | normal bold 100 200 300 400 500 600 700 800 900              | 可选。定义字体的粗细。默认是 "normal"。                      |
| unicode-range | *unicode-range*                                              | 可选。定义字体支持的 UNICODE 字符范围。默认是 "U+0-10FFFF"。 |

#### （1）字号

`font-size`字号，字体的大小，可以使用长度单位，不能为负数。字体大小属性是会被继承的。

大部分浏览器默认字号是16px，谷歌pc端默认最小字体字号12px

> 一般同学写代码用谷歌浏览器做测试，谷歌最小字号12px，测试的是移动端，就会产生字号不能再缩小的情况
>
> 用测试服务器，更改样式之后手机不能马上更新样式，所以手机浏览器会产生缓存

* px像素单位是绝对单位，在任何的终端尺寸是一样的
* `em`和`rem`相对单位
  * `em`单位指的是父级元素字号的倍数
  * `rem`单位指`html`根标签的字号倍数

#### （2）字体系列

`font-family`字体系列允许通过制定有先后顺序的，由字体”名称“或者字体“族名”的列表来选定元素的字体。

简单说，多写几个字体，按先后顺序排列，前面的优先使用。要写的就是字体名字或者一些列字体的统一名字。

* 执行顺序是从前向后执行，当遇到用户电脑没有的字体，就会按照顺序向后渲染
* 如果字体有空格或者中文，需要用引号包裹
* 一般情况下，设置字体系列放到`html`标签上渲染
* 注意的是：商用字体考虑版权

#### （3）字体字重

`font-weight`字体字重就是字体的粗细。浏览器不同展现的效果也会不同（手机端）。

* `font-weight`常用关键词`normal`默认代表正常体，`lighter`细体，`bold`粗体
* `font-weight`使用数值的方式100的倍数，100-900。默认400正常体，600粗体，300细体。

#### （4）简写

可设置的属性是（按顺序）： "font-style font-variant font-weight font-size/line-height font-family"

### 3.13 文本属性

**CSS文本属性**

| 属性                                                         | 描述                     |
| :----------------------------------------------------------- | :----------------------- |
| [color](https://www.runoob.com/cssref/pr-text-color.html)    | 设置文本颜色             |
| [direction](https://www.runoob.com/cssref/pr-text-direction.html) | 设置文本方向。           |
| [letter-spacing](https://www.runoob.com/cssref/pr-text-letter-spacing.html) | 设置字符间距             |
| [line-height](https://www.runoob.com/cssref/pr-dim-line-height.html) | 设置行高                 |
| [text-align](https://www.runoob.com/cssref/pr-text-text-align.html) | 对齐元素中的文本         |
| [text-decoration](https://www.runoob.com/cssref/pr-text-text-decoration.html) | 向文本添加修饰           |
| [text-indent](https://www.runoob.com/cssref/pr-text-text-indent.html) | 缩进元素中文本的首行     |
| [text-shadow](https://www.runoob.com/cssref/css3-pr-text-shadow.html) | 设置文本阴影             |
| [text-transform](https://www.runoob.com/cssref/pr-text-text-transform.html) | 控制元素中的字母         |
| [unicode-bidi](https://www.runoob.com/cssref/pr-text-unicode-bidi.html) | 设置或返回文本是否被重写 |
| [vertical-align](https://www.runoob.com/cssref/pr-pos-vertical-align.html) | 设置元素的垂直对齐       |
| [white-space](https://www.runoob.com/cssref/pr-text-white-space.html) | 设置元素中空白的处理方式 |
| [word-spacing](https://www.runoob.com/cssref/pr-text-word-spacing.html) | 设置字间距               |

**新文本属性**

| 属性                                                         | 描述                                                    | CSS  |
| :----------------------------------------------------------- | :------------------------------------------------------ | :--- |
| [hanging-punctuation](https://www.runoob.com/cssref/css3-pr-hanging-punctuation.html) | 规定标点字符是否位于线框之外。                          | 3    |
| [punctuation-trim](https://www.runoob.com/cssref/css3-pr-punctuation-trim.html) | 规定是否对标点字符进行修剪。                            | 3    |
| [text-align-last](https://www.runoob.com/cssref/css3-pr-text-align-last.html) | 设置如何对齐最后一行或紧挨着强制换行符之前的行。        | 3    |
| [text-emphasis](https://www.runoob.com/css3/css3-pr-text-emphasis.html) | 向元素的文本应用重点标记以及重点标记的前景色。          | 3    |
| [text-justify](https://www.runoob.com/cssref/css3-pr-text-justify.html) | 规定当 text-align 设置为 "justify" 时所使用的对齐方法。 | 3    |
| [text-outline](https://www.runoob.com/cssref/css3-pr-text-outline.html) | 规定文本的轮廓。                                        | 3    |
| [text-overflow](https://www.runoob.com/cssref/css3-pr-text-overflow.html) | 规定当文本溢出包含元素时发生的事情。                    | 3    |
| [text-shadow](https://www.runoob.com/cssref/css3-pr-text-shadow.html) | 向文本添加阴影。                                        | 3    |
| [text-wrap](https://www.runoob.com/cssref/css3-pr-text-wrap.html) | 规定文本的换行规则。                                    | 3    |
| [word-break](https://www.runoob.com/cssref/css3-pr-word-break.html) | 规定非中日韩文本的换行规则。                            | 3    |
| [word-wrap](https://www.runoob.com/cssref/css3-pr-word-wrap.html) | 允许对长的不可分割的单词进行分割并换行到下一行。        | 3    |

#### （1）文本颜色

- `color:色值`文字的颜色，该属性可以被继承。值使用颜色色值。

#### （2）文本的水平对齐方式

- `text-align`定义行内内容(文本、内联元素),如何相对他的块级父元素对齐。

* `text-align`属性并不写给对齐的元素而是写给它的块级父元素（写给爸爸）
* 取值
  * `text-align:left`默认左对齐
  * `text-align:center`居中对齐
  * `text-align:right`右对齐

#### （3）行高

`line-height`行高也叫作行间距，指的是文本之间的距离，含文本本身的高度。

* `line-height:20px`长度
* `line-height:数字`数字每单位，代表倍数（字号的几倍行距）
* 如果需要单行文字在元素内垂直居中，`line-height:元素高度`

#### （4）文本的修饰线

* `text-decoration: underline;`下划线
* `text-decoration: none;`无线条
* `text-decoration: line-through;`删除线

#### （5）文本溢出效果

* 文本溢出先要控制元素范围（宽度)
* 强制不换行`white-space:nowrap`
* 溢出部分隐藏`overflow:hidden`
* 文本溢出的省略号`text-overflow: ellipsis`

```css
.text {
/* 1.限制边界 */
width: 150px;
/* 2.强制文本不换行 */
white-space:nowrap;
/* 3.溢出部分不看 */
overflow: hidden;
/* 4.文本溢出的省略号 */
text-overflow: ellipsis;
}

/*1. 书写HTML结构,用一个标签包裹内容,也可以指定这个标签的宽度,如果不指定就会根据浏览器的宽度变化而变化*/

/*2. 单行文字显示省略号*/

/*让内容溢出不换行*/

white-space:nowrap;

/*让超出的内容隐藏*/

overflow:hidden;

/*让超出的内容用省略号显示*/

text-overflow:ellipsis;

/*3. 多行文字显示省略号*/

/*让超出的内容隐藏*/

overflow:hidden;

/*让超出的内容用省略号显示*/

text-overflow:ellipsis;

/*作为弹性伸缩盒子模型显示*/

display:-webkit-box;

/*设置伸缩盒子的子元素排列方式--从上到下垂直排列*/

-webkit-box-orient:vertical;

/*指定显示的多少行*/

-webkit-line-clamp:3;
```

#### （6）首行缩进

- 一般用于中文段落的首行，首行需要缩进两个中文字符`text-indent:2em`

#### （7）垂直对齐方式

`vertiacl-align`针对的是内联元素左右的文本和内联元素与自己的垂直对齐方式，块级无效。

* `img`标签默认`vertiacl-align:baseline`基线对齐
* `vertical-align: top`顶部对齐
* `vertical-align: bottom`底部对齐
* `vertical-align: middle`居中对齐

### 3.14 过渡

下表列出了所有的过渡属性:

| 属性                                                         | 描述                                         | CSS  |
| :----------------------------------------------------------- | :------------------------------------------- | :--- |
| [transition](https://www.runoob.com/cssref/css3-pr-transition.html) | 简写属性，用于在一个属性中设置四个过渡属性。 | 3    |
| [transition-property](https://www.runoob.com/cssref/css3-pr-transition-property.html) | 规定应用过渡的 CSS 属性的名称。              | 3    |
| [transition-duration](https://www.runoob.com/cssref/css3-pr-transition-duration.html) | 定义过渡效果花费的时间。默认是 0。           | 3    |
| [transition-timing-function](https://www.runoob.com/cssref/css3-pr-transition-timing-function.html) | 规定过渡效果的时间曲线。默认是 "ease"。      | 3    |
| [transition-delay](https://www.runoob.com/cssref/css3-pr-transition-delay.html) | 规定过渡效果何时开始。默认是 0。             | 3    |

#### （1）transition

- 简写属性，用于在一个属性中设置四个过渡属性`transition-property`、`transition-duration`、`transition-timing-function`、`transition-delay`。
-  始终指定transition-duration属性，否则持续时间为0，transition不会有任何效果。
-  `transition`过渡的简写值只有过渡时间和延迟时间同时出现是，它们必须是过渡时间在前，延迟时间在后，其他属性值都无顺序。
-  使用多组过渡，延迟时间，一定是之前所有组过渡的执行时间的累加
-  可过渡的样式属性：https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_animated_properties

#### （2）transition-property

-  指定CSS属性的name，transition效果

| 值         | 描述                                                  |
| :--------- | :---------------------------------------------------- |
| none       | 没有属性会获得过渡效果。                              |
| all        | 所有属性都将获得过渡效果。                            |
| *property* | 定义应用过渡效果的 CSS 属性名称列表，列表以逗号分隔。 |

#### （3）transition-duration

- 规定完成过渡效果需要花费的时间（以秒或毫秒计）

#### （4）transition-timing-function

- 指定切换效果的速度。
- 默认值为ease，常用linear
- 贝塞尔曲线在线调整：https://cubic-bezier.com/

| 值                            | 描述                                                         |
| :---------------------------- | :----------------------------------------------------------- |
| linear                        | 规定以相同速度开始至结束的过渡效果（等于 cubic-bezier(0,0,1,1)）。 |
| ease                          | 规定慢速开始，然后变快，然后慢速结束的过渡效果（cubic-bezier(0.25,0.1,0.25,1)）。 |
| ease-in                       | 规定以慢速开始的过渡效果（等于 cubic-bezier(0.42,0,1,1)）。  |
| ease-out                      | 规定以慢速结束的过渡效果（等于 cubic-bezier(0,0,0.58,1)）。  |
| ease-in-out                   | 规定以慢速开始和结束的过渡效果（等于 cubic-bezier(0.42,0,0.58,1)）。 |
| cubic-bezier(*n*,*n*,*n*,*n*) | 在 cubic-bezier 函数中定义自己的值。可能的值是 0 至 1 之间的数值。 |

#### （5）transition-delay

- 指定何时将开始切换效果
- 值是指以秒为单位（S）或毫秒（ms）

### 3.14 变换

> CSS**`transform`**属性允许你旋转，缩放，倾斜或平移给定元素。这是通过修改CSS视觉格式化模型的坐标空间来实现的。

下表列出了所有的转换属性：

| 属性                                                         | 描述                                   | CSS  |
| :----------------------------------------------------------- | :------------------------------------- | :--- |
| [transform](https://www.runoob.com/cssref/css3-pr-transform.html) | 向元素应用 2D 或 3D 转换。             | 3    |
| [transform-origin](https://www.runoob.com/cssref/css3-pr-transform-origin.html) | 允许你改变被转换元素的位置。           | 3    |
| [transform-style](https://www.runoob.com/cssref/css3-pr-transform-style.html) | 规定被嵌套元素如何在 3D 空间中显示。   | 3    |
| [perspective](https://www.runoob.com/cssref/css3-pr-perspective.html) | 规定 3D 元素的透视效果。               | 3    |
| [perspective-origin](https://www.runoob.com/cssref/css3-pr-perspective-origin.html) | 规定 3D 元素的底部位置。               | 3    |
| [backface-visibility](https://www.runoob.com/cssref/css3-pr-backface-visibility.html) | 定义元素在不面对屏幕时是否可见。（3D） | 3    |

**2D 转换方法**

| 函数                            | 描述                                     |
| :------------------------------ | :--------------------------------------- |
| matrix(*n*,*n*,*n*,*n*,*n*,*n*) | 定义 2D 转换，使用六个值的矩阵。         |
| translate(*x*,*y*)              | 定义 2D 转换，沿着 X 和 Y 轴移动元素。   |
| translateX(*n*)                 | 定义 2D 转换，沿着 X 轴移动元素。        |
| translateY(*n*)                 | 定义 2D 转换，沿着 Y 轴移动元素。        |
| scale(*x*,*y*)                  | 定义 2D 缩放转换，改变元素的宽度和高度。 |
| scaleX(*n*)                     | 定义 2D 缩放转换，改变元素的宽度。       |
| scaleY(*n*)                     | 定义 2D 缩放转换，改变元素的高度。       |
| rotate(*angle*)                 | 定义 2D 旋转，在参数中规定角度。         |
| skew(*x-angle*,*y-angle*)       | 定义 2D 倾斜转换，沿着 X 和 Y 轴。       |
| skewX(*angle*)                  | 定义 2D 倾斜转换，沿着 X 轴。            |
| skewY(*angle*)                  | 定义 2D 倾斜转换，沿着 Y 轴。            |

**3D 转换方法**

| 函数                                                         | 描述                                      |
| :----------------------------------------------------------- | :---------------------------------------- |
| matrix3d(*n*,*n*,*n*,*n*,*n*,*n*, *n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*) | 定义 3D 转换，使用 16 个值的 4x4 矩阵。   |
| translate3d(*x*,*y*,*z*)                                     | 定义 3D 转化。                            |
| translateX(*x*)                                              | 定义 3D 转化，仅使用用于 X 轴的值。       |
| translateY(*y*)                                              | 定义 3D 转化，仅使用用于 Y 轴的值。       |
| translateZ(*z*)                                              | 定义 3D 转化，仅使用用于 Z 轴的值。       |
| scale3d(*x*,*y*,*z*)                                         | 定义 3D 缩放转换。                        |
| scaleX(*x*)                                                  | 定义 3D 缩放转换，通过给定一个 X 轴的值。 |
| scaleY(*y*)                                                  | 定义 3D 缩放转换，通过给定一个 Y 轴的值。 |
| scaleZ(*z*)                                                  | 定义 3D 缩放转换，通过给定一个 Z 轴的值。 |
| rotate3d(*x*,*y*,*z*,*angle*)                                | 定义 3D 旋转。                            |
| rotateX(*angle*)                                             | 定义沿 X 轴的 3D 旋转。                   |
| rotateY(*angle*)                                             | 定义沿 Y 轴的 3D 旋转。                   |
| rotateZ(*angle*)                                             | 定义沿 Z 轴的 3D 旋转。                   |
| perspective(*n*)                                             | 定义 3D 转换元素的透视视图。              |

#### （1）transform

- 当元素使用了`transform`变换属性发生变换时。元素的基点（参照变换的点）是默认元素的中心点
- 不脱离文档流，只要是移动到了或者遮盖到了其他元素的位置，不会影响其他元素位置，从而导致布局错乱。出现遮盖，出现堆叠。
- 内联元素使用变换属性无效，除了`img`
- 在变换属性中使用百分比的值，针对的是自身的宽度和高度
- 想用多个,需要将多个函数用空格链接的方法放在`transform`值的位置。有先后顺序，从左向右执行。

#### （2）translate(*x*,*y*)

* `transform: translateX(20px);`x轴方向的平移，正值向右平移，负值向左平移
* `transform: translateY(-30px);`y轴方向的平移，正值向下平移，负值向上平移
* `transform: translate(100px,50px);`双方向均可以平移，第一个值x轴，第二个值y轴
* `transform: translate(150px);`如果只写一个值，默认是x轴平移

#### （3）rotate(*angle*)

>  `rotate()`可以让元素产生一个角度的旋转，当元素旋转的时候，旋转的基点是元素的中心点。使用角度单位deg。

* `transform: rotate(-30deg);`函数中在二维空间中默认指z轴，正值顺时针旋转，负值逆时针旋转
* `transform: rotateX(-30deg);`x轴（水平）旋转，正值向前扑，负值向右躺
* `transform: rotateY(30deg);`y轴（垂直）旋转

#### （4） scale(*x*,*y*)   注：仅对block生效

> `scale()`让元素进行放大和缩小，使用比例，无需单位。

* 元素放大，比1大的数字
  * `transform: scaleX(2);`x轴放大
  * `transform: scaleY(2);`y轴放大
  * `transform: scale(1.2);`x轴y轴都同时放大
* 元素缩小，比1小比0大的数字
  * `transform: scaleX(0.5);`x轴缩小
  * `transform: scaleY(0.5);`y轴缩小
  * `transform: scale(0.5);`x轴和y轴同时缩小
* 元素缩小到消失，使用0值`transform: scale(0);`
* 翻转效果，使用负号可使元素发生镜面翻转
  * `transform: scaleX(-1);`x轴镜面翻转
  * `transform: scaleY(-1);`y轴镜面翻转
  * `transform: scale(-1);`双方向镜面翻转

#### （5）skew(*x-angle*,*y-angle*)

> skew使用的是角度值，可以为正值或者负值

* `transform: skewX(-40deg);`x轴的扭曲
* `transform: skewY(-30deg);`y轴的扭曲
* `transform: skew(50deg,30deg);`x轴和y轴一起扭曲
* `transform: skew(50deg);`如果只写一个值，默认为x轴扭曲

#### （6）变换的基点位置

> `transform-origin`，默认是`center`，即 50% 50% 0
>
> 可以使用关键词和百分比切换基地的位置。
>
> 语法： transform-origin: *x-axis y-axis z-axis*;

| 值     | 描述                                                         |
| :----- | :----------------------------------------------------------- |
| x-axis | 定义视图被置于 X 轴的何处。可能的值：left  center  right  *length*  *%* |
| y-axis | 定义视图被置于 Y 轴的何处。可能的值：top  center    bottom  *length*  *%* |
| z-axis | 定义视图被置于 Z 轴的何处。可能的值：*length*                |

### 3.15 动画

下面的表格列出了 @keyframes 规则和所有动画属性：

| 属性                                                         | 描述                                                         | CSS  |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :--- |
| [@keyframes](https://www.runoob.com/cssref/css3-pr-animation-keyframes.html) | 规定动画。                                                   | 3    |
| [animation](https://www.runoob.com/cssref/css3-pr-animation.html) | 所有动画属性的简写属性。                                     | 3    |
| [animation-name](https://www.runoob.com/cssref/css3-pr-animation-name.html) | 规定 @keyframes 动画的名称。                                 | 3    |
| [animation-duration](https://www.runoob.com/cssref/css3-pr-animation-duration.html) | 规定动画完成一个周期所花费的秒或毫秒。默认是 0。             | 3    |
| [animation-timing-function](https://www.runoob.com/cssref/css3-pr-animation-timing-function.html) | 规定动画的速度曲线。默认是 "ease"。                          | 3    |
| [animation-fill-mode](https://www.runoob.com/cssref/css3-pr-animation-fill-mode.html) | 规定当动画不播放时（当动画完成时，或当动画有一个延迟未开始播放时），要应用到元素的样式。 | 3    |
| [animation-delay](https://www.runoob.com/cssref/css3-pr-animation-delay.html) | 规定动画何时开始。默认是 0。                                 | 3    |
| [animation-iteration-count](https://www.runoob.com/cssref/css3-pr-animation-iteration-count.html) | 规定动画被播放的次数。默认是 1。                             | 3    |
| [animation-direction](https://www.runoob.com/cssref/css3-pr-animation-direction.html) | 规定动画是否在下一周期逆向地播放。默认是 "normal"。          | 3    |
| [animation-play-state](https://www.runoob.com/cssref/css3-pr-animation-play-state.html) | 规定动画是否正在运行或暂停。默认是 "running"。               | 3    |

#### （1）关键帧

```css
    @keyframes move {
      /* 准备运动但还没动，有一个样式 */
      0% {transform: translateX(0);}
      /* 动完了最后的动作 */
      100% {transform: translateX(300px);}
    }
```

**注意事项：**

* `@keyframes` 使用关键帧规则
* 关键帧的名字，不能用数字开头，尽量见名知意
* `{}`包裹所有的执行阶段
* from等同于0%，to到某个阶段，不如使用百分比更好控制阶段，0%起始状态，100%结束状态。
* 默认动画之行完毕后，会自动回到起始状态
* 在某个阶段可以设置多个css样式属性

#### （2）动画属性的拆分

* `animation-name:关键帧的名字`，必写
* `animation-duration: 动画的执行时间;`时间单位s，必写
* `animation-timing-function: ease;`动画的执行方式，和过渡的执行方式一样，同样可以应用贝塞尔曲线，默认`ease`，匀速`linear`
* `animation-delay: 延迟执行动画的时间;`时间单位s
* `animation-iteration-count: 1;`执行次数不用加单位，默认1次，`infinite`无限次
* `animation-fill-mode: backwards;`默认回到初始位置，有时需要动画之行完，元素停留在终点位置`forwards`
* `animation-direction: normal;执行动画的顺序（序列）默认顺序执行，反顺序执行`reverse`
* `animation-play-state: running;`动画是否为播放状态，默认运行（播放）`running`,动画暂停状态`paused`。一般情况下，可以通过伪类的参与，通过用户触发动画的暂停。

#### （3）动画的简写

* 动画的简写直接写`animation`属性，后面所有的值用空格链接。

* 顺序只有两个值有顺序，动画执行时间和动画延迟时间，必须是执行时间在前，如果只有一个时间的值，默认为执行时间。
* 最简：执行关键帧的名字和执行时间

```css
/*顺序只有时间是有顺序的，其他都可以颠倒顺序*/
animation: name duration timing-function delay iteration-count direction fill-mode;
/*最简写法:执行关键帧的名字，执行时间*/
animation: name duration;
```

****

### 3.16 计数器

| 属性                                                         | 描述                                                |
| :----------------------------------------------------------- | :-------------------------------------------------- |
| [content](https://www.runoob.com/cssref/pr-gen-content.html) | 使用 ::before 和 ::after 伪元素来插入自动生成的内容 |
| [counter-increment](https://www.runoob.com/cssref/pr-gen-counter-increment.html) | 递增一个或多个值                                    |
| [counter-reset](https://www.runoob.com/cssref/pr-gen-counter-reset.html) | 创建或重置一个或多个计数器                          |

以下实例在页面创建一个计数器，在每一个 <h1> 元素前添加计数值 "Section <*主标题计数值*>.", 嵌套的计数值则放在 <h2> 元素的前面，内容为 "<*主标题计数值*>.<*副标题计数值*>":

```css
body {
  counter-reset: section;
}
 
h1 {
  counter-reset: subsection;
}
 
h1::before {
  counter-increment: section;
  content: "Section " counter(section) ". ";
}
 
h2::before {
  counter-increment: subsection;
  content: counter(section) "." counter(subsection) " ";
}
```

计数器也可用于列表中，列表的子元素会自动创建。这里我们使用了 `counters()` 函数在不同的嵌套层级中插入字符串:

```css
ol {
  counter-reset: section;
  list-style-type: none;
}
 
li::before {
  counter-increment: section;
  content: counters(section,".") " ";
}
```

### 3.17 多列

下表列出了所有 CSS3 的多列属性：

| 属性                                                         | 描述                                      |
| :----------------------------------------------------------- | :---------------------------------------- |
| [column-count](https://www.runoob.com/cssref/css3-pr-column-count.html) | 指定元素应该被分割的列数。                |
| [column-fill](https://www.runoob.com/cssref/css3-pr-column-fill.html) | 指定如何填充列                            |
| [column-gap](https://www.runoob.com/cssref/css3-pr-column-gap.html) | 指定列与列之间的间隙                      |
| [column-rule](https://www.runoob.com/cssref/css3-pr-column-rule.html) | 所有 column-rule-* 属性的简写             |
| [column-rule-color](https://www.runoob.com/cssref/css3-pr-column-rule-color.html) | 指定两列间边框的颜色                      |
| [column-rule-style](https://www.runoob.com/cssref/css3-pr-column-rule-style.html) | 指定两列间边框的样式                      |
| [column-rule-width](https://www.runoob.com/cssref/css3-pr-column-rule-width.html) | 指定两列间边框的厚度                      |
| [column-span](https://www.runoob.com/cssref/css3-pr-column-span.html) | 指定元素要跨越多少列                      |
| [column-width](https://www.runoob.com/cssref/css3-pr-column-width.html) | 指定列的宽度                              |
| [columns](https://www.runoob.com/cssref/css3-pr-columns.html) | column-width 与 column-count 的简写属性。 |

### 3.18 用户界面

**新的用户界面特性**

| 属性                                                         | 说明                                           | CSS  |
| :----------------------------------------------------------- | :--------------------------------------------- | :--- |
| [appearance](https://www.runoob.com/cssref/css3-pr-appearance.html) | 允许您使一个元素的外观像一个标准的用户界面元素 | 3    |
| [box-sizing](https://www.runoob.com/cssref/css3-pr-box-sizing.html) | 允许你以适应区域而用某种方式定义某些元素       | 3    |
| [icon](https://www.runoob.com/cssref/css3-pr-icon.html)      | 为创作者提供了将元素设置为图标等价物的能力。   | 3    |
| [nav-down](https://www.runoob.com/cssref/css3-pr-nav-down.html) | 指定在何处使用箭头向下导航键时进行导航         | 3    |
| [nav-index](https://www.runoob.com/cssref/css3-pr-nav-index.html) | 指定一个元素的Tab的顺序                        | 3    |
| [nav-left](https://www.runoob.com/cssref/css3-pr-nav-left.html) | 指定在何处使用左侧的箭头导航键进行导航         | 3    |
| [nav-right](https://www.runoob.com/cssref/css3-pr-nav-right.html) | 指定在何处使用右侧的箭头导航键进行导航         | 3    |
| [nav-up](https://www.runoob.com/cssref/css3-pr-nav-up.html)  | 指定在何处使用箭头向上导航键时进行导航         | 3    |
| [outline-offset](https://www.runoob.com/cssref/css3-pr-outline-offset.html) | 外轮廓修饰并绘制超出边框的边缘                 | 3    |
| [resize](https://www.runoob.com/cssref/css3-pr-resize.html)  | 指定一个元素是否是由用户调整大小               | 3    |

### 3.19 网格布局

**CSS 网格属性**

| 属性                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [column-gap](https://www.runoob.com/cssref/css3-pr-column-gap.html) | 指定列之间的间隙                                             |
| [gap](https://www.runoob.com/cssref/css3-pr-gap.html)        | *row-gap* 和 *column-gap* 的简写属性                         |
| [grid](https://www.runoob.com/cssref/css-pr-grid.html)       | *grid-template-rows, grid-template-columns, grid-template-areas, grid-auto-rows, grid-auto-columns*, 以及 *grid-auto-flow* 的简写属性 |
| [grid-area](https://www.runoob.com/cssref/pr-grid-area.html) | 指定网格元素的名称，或者也可以是 *grid-row-start*, *grid-column-start*, *grid-row-end*, 和 *grid-column-end* 的简写属性 |
| [grid-auto-columns](https://www.runoob.com/cssref/pr-grid-auto-columns.html) | 指的默认的列尺寸                                             |
| [grid-auto-flow](https://www.runoob.com/cssref/pr-grid-auto-flow.html) | 指定自动布局算法怎样运作，精确指定在网格中被自动布局的元素怎样排列。 |
| [grid-auto-rows](https://www.runoob.com/cssref/pr-grid-auto-rows.html) | 指的默认的行尺寸                                             |
| [grid-column](https://www.runoob.com/cssref/pr-grid-column.html) | *grid-column-start* 和 *grid-column-end* 的简写属性          |
| [grid-column-end](https://www.runoob.com/cssref/pr-grid-column-end.html) | 指定网格元素列的结束位置                                     |
| [grid-column-gap](https://www.runoob.com/cssref/pr-grid-column-gap.html) | 指定网格元素的间距大小                                       |
| [grid-column-start](https://www.runoob.com/cssref/pr-grid-column-start.html) | 指定网格元素列的开始位置                                     |
| [grid-gap](https://www.runoob.com/cssref/pr-grid-gap.html)   | *grid-row-gap* 和 *grid-column-gap* 的简写属性               |
| [grid-row](https://www.runoob.com/cssref/pr-grid-row.html)   | *grid-row-start* 和 *grid-row-end* 的简写属性                |
| [grid-row-end](https://www.runoob.com/cssref/pr-grid-row-end.html) | 指定网格元素行的结束位置                                     |
| [grid-row-gap](https://www.runoob.com/cssref/pr-grid-row-gap.html) | 指定网格元素的行间距                                         |
| [grid-row-start](https://www.runoob.com/cssref/pr-grid-row-start.html) | 指定网格元素行的开始位置                                     |
| [grid-template](https://www.runoob.com/cssref/pr-grid-template.html) | *grid-template-rows*, *grid-template-columns* 和 *grid-areas* 的简写属性 |
| [grid-template-areas](https://www.runoob.com/cssref/pr-grid-template-areas.html) | 指定如何显示行和列，使用命名的网格元素                       |
| [grid-template-columns](https://www.runoob.com/cssref/pr-grid-template-columns.html) | 指定列的大小，以及网格布局中设置列的数量                     |
| [grid-template-rows](https://www.runoob.com/cssref/pr-grid-template-rows.html) | 指定网格布局中行的大小                                       |
| [row-gap](https://www.runoob.com/cssref/css3-pr-row-gap.html) | 指定两个行之间的间距                                         |

### 3.20 css3弹性盒子

下表列出了在弹性盒子中常用到的属性:

| 属性                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [display](https://www.runoob.com/cssref/pr-class-display.html) | 指定 HTML 元素盒子类型。                                     |
| [flex-direction](https://www.runoob.com/cssref/css3-pr-flex-direction.html) | 指定了弹性容器中子元素的排列方式                             |
| [justify-content](https://www.runoob.com/cssref/css3-pr-justify-content.html) | 设置弹性盒子元素在主轴（横轴）方向上的对齐方式。             |
| [align-items](https://www.runoob.com/cssref/css3-pr-align-items.html) | 设置弹性盒子元素在侧轴（纵轴）方向上的对齐方式。             |
| [flex-wrap](https://www.runoob.com/cssref/css3-pr-flex-wrap.html) | 设置弹性盒子的子元素超出父容器时是否换行。                   |
| [align-content](https://www.runoob.com/cssref/css3-pr-align-content.html) | 修改 flex-wrap 属性的行为，类似 align-items, 但不是设置子元素对齐，而是设置行对齐 |
| [flex-flow](https://www.runoob.com/cssref/css3-pr-flex-flow.html) | flex-direction 和 flex-wrap 的简写                           |
| [order](https://www.runoob.com/cssref/css3-pr-order.html)    | 设置弹性盒子的子元素排列顺序。                               |
| [align-self](https://www.runoob.com/cssref/css3-pr-align-self.html) | 在弹性子元素上使用。覆盖容器的 align-items 属性。            |
| [flex](https://www.runoob.com/cssref/css3-pr-flex.html)      | 设置弹性盒子的子元素如何分配空间。                           |

## 4 布局

### 4.1 流式布局

> "文档流"或"流式布局"是在对布局进行任何更改之前，在页面上显示"块"和"内联"元素的方式。在文档流中，内联元素按内联方向显示，即词语在依据文件写作模式的句子中表示的方向。块元素则一个接一个地显示，就像该文档的写作模式中的段落一样。 

| 块元素                 | 内联元素                                           | 内联中的行内块                                     |
| ---------------------- | -------------------------------------------------- | -------------------------------------------------- |
| display:block          | display:inline                                     | display:inline-block                               |
| 默认有宽度，父级的100% | 默认的宽高受内容文字的影响                         | 受内容和默认样式的                                 |
| 宽度高度设置生效       | 宽度高度设置不生效                                 | 宽度高度设置生效                                   |
| 从上向下排列           | 从左向右排列（参照父级边界）超过父级边界会换行显示 | 从左向右排列（参照父级边界）超过父级边界会换行显示 |
| 无幽灵节点             | 有幽灵节点                                         | 有幽灵节点                                         |

### 4.2 弹性盒子布局

> **CSS 弹性盒子布局**是 CSS 的模块之一，定义了一种针对用户界面设计而优化的 CSS 盒子模型。在弹性布局模型中，弹性容器的子元素可以在任何方向上排布，也可以“弹性伸缩”其尺寸，既可以增加尺寸以填满未使用的空间，也可以收缩尺寸以避免父元素溢出。子元素的水平对齐和垂直对齐都能很方便的进行操控。通过嵌套这些框（水平框在垂直框内，或垂直框在水平框内）可以在两个维度上构建布局。

#### 4.2.1 flexbox

```css
/*
创建弹性盒子
1.容器和项目
- 使用`display:flex`的父级元素叫做“容器”（flex容器），在容器中使用的相关属性叫“容器属性”
- 容器中的第一层子元素，受控于容器的元素叫做"项目"（或flex元素）,使用项目的相关属性叫"项目属性"
2.注意事项
- 子元素是依赖容器元素，控制子元素排列，不再依靠子元素的`float`
- 设置的父元素为弹性盒，子元素的`float`将失效
- 切记不要把`flex`与浮动布局与定位布局一起使用
- 使用了`display:flex`,其子元素将块状化（因为flex的底层其实是浮动，只不过帮你封装了）
*/

div {
    display : flex;
}
```

#### 4.2.2 主轴和交叉轴

##### （1）主轴和交叉轴

* 主轴，先要看是行模式还是列模式。
  * 行模式的主轴是水平方向的
  * 列模式的主轴是垂直方向的
* 交叉轴，就是垂直于主轴的轴线

##### （2）主轴的排序

* `flex-direction: row;`默认行模式
* `flex-direction: row-reverse`行模式的反向排序
* `flex-direction: column;`正向的列模式
* `flex-direction: column-reverse;`反向的列模式

#### 4.2.3 换行

`flex-wrap`控制项目在容器中是否换行显示，默认不换行，容器空间不足时，项目等比例压缩。

* `flex-wrap: nowrap;`不换行默认的
* `flex-wrap: wrap;`换行
* `flex-wrap: wrap-reverse;`反向换行

#### 4.2.4 主轴排序和项目换行的简写

`flex-flow`简写属性，第一个值是主轴排序，第二个值是是否换行。

```css
/*常用写法 横向 换行*/
flex-flow: row wrap;
```

#### 4.2.5 主轴上的对齐方式

`justify-content`定义项目在主轴上的对齐方式，注意需要区别行模式和列模式，在渲染之前，会先找到项目的排列方式再做渲染。

* `justify-content: flex-start;`主轴的起点对齐
* `justify-content: flex-end;`主轴的终点对齐
* `justify-content: center;`主轴居中对齐
* `justify-content: space-between;`主轴两端对齐，每行第一个贴容器起点，每行最后一个贴容器终点，其它富裕空间均分
* `justify-content: space-around;`均匀排列每个元素周围的间距相等，每个元素一臂间隔，遇到相邻元素，就成了两臂间隔
* `justify-content: space-evenly;`每个项目元素之间的距离相等，均分所有空间

#### 4.2.6 交叉轴对齐方式

`align-items`指的项目在交叉轴对齐的方式，但是有前提，交叉轴要有富裕的空间。优先考虑已知项目数量的布局。

* `align-items: flex-start;`交叉轴的起点对齐
* `align-items: flex-end;`交叉轴的终点对齐
* `align-items: center;`交叉轴的居中对齐
* `align-items: stretch;`默认值，拉伸以填满flex容器

#### 4.2.7 多行的交叉轴对齐

多行显示的前提，有换行`flex-wrap: wrap;`，还要在交叉轴上有多余的空间。

* `align-content: flex-start;`交叉轴多行起点对齐
* `align-content: flex-end;`交叉轴多行终点对齐

* `align-content: center;`多轴线交叉轴居中对齐
* `align-content: space-between;`多轴线交叉轴两端对齐
* `align-content: space-around;`多轴线两侧距离相等，相邻行出现两倍距离
* `align-content: space-evenly;`平均分配多轴线交叉轴上的空间

#### 4.2.8 项目属性

##### （1）flex

`flex`写形式允许你把三个数值按这个顺序书写 — `flex-grow`，`flex-shrink`，`flex-basis`。****

-  `flex-grow` 属性可以按比例分配剩余空间。

   -  负值无效，默认为0，正值按比例分配剩余空间。
   -  例如三个元素中，第一个元素 `flex-grow` 值为2， 其他元素值为1，则第一个元素将占有2/4。
-  `flex-shrink`属性是处理flex元素收缩的问题。

   -  默认值是1，不能为负值，0代表不压缩
   -  如果我们的容器中没有足够排列flex元素的空间（项目不能换行），那么可以把flex元素`flex-shrink`属性设置为正整数来缩小它所占空间到`flex-basis`以下。
-  `flex-basis` 定义了该元素的**空间大小（**the size of that item in terms of the space**）**。
   -  该属性的默认值是 `auto` 
   -  当元素设定了宽度（width）时， `flex-basis` 的值等同。如果没有给元素设定尺寸，`flex-basis` 的值采用元素内容的尺寸。
-  `flex`常用值
   -   `flex: initial`是把flex元素重置为Flexbox的初始值，它相当于 `flex: 0 1 auto`。flex元素不会超过它们 `flex-basis` 的尺寸。
   -  `flex: auto` 等同于 `flex: 1 1 auto`；和上面的 `flex:initial` 基本相同，但是这种情况下，flex元素在需要的时候既可以拉伸也可以收缩。
   -  `flex: none` 可以把flex元素设置为不可伸缩。它和设置为 `flex: 0 0 auto` 是一样的。
   -  `flex: 1` 放大比例
   -  `flex: 0 0 ??px` 不放大不缩小，尺寸定义为...

##### （2）order

- order可以有负值，默认为0
- order越大，排列越前

### 4.3 网格布局

> 网格是一组相交的水平线和垂直线，它定义了网格的列和行。
>
> CSS 提供了一个基于网格的布局系统，带有行和列，可以让我们更轻松地设计网页，而无需使用浮动和定位。
>
> 轨道可以使用任何长度单位进行定义。网格引入了 **fr** 单位来帮助我们创建灵活的网格轨道。一个 fr 单位代表网格容器中可用空间的一等份。

| 属性                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [column-gap](https://www.runoob.com/cssref/css3-pr-column-gap.html) | 指定列之间的间隙                                             |
| [gap](https://www.runoob.com/cssref/css3-pr-gap.html)        | *row-gap* 和 *column-gap* 的简写属性                         |
| [grid](https://www.runoob.com/cssref/css-pr-grid.html)       | *grid-template-rows, grid-template-columns, grid-template-areas, grid-auto-rows, grid-auto-columns*, 以及 *grid-auto-flow* 的简写属性 |
| [grid-area](https://www.runoob.com/cssref/pr-grid-area.html) | 指定网格元素的名称，或者也可以是 *grid-row-start*, *grid-column-start*, *grid-row-end*, 和 *grid-column-end* 的简写属性 |
| [grid-auto-columns](https://www.runoob.com/cssref/pr-grid-auto-columns.html) | 指的默认的列尺寸                                             |
| [grid-auto-flow](https://www.runoob.com/cssref/pr-grid-auto-flow.html) | 指定自动布局算法怎样运作，精确指定在网格中被自动布局的元素怎样排列。 |
| [grid-auto-rows](https://www.runoob.com/cssref/pr-grid-auto-rows.html) | 指的默认的行尺寸                                             |
| [grid-column](https://www.runoob.com/cssref/pr-grid-column.html) | *grid-column-start* 和 *grid-column-end* 的简写属性          |
| [grid-column-end](https://www.runoob.com/cssref/pr-grid-column-end.html) | 指定网格元素列的结束位置                                     |
| [grid-column-gap](https://www.runoob.com/cssref/pr-grid-column-gap.html) | 指定网格元素的间距大小                                       |
| [grid-column-start](https://www.runoob.com/cssref/pr-grid-column-start.html) | 指定网格元素列的开始位置                                     |
| [grid-gap](https://www.runoob.com/cssref/pr-grid-gap.html)   | *grid-row-gap* 和 *grid-column-gap* 的简写属性               |
| [grid-row](https://www.runoob.com/cssref/pr-grid-row.html)   | *grid-row-start* 和 *grid-row-end* 的简写属性                |
| [grid-row-end](https://www.runoob.com/cssref/pr-grid-row-end.html) | 指定网格元素行的结束位置                                     |
| [grid-row-gap](https://www.runoob.com/cssref/pr-grid-row-gap.html) | 指定网格元素的行间距                                         |
| [grid-row-start](https://www.runoob.com/cssref/pr-grid-row-start.html) | 指定网格元素行的开始位置                                     |
| [grid-template](https://www.runoob.com/cssref/pr-grid-template.html) | *grid-template-rows*, *grid-template-columns* 和 *grid-areas* 的简写属性 |
| [grid-template-areas](https://www.runoob.com/cssref/pr-grid-template-areas.html) | 指定如何显示行和列，使用命名的网格元素                       |
| [grid-template-columns](https://www.runoob.com/cssref/pr-grid-template-columns.html) | 指定列的大小，以及网格布局中设置列的数量                     |
| [grid-template-rows](https://www.runoob.com/cssref/pr-grid-template-rows.html) | 指定网格布局中行的大小                                       |
| [row-gap](https://www.runoob.com/cssref/css3-pr-row-gap.html) | 指定两个行之间的间距                                         |

#### 4.3.1 网格容器

（1）`display:grid`

```css
/*要使 HTML 元素变成一个网格容器，可以将 display 属性设置为 grid 或 inline-grid。
网格容器内放置着由列和行内组成的网格元素。*/
.grid-container {
  display: grid;
}
```

（2）`grid-template-columns`属性

```css
/*grid-template-columns 属性定义了网格布局中的列的数量，它也可以设置每个列的宽度。
属性值是一个以空格分隔的列表，其中每个值定义相对应列的宽度*/
.grid-container {
  display: grid;
  grid-template-columns: auto auto auto auto;
}

.grid-container {
  display: grid;
  grid-template-columns: 80px 200px auto 40px;
}
```

（3）`grid-template-rows`属性

```css
/*grid-template-rows 属性设置每一行的高度。
属性值是一个以空格分隔的列表，其中每个值定义相对应行的高度*/
.grid-container {
  display: grid;
  grid-template-rows: 80px 200px;
}
```

（4）`justify-content`属性

```css
/*justify-content 属性用于对齐容器内的网格，设置如何分配顺着弹性容器主轴(或者网格行轴) 的元素之间及其周围的空间。注意：网格的总宽度必须小于容器的宽度才能使 justify-content 属性生效。*/
.grid-container {
  display: grid;
  justify-content: space-evenly;
}
```

（5）`align-content`属性

```css
/*align-content 属性用于设置垂直方向上的网格元素在容器中的对齐方式。
注意：网格元素的总高度必须小于容器的高度才能使 align-content 属性生效。*/
.grid-container {
  display: grid;
  height: 400px;
  align-content: center;
}
```

#### 4.3.2 网格元素

（1）`grid-column`属性

```css
/*grid-column 属性定义了网格元素列的开始和结束位置。
注意： grid-column 是 grid-column-start 和 grid-column-end 属性的简写属性。
我们可以参考行号来设置网格元素，也可以使用关键字 "span" 来定义元素将跨越的列数。*/
.item1 {
  grid-column: 1 / 5;
}

.item1 {
  grid-column: 1 / span 3;
}
```

（2）`grid-row`属性

```css
/*grid-row 属性定义了网格元素行的开始和结束位置。
注意： grid-row 是 grid-row-start 和 grid-row-end 属性的简写属性。
我们可以参考行号来设置网格元素，也可以使用关键字 "span" 来定义元素将跨越的行数。*/
.item1 {
  grid-row: 1 / 4;
}

.item1 {
  grid-row: 1 / span 2;
}
```

（3）`grid-area`属性

```css
/*grid-area 属性是 grid-row-start, grid-column-start, grid-row-end 以及 grid-column-end 属性的简写。*/
.item8 {
  grid-area: 1 / 2 / 5 / 6;
}

.item8 {
  grid-area: 2 / 1 / span 2 / span 3;
}
```

（4）网格元素命名

```css
/*grid-area 属性可以对网格元素进行命名。
命名的网格元素可以通过容器的 grid-template-areas 属性来引用。*/
.item1 {
  grid-area: myArea;
}
.grid-container {
  grid-template-areas: 'myArea myArea myArea myArea myArea';
}
/*每行由单引号内 ' ' 定义，以空格分隔。
. 号表示没有名称的网格项。*/
.item1 {
  grid-area: myArea;
}
.grid-container {
  grid-template-areas: 'myArea myArea . . .';
}
/*要定义两行，请在另一组单引号内 ' ' 定义第二行的列。
命名所有网格元素，并制作一个网页模板：*/
.item1 { grid-area: header; }
.item2 { grid-area: menu; }
.item3 { grid-area: main; }
.item4 { grid-area: right; }
.item5 { grid-area: footer; }
 
.grid-container {
  grid-template-areas:
    'header header header header header header'
    'menu main main main right right'
    'menu footer footer footer footer footer';
}
```

（5）网格元素的顺序

```css
/*网格布局允许我们将网格元素放置在我们喜欢的任何地方。
HTML 代码中的第一元素不一定非要显示为网格中元素的第一项。*/
.item1 { grid-area: 1 / 3 / 2 / 4; }
.item2 { grid-area: 2 / 3 / 3 / 4; }
.item3 { grid-area: 1 / 1 / 2 / 2; }
.item4 { grid-area: 1 / 2 / 2 / 3; }
.item5 { grid-area: 2 / 1 / 3 / 2; }
.item6 { grid-area: 2 / 2 / 3 / 3; }
/*可以使用媒体查询，重新排列在指定屏幕尺寸下的顺序：*/
@media only screen and (max-width: 500px) {
  .item1 { grid-area: 1 / span 3 / 2 / 4; }
  .item2 { grid-area: 3 / 3 / 4 / 4; }
  .item3 { grid-area: 2 / 1 / 3 / 2; }
  .item4 { grid-area: 2 / 2 / span 2 / 3; }
  .item5 { grid-area: 3 / 1 / 4 / 2; }
  .item6 { grid-area: 2 / 3 / 3 / 4; }
}
```



## 5 响应式

### 5.1 响应式的概念

随着移动终端的兴起，多种规格页面出现了，用户各种需求增加。响应式就可以让多种终端，同时看到接近相同的内容。

响应式也叫做“自适应页面”，可以根据浏览器设备的不同（大多指设备的宽度）改变不同的布局，文本，图片的效果。

特点使用一套html结构，根据终端检测变化，同时使用“媒体查询”，将不同宽度的css加入到不同的媒体查询中，从而随着页面宽度的变化，改变布局样式。



### 5.2 设置viewport

用浏览器打开页面，打开手机模式的时候，字会变小。因为页面宽度大于设备的屏幕宽度，所以会整体缩小页面，字体也一起缩小了。

在html中需要，告诉浏览器，需要符合我设备的大小。在`head`标签中加入一个监听设备宽度的标签。

*** meta:vp 然后敲tab键 ***

```css
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

* `width=device-width`视口宽度就等于设备宽度
* `initial-scale=1.0`初始化视口不缩放
* `maximum-scale`：允许用户缩放到的最大比例。
* `minimum-scale`：允许用户缩放到的最小比例。
* `user-scalable`：用户是否可以手动缩放。
* `height`：和 width 相对应，指定高度。

### 5.3 媒体查询

* `@media`媒体查询规则
* `max-width` 最大宽度，不能超过这个值
* `min-width` 最小宽度，不能低于这个值

#### 5.3.1 多媒体查询语法

> 多媒体查询由多种媒体组成，可以包含一个或多个表达式，表达式根据条件是否成立返回 true 或 false。@media not|only mediatype and (expressions) {    CSS 代码...; }
>
> 如果指定的多媒体类型匹配设备类型则查询结果返回 true，文档会在匹配的设备上显示指定样式效果。
>
> 除非你使用了 not 或 only 操作符，否则所有的样式会适应在所有设备上显示效果。

- **not:** not是用来排除掉某些特定的设备的，比如 @media not print（非打印设备）。
- **only:** 用来定某种特别的媒体类型。对于支持Media Queries的移动设备来说，如果存在only关键字，移动设备的Web浏览器会忽略only关键字并直接根据后面的表达式应用样式文件。对于不支持Media Queries的设备但能够读取Media Type类型的Web浏览器，遇到only关键字时会忽略这个样式文件。
- **all:** 所有设备，这个应该经常看到。

**方向: **结合CSS媒体查询,可以创建适应不同设备的方向(横屏landscape、竖屏portrait等)的布局。

```css
@media only screen and (orientation: landscape) {
    body {
        background-color: lightblue;
    }
}
```

#### 5.3.2 CSS3 多媒体类型

| 值     | 描述                             |
| :----- | :------------------------------- |
| all    | 用于所有多媒体类型设备           |
| print  | 用于打印机                       |
| screen | 用于电脑屏幕，平板，智能手机等。 |
| speech | 用于屏幕阅读器                   |

### 5.4 响应式断点的设计原则

响应式核心是适配多种终端，多种终端就具备多种尺寸范围。考虑什么范围下，会出现什么样的终端类型。

先写小屏幕的媒体查询，顺序往大写。

* 手机：小于等于480px，手机竖屏
* 手机&平板：小于等于767px，手机横屏和pad竖屏
* 平板：大于等于768px，平板电脑或者pad横屏
* 默认：大于等于980px，低端显示器
* 大屏幕：大于等于1200px，普通显示器
* 超大屏：大于等于1400px，高清显示器@

```css
  /* 按照屏幕宽度设计媒体查询 */
    /* 手机平板 */
    @media (max-width:767px) {}
    /* 手机 */
    @media (max-width:480px) {}
    /* 平板 */
    @media (min-width:768px) {}
    /* 默认 */
    @media (min-width:980px) {}
    /* 大屏幕 */
    @media (min-width:1200px) {}
    /* 超大屏幕 */
    @media (min-width:1400px) {}
```

### 5.5 相对于视口的尺寸

`vw`(viewport width视口宽度)，`vh`(viewport height视口高度)。参照的是浏览器可视区域的比例大小，不含任务栏，不含工作栏，不含浏览器地址栏。

```
1vw == 视口（浏览器可视区域）宽度的1%
1vh == 视口（浏览器可视区域）高度的1%
浏览器可视区域的宽度都是100vw
浏览器可视区域的高度都是100vh
```

### 5.6 响应式网格视图

> 响应式网格视图通常是 12 列，宽度为100%，在浏览器窗口大小调整时会自动伸缩。

```css
* {
    box-sizing: border-box;
}
.col-1 {width: 8.33%;}
.col-2 {width: 16.66%;}
.col-3 {width: 25%;}
.col-4 {width: 33.33%;}
.col-5 {width: 41.66%;}
.col-6 {width: 50%;}
.col-7 {width: 58.33%;}
.col-8 {width: 66.66%;}
.col-9 {width: 75%;}
.col-10 {width: 83.33%;}
.col-11 {width: 91.66%;}
.col-12 {width: 100%;}
```

### 5.7 框架

- Bootstrap，来自 Twitter，是目前最受欢迎的前端框架。Bootstrap 是基于 HTML、CSS、JAVASCRIPT 的，它简洁灵活，使得 Web 开发更加快捷。



## 6 CSS 参考手册

### 6.1 CSS函数

| 函数                                                         | 描述                                                         | CSS 版本 |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :------- |
| [attr()](https://www.runoob.com/cssref/func-attr.html)       | 返回选择元素的属性值。                                       | 2        |
| [calc()](https://www.runoob.com/cssref/func-calc.html)       | 允许计算 CSS 的属性值，比如动态计算长度值。                  | 3        |
| [cubic-bezier()](https://www.runoob.com/cssref/func-cubic-bezier.html) | 定义了一个贝塞尔曲线(Cubic Bezier)。                         | 3        |
| [conic-gradient()](https://www.runoob.com/cssref/func-conic-gradient.html) | 定义了一个圆锥渐变。                                         | 3        |
| [counter()](https://www.runoob.com/cssref/func-counter.html) | 设置计数器。                                                 | 3        |
| [hsl()](https://www.runoob.com/cssref/func-hsl.html)         | 使用色相、饱和度、亮度来定义颜色。                           | 3        |
| [hsla()](https://www.runoob.com/cssref/func-hsla.html)       | 使用色相、饱和度、亮度、透明度来定义颜色。                   | 3        |
| [linear-gradient()](https://www.runoob.com/cssref/func-linear-gradient.html) | 创建一个线性渐变的图像                                       | 3        |
| [max()](https://www.runoob.com/cssref/func-max.html)         | 从一个逗号分隔的表达式列表中选择最大的值作为属性的值。       | 3        |
| [min()](https://www.runoob.com/cssref/func-min.html)         | 从一个逗号分隔的表达式列表中选择最小的值作为属性的值。       | 3        |
| [radial-gradient()](https://www.runoob.com/cssref/func-radial-gradient.html) | 用径向渐变创建图像。                                         | 3        |
| [repeating-linear-gradient()](https://www.runoob.com/cssref/func-repeating-linear-gradient.html) | 用重复的线性渐变创建图像。                                   | 3        |
| [repeating-radial-gradient()](https://www.runoob.com/cssref/func-repeating-radial-gradient.html) | 类似 radial-gradient()，用重复的径向渐变创建图像。           | 3        |
| [repeating-conic-gradient()](https://www.runoob.com/cssref/func-repeating-conic-gradient.html) | 重复的圆锥渐变。                                             | 3        |
| [rgb()](https://www.runoob.com/cssref/func-rgb-css.html)     | 使用红(R)、绿(G)、蓝(B)三个颜色的叠加来生成各式各样的颜色。  | 2        |
| [rgba()](https://www.runoob.com/cssref/func-rgba.html)       | 使用红(R)、绿(G)、蓝(B)、透明度(A)的叠加来生成各式各样的颜色。 | 3        |
| [var()](https://www.runoob.com/cssref/func-var.html)         | 用于插入自定义的属性值。                                     | 3        |

### 6.2  CSS选择器

| 选择器                                                       | 示例                                    | 示例说明                                                   | CSS  |
| :----------------------------------------------------------- | :-------------------------------------- | :--------------------------------------------------------- | :--- |
| [.*class*](https://www.runoob.com/cssref/sel-class.html)     | .intro                                  | 选择所有class="intro"的元素                                | 1    |
| [#*id*](https://www.runoob.com/cssref/sel-id.html)           | #firstname                              | 选择所有id="firstname"的元素                               | 1    |
| [*](https://www.runoob.com/cssref/sel-all.html)              | *                                       | 选择所有元素                                               | 2    |
| *[element](https://www.runoob.com/cssref/sel-element.html)*  | p                                       | 选择所有<p>元素                                            | 1    |
| *[element,element](https://www.runoob.com/cssref/sel-element-comma.html)* | div,p                                   | 选择所有<div>元素和<p>元素                                 | 1    |
| [*element* *element*](https://www.runoob.com/cssref/sel-element-element.html) | div p                                   | 选择<div>元素内的所有<p>元素                               | 1    |
| [*element*>*element*](https://www.runoob.com/cssref/sel-element-gt.html) | div>p                                   | 选择所有父级是 <div> 元素的 <p> 元素                       | 2    |
| [*element*+*element*](https://www.runoob.com/cssref/sel-element-pluss.html) | div+p                                   | 选择所有紧跟在 <div> 元素之后的第一个 <p> 元素             | 2    |
| [[*attribute*\]](https://www.runoob.com/cssref/sel-attribute.html) | [target]                                | 选择所有带有target属性元素                                 | 2    |
| [[*attribute*=*value*\]](https://www.runoob.com/cssref/sel-attribute-value.html) | [target=-blank]                         | 选择所有使用target="-blank"的元素                          | 2    |
| [[*attribute*~=*value*\]](https://www.runoob.com/cssref/sel-attribute-value-contains.html) | [title~=flower]                         | 选择标题属性包含单词"flower"的所有元素                     | 2    |
| [[*attribute*\|=*language*\]](https://www.runoob.com/cssref/sel-attribute-value-lang.html) | [lang\|=en]                             | 选择 lang 属性等于 **en**，或者以 **en-** 为开头的所有元素 | 2    |
| [:link](https://www.runoob.com/cssref/sel-link.html)         | a:link                                  | 选择所有未访问链接                                         | 1    |
| [:visited](https://www.runoob.com/cssref/sel-visited.html)   | a:visited                               | 选择所有访问过的链接                                       | 1    |
| [:active](https://www.runoob.com/cssref/sel-active.html)     | a:active                                | 选择活动链接                                               | 1    |
| [:hover](https://www.runoob.com/cssref/sel-hover.html)       | a:hover                                 | 选择鼠标在链接上面时                                       | 1    |
| [:focus](https://www.runoob.com/cssref/sel-focus.html)       | input:focus                             | 选择具有焦点的输入元素                                     | 2    |
| [:first-letter](https://www.runoob.com/cssref/sel-firstletter.html) | p:first-letter                          | 选择每一个<p>元素的第一个字母                              | 1    |
| [:first-line](https://www.runoob.com/cssref/sel-firstline.html) | p:first-line                            | 选择每一个<p>元素的第一行                                  | 1    |
| [:first-child](https://www.runoob.com/cssref/sel-firstchild.html) | p:first-child                           | 指定只有当<p>元素是其父级的第一个子级的样式。              | 2    |
| [:before](https://www.runoob.com/cssref/sel-before.html)     | p:before                                | 在每个<p>元素之前插入内容                                  | 2    |
| [:after](https://www.runoob.com/cssref/sel-after.html)       | p:after                                 | 在每个<p>元素之后插入内容                                  | 2    |
| [:lang(*language*)](https://www.runoob.com/cssref/sel-lang.html) | p:lang(it)                              | 选择一个lang属性的起始值="it"的所有<p>元素                 | 2    |
| [*element1*~*element2*](https://www.runoob.com/cssref/sel-gen-sibling.html) | p~ul                                    | 选择p元素之后的每一个ul元素                                | 3    |
| [[*attribute*^=*value*\]](https://www.runoob.com/cssref/sel-attr-begin.html) | a[src^="https"]                         | 选择每一个src属性的值以"https"开头的元素                   | 3    |
| [[*attribute*$=*value*\]](https://www.runoob.com/cssref/sel-attr-end.html) | a[src$=".pdf"] | 选择每一个src属性的值以".pdf"结尾的元素 | 3                                                          |      |
| [[*attribute**=*value*\]](https://www.runoob.com/cssref/sel-attr-contain.html) | a[src*="runoob"]                        | 选择每一个src属性的值包含子字符串"runoob"的元素            | 3    |
| [:first-of-type](https://www.runoob.com/cssref/sel-first-of-type.html) | p:first-of-type                         | 选择每个p元素是其父级的第一个p元素                         | 3    |
| [:last-of-type](https://www.runoob.com/cssref/sel-last-of-type.html) | p:last-of-type                          | 选择每个p元素是其父级的最后一个p元素                       | 3    |
| [:only-of-type](https://www.runoob.com/cssref/sel-only-of-type.html) | p:only-of-type                          | 选择每个p元素是其父级的唯一p元素                           | 3    |
| [:only-child](https://www.runoob.com/cssref/sel-only-child.html) | p:only-child                            | 选择每个p元素是其父级的唯一子元素                          | 3    |
| [:nth-child(*n*)](https://www.runoob.com/cssref/sel-nth-child.html) | p:nth-child(2)                          | 选择每个p元素是其父级的第二个子元素                        | 3    |
| [:nth-last-child(*n*)](https://www.runoob.com/cssref/sel-nth-last-child.html) | p:nth-last-child(2)                     | 选择每个p元素的是其父级的第二个子元素，从最后一个子项计数  | 3    |
| [:nth-of-type(*n*)](https://www.runoob.com/cssref/sel-nth-of-type.html) | p:nth-of-type(2)                        | 选择每个p元素是其父级的第二个p元素                         | 3    |
| [:nth-last-of-type(*n*)](https://www.runoob.com/cssref/sel-nth-last-of-type.html) | p:nth-last-of-type(2)                   | 选择每个p元素的是其父级的第二个p元素，从最后一个子项计数   | 3    |
| [:last-child](https://www.runoob.com/cssref/sel-last-child.html) | p:last-child                            | 选择每个p元素是其父级的最后一个子级。                      | 3    |
| [:root](https://www.runoob.com/cssref/sel-root.html)         | :root                                   | 选择文档的根元素                                           | 3    |
| [:empty](https://www.runoob.com/cssref/sel-empty.html)       | p:empty                                 | 选择每个没有任何子级的p元素（包括文本节点）                | 3    |
| [:target](https://www.runoob.com/cssref/sel-target.html)     | #news:target                            | 选择当前活动的#news元素（包含该锚名称的点击的URL）         | 3    |
| [:enabled](https://www.runoob.com/cssref/sel-enabled.html)   | input:enabled                           | 选择每一个已启用的输入元素                                 | 3    |
| [:disabled](https://www.runoob.com/cssref/sel-disabled.html) | input:disabled                          | 选择每一个禁用的输入元素                                   | 3    |
| [:checked](https://www.runoob.com/cssref/sel-checked.html)   | input:checked                           | 选择每个选中的输入元素                                     | 3    |
| [:not(*selector*)](https://www.runoob.com/cssref/sel-not.html) | :not(p)                                 | 选择每个并非p元素的元素                                    | 3    |
| [::selection](https://www.runoob.com/cssref/sel-selection.html) | ::selection                             | 匹配元素中被用户选中或处于高亮状态的部分                   | 3    |
| [:out-of-range](https://www.runoob.com/cssref/sel-out-of-range.html) | :out-of-range                           | 匹配值在指定区间之外的input元素                            | 3    |
| [:in-range](https://www.runoob.com/cssref/sel-in-range.html) | :in-range                               | 匹配值在指定区间之内的input元素                            | 3    |
| [:read-write](https://www.runoob.com/cssref/sel-read-write.html) | :read-write                             | 用于匹配可读及可写的元素                                   | 3    |
| [:read-only](https://www.runoob.com/cssref/sel-read-only.html) | :read-only                              | 用于匹配设置 "readonly"（只读） 属性的元素                 | 3    |
| [:optional](https://www.runoob.com/cssref/sel-optional.html) | :optional                               | 用于匹配可选的输入元素                                     | 3    |
| [:required](https://www.runoob.com/cssref/sel-required.html) | :required                               | 用于匹配设置了 "required" 属性的元素                       | 3    |
| [:valid](https://www.runoob.com/cssref/sel-valid.html)       | :valid                                  | 用于匹配输入值为合法的元素                                 | 3    |
| [:invalid](https://www.runoob.com/cssref/sel-invalid.html)   | :invalid                                | 用于匹配输入值为非法的元素                                 | 3    |

### 6.3 其他属性

| 属性           | 说明                                                         | CSS  |
| :------------- | :----------------------------------------------------------- | :--- |
| user-select    | 元素能否被选中，none:不能被选中，all:点击全部选中，text:可选，auto:自动判断 |      |
| pointer-events | 元素能否成为鼠标事件的target                                 |      |

