## CSS 选择器及其优先级

| 选择器         | 格式          | 优先级权重 |
| -------------- | ------------- | ---------- |
| !important     | 10000         |            |
| 内联样式       | 1000          |            |
| id 选择器      | #id           | 100        |
| 类选择器       | .classname    | 10         |
| 属性选择器     | a[ref=“eee”]  | 10         |
| 伪类选择器     | li:last-child | 10         |
| 标签选择器     | div           | 1          |
| 伪元素选择器   | li::after     | 1          |
| 相邻兄弟选择器 | h1+p          | 0          |
| 子选择器       | ul>li         | 0          |
| 后代选择器     | li a          | 0          |
| 通配符选择器   | *             | 0          |

**注意事项：**

- !important 声明的样式的优先级最高；
- 如果优先级相同，则最后出现的样式生效；
- 继承得到的样式的优先级最低；
- 通用选择器（*）、子选择器（>）和相邻同胞选择器（+）并不在这四个等级中，它们的权值都为 0 ；
- 样式表的来源不同时，优先级顺序为：内联样式 > 内部样式 > 外部样式 > 浏览器用户自定义样式 > 浏览器默认样式。

## CSS 中可继承与不可继承属性有哪些

**可继承：**

`字体系列` font-family font-weight font-size

`文本系列` color text-align line-height

`可见系列` 如 visibility

> 由于属性太多，这里只列举常见的可继承的属性

## display 的属性值及其作用

| 属性值       | 作用                                                       |
| ------------ | ---------------------------------------------------------- |
| none         | 元素不显示，并且会从文档流中移除。                         |
| block        | 块类型。默认宽度为父元素宽度，可设置宽高，换行显示。       |
| inline       | 行内元素类型。默认宽度为内容宽度，不可设置宽高，同行显示。 |
| inline-block | 默认宽度为内容宽度，可以设置宽高，同行显示。               |
| list-item    | 像块类型元素一样显示，并添加样式列表标记。                 |
| table        | 此元素会作为块级表格来显示。                               |
| inherit      | 规定应该从父元素继承 display 属性的值。                    |

## display 的 block、inline 和 inline-block 的区别

**block：** 会独占一行，可以设置 width、height、margin 和 padding 属性；

**inline：** 元素不会独占一行，设置 width、height 属性无效。但可以设置水平方向的 margin 和 padding 属性，不能设置垂直方向的 padding 和 margin；

**inline-block：** 将对象设置为 inline 对象，但对象的内容作为 block 对象呈现，之后的内联对象会被排列在同一行内。

## 隐藏元素的方法有哪些

**display: none:** 渲染树不会渲染对象
 **visibility: hidden:**  元素在页面中仍占据空间，但是不会响应绑定的监听事件。
 **opacity: 0:**  元素在页面中仍然占据空间，并且能够响应元素绑定的监听事件。
 **position: absolute:**  通过使用绝对定位将元素移除可视区域内，以此来实现元素的隐藏。
 **z-index:**  负值:来使其他元素遮盖住该元素，以此来实现隐藏。
 **clip/clip-path:** 元素仍在页面中占据位置，但是不会响应绑定的监听事件。
 **transform: scale(0,0):** 将元素缩放为 0，元素仍在页面中占据位置，但是不会响应绑定的监听事件。

## link 和 @import 的区别

两者都是外部引用 CSS 的方式，它们的区别如下：

`link` 是 XHTML 标签，除了加载 CSS 外，还可以定义 RSS 等其他事务；  `@import` 只能加载 CSS。
 `link` 引用 CSS 时，在页面载入时同时加载；  `@import` 需要页面网页完全载入以后加载。
 `link` 是 XHTML 标签，无兼容问题；  `@import` 是在 CSS2.1 提出的，低版本的浏览器不支持。
 `link` 支持使用 Javascript 控制 DOM 去改变样式；  `@import` 不支持。

## transition 和 animation 的区别

`transition` 是`过度属性`，强调过度，它的实现需要触发一个事件（比如鼠标移动上去，焦点，点击等）才执行动画。它类似于 flash 的补间动画，设置一个开始关键帧，一个结束关键帧。

`animation` 是`动画属性`，它的实现不需要触发事件，设定好时间之后可以自己执行，且可以循环一个动画。它也类似于 flash 的补间动画，但是它可以设置多个关键帧（用@keyframe 定义）完成动画。

## display:none 与 visibility:hidden 的区别

这两个属性都是让元素隐藏，不可见。两者区别如下：

**1. 在渲染树中**

- `display:none` 不渲染元素
- `sibility:hidden`渲染元素，只是不可见

**2. 是否是继承属性**

- `display:none` 是非继承属性，子孙节点会随着父节点从渲染树消失，通过修改子孙节点的属性也无法显示；
- `visibility:hidden` 是继承属性，子孙节点消失是由于继承了hidden，通过设置visibility:visible可以让子孙节点显示；

**3. 重排与重绘**

- `display:none` 修改此属性，会导致整个文档重排
- `visibility:hidden` 修改此属性，只会导致当前元素重绘

## 伪元素和伪类的区别和作用？

**伪元素：** 在内容元素的前后插入额外的元素或样式，但是这些元素实际上并不在文档中生成。它们只在外部显示可见，但不会在文档的源代码中找到它们，因此，称为“伪”元素。例如：

```css
p::before {content: "第一章：";}
p::after {content: "Hot!";}
p::first-line {background: red;}
p::first-letter {font-size: 30px;}
复制代码
```

**伪类：** 将特殊的效果添加到特定选择器上。它是已有元素上添加类别的，不会产生新的元素。例如：

```css
a:hover {color: #FF00FF}
p:first-child {color: red}
复制代码
```

## 对盒模型的理解

CSS3 中的盒模型有以下两种：`标准盒模型`、`IE 盒模型`

`盒模型`是由四个部分组成的，分别是 `margin`、`border`、`padding` 和 `content`。

`标准盒模型`和 `IE 盒模型`的区别在于设置 `width` 和 `height` 时，所对应的范围不同：
 标准盒模型的 width 和 height 属性的范围只包含了 `content`，
 IE 盒模型的 width 和 height 属性的范围包含了 `border、padding 和 content`。

可以通过修改元素的 box-sizing 属性来改变元素的盒模型：
 box-sizing: `content-box`表示标准盒模型（默认值）
 box-sizing: `border-box`表示 IE 盒模型（怪异盒模型）

## 为什么有时候⽤ translate 来改变位置⽽不是定位？

`translate` 不会触发浏览器重排和重绘,只会触发复合, 利用GPU效率高
 `绝对定位`会导致重排, 进而触发重绘, 利用CPU效率低

## li 与 li 之间有看不见的空白间隔是什么原因引起的？如何解决？

浏览器会把 inline 内联元素间的空白字符（空格、换行、Tab 等）渲染成一个空格。为了美观，通常是一个`<li>`放在一行，这导致`<li>`换行后产生换行字符，它变成一个空格，占用了一个字符的宽度。

**解决办法：**

- 为`<li>`设置 float:left。不足：有些容器是不能设置浮动，如左右切换的焦点图等。
- 将所有`<li>`写在同一行。不足：代码不美观。
- 将`<ul>`内的字符尺寸直接设为 0，即 font-size:0。不足：`<ul>`中的其他字符尺寸也被设为 0，需要额外重新设定其他字符尺寸，且在 Safari 浏览器依然会出现空白间隔。
- 消除`<ul>`的字符间隔 letter-spacing:-8px，不足：这也设置了`<li>`内的字符间隔，因此需要将`<li>`内的字符间隔设为默认 letter-spacing:normal。

## CSS3 中有哪些新特性

1. 新增各种 `CSS` 选择器 `nth` `not`
2. 圆角 `border-radius`
3. 旋转 `transform`
4. 阴影 `ext-shadow`
5. 其他

## 常见的图片格式及使用场景

1. `GIF`  动图
2. `JPEG` 有损色彩丰富，适合存储照片, 文件较大。
3. `PNG`  无损，体积小，支持透明度
4. `SVG`  放大不失真，适合 logo icon
5. `BMP`  无损, 不压缩, 文件较大。
6. `WebP` 谷歌新出的图片格式, 体积比 `png` 更小, 兼容性不好。

## 对 CSS Sprites 的理解

`CSS Sprites`（精灵图），将一个页面涉及到的所有图片都包含到一张大图中去，然后利用 CSS 的 background-image，background-repeat，background-position 属性的组合进行背景定位。

**优点：**

- 利用 CSS Sprites 能很好地`减少`网页的 `http` 请求，从而大大提高了页面的性能，这是 `CSS Sprites` 最大的优点；
- CSS Sprites 能`减少`图片的`字节`，把 3 张图片合并成 1 张图片的字节总是小于这 3 张图片的字节总和。

**缺点：**

- 在图片合并时，要把多张图片有序的、合理的合并成一张图片，还要留好足够的空间，防止板块内出现不必要的背景。在宽屏及高分辨率下的自适应页面，如果背景不够宽，很容易出现背景断裂；
- CSS Sprites 在开发的时候相对来说有点麻烦，需要借助photoshop或其他工具来对每个背景单元测量其准确的位置。
- 维护方面：CSS Sprites 在`维护`的时候比较`麻烦`，页面背景有少许改动时，就要改这张合并的图片，无需改的地方尽量不要动，这样避免改动更多的CSS，

## 什么是物理像素，逻辑像素和像素密度，为什么在移动端开发时需要用到@3x, @2x 这种图片？

以 `iPhone XS` 为例，当写 CSS 代码时，针对于单位 `px`，其宽度为 414px & 896px，也就是说当赋予一个 div 元素宽度为 414px，这个 div 就会填满手机的宽度；

而如果有一把尺子来实际测量这部手机的`物理像素`，实际为 1242*2688 物理像素；经过计算可知，1242/414=3，也就是说，在单边上，一个`逻辑像素` = 3 个物理像素，就说这个屏幕的像素密度为 3，也就是常说的 3 倍屏。

对于图片来说，为了保证其不`失真`，1 个图片像素至少要对应一个物理像素，假如原始图片是 `500*300` 像素，那么在 3 倍屏上就要放一个 `1500*900` 像素的图片才能保证 1 个物理像素至少对应一个图片像素，才能不失真。

当然，也可以针对所有屏幕，都只提供最高清图片。虽然`低密度`屏幕用不到那么多图片像素，而且会因为下载多余的像素造成`带宽浪费`和`下载延迟`，但从结果上说能保证图片在所有屏幕上都不会失真。

还可以使用 CSS 媒体查询来判断不同的像素密度，从而选择不同的图片:

```css
my-image { background: (low.png); }
@media only screen and (min-device-pixel-ratio: 1.5) {
  #my-image { background: (high.png); }
}
复制代码
```

## CSS 优化和提高性能的方法有哪些？

**加载性能：**

- css `压缩`, 减小文件体积。
- css `单一`样式 margin-bottom:bottom； margin-left:left；比 margin:top 0 bottom 0；执行效率高。
- 减少使用 `@import`，建议使用 `link`，因为 link 在页面加载时一起加载，import 是页面加载完成之后再加载。

**选择器性能：**

- `关键`选择器, 减少层级, 最高不超过3层
- 尽量使用 `class`, 避免使用html标签选择
- 少使用`后代`选择器, 后代选择器`开销高`
- 避免对`可继承`的属性`重复`定义
- 避免使用`通配`规则, 只对需要的元素进行处理`

**渲染性能：**

- 慎重使用高性能属性：`浮动`、`定位`。
- 尽量减少页面`重排`、`重绘`。
- 属性值为 0 时，不加`单位`。
- 属性值为浮动小数 0.**，可以`省略`小数点之前的 0。
- 不使用 `@import` 前缀，它会影响 css 的`加载速度`。

**可维护性：**

- 抽离 `css`, 提高`可复用性`。
- 样式与内容`分离`, 提高`可维护性`。

## CSS 预处理器/后处理器是什么？为什么要使用它们？

**预处理器**， 如：`less`，`sass`，用来预编译 sass或者less，增加了 css 代码的`复用性`。层级，循环， 变量，循环等功能对UI组件`更易开发`与`维护`。

**后处理器**， 如： `PostCSS`，通常是在完成的样式表中根据 CSS 规范处理 CSS`有效`。最常做的是添加浏览器私有`前缀`，解决跨浏览器`兼容性`的问题。

**使用原因：**

1. 结构清晰， 便于`扩展`
2. 可以很方便的`屏蔽`浏览器私有语法的差异
3. 完美的`兼容`了 CSS 代码，可以应用到老项目中
4. 可以轻松实现`多重继承`

## inline-block 什么时候会显示间隙？

**主要有以下三种情形:**

- 有空格时会有间隙，可以`删除空格`解决；
- `margin` 正值时，可以让 `margin` 使用`负值`解决；
- 使用 `font-size` 时，可通过设置 font-size:0、letter-spacing、word-spacing 解决；

## 单行、多行文本溢出隐藏

**单行文本溢出**

```css
overflow: hidden;            // 溢出隐藏
text-overflow: ellipsis;      // 溢出用省略号显示
white-space: nowrap;         // 规定段落中的文本不进行换行
复制代码
```

**多行文本溢出**

```css
overflow: hidden;            // 溢出隐藏
text-overflow: ellipsis;     // 溢出用省略号显示
display: -webkit-box;         // 作为弹性伸缩盒子模型显示。
-webkit-box-orient: vertical; // 设置伸缩盒子的子元素排列方式：从上到下垂直排列
-webkit-line-clamp: 3;        // 显示的行数
复制代码
```

## 对媒体查询的理解？

```html
<!-- link元素中的CSS媒体查询 -->
<link rel="stylesheet" media="(max-width: 800px)" href="example.css" />
<!-- 样式表中的CSS媒体查询 -->
<style>
@media (max-width: 600px) {
  .facet_sidebar {
    display: none;
  }
}
</style>
复制代码
```

简单来说，`@media` 可以针对不同的`屏幕尺寸`设置不同的样式，特别是需要设置设计`响应式`的页面。

## 对 CSS 工程化的理解

**CSS 工程化是为了解决以下问题：**
 `宏观设计：` `CSS` 代码如何组织、如何拆分、模块结构怎样设计？
 `编码优化：` 怎样写出更好的 CSS ？
 `构建：` 如何处理我的 CSS，才能让它的`打包`结果最优？
 `可维护性：` 容易变更, 容易接手

**以下三个方向都是时下比较流行的、普适性非常好的 CSS 工程化实践：**
 `预处理器：` Less、 Sass 等；
 `后处理器：` PostCSS
 `Webpack loader 等`  。

**如何用 Webpack 实现对 CSS 的处理：**
 `css-loader：` 导入 CSS 模块，对 CSS 代码进行编译处理；
 `style-loader：` 创建 style 标签，把 CSS 内容写入标签。

在实际使用中，`css-loader 的执行顺序一定要安排在 style-loader 的前面`。因为只有完成了编译过程，才可以对 css 代码进行插入；若提前插入了未编译的代码，那么 webpack 是无法理解这坨东西的，它会无情报错。

## 如何判断元素是否到达可视区域

以图片显示为例：

- `window.innerHeight` 是浏览器可视区的高度；
- `document.body.scrollTop` || `document.documentElement.scrollTop` 是浏览器滚动的过的距离；
- `imgs.offsetTop` 是元素顶部距离文档顶部的高度（包括滚动条的距离）；
- 内容达到显示区域的：`img.offsetTop < window.innerHeight + document.body.scrollTop`;

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/919077c9295e4a1884c14aa60db7dbfa~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

## z-index 属性在什么情况下会失效

通常 `z-index` 的使用是在有两个`重叠`的标签，z-index 值越大就越是在上层。z-index 元素的 `position` 属性需要是 `relative`，`absolute` 或是 `fixed`。

**z-index 属性在下列情况下会失效：**

- 父元素 position 为 `relative` 时，子元素的 z-index 失效。解决：父元素 position 改为 absolute 或 static；
- 元素没有设置 position 属性为非 static 属性。解决：设置该元素的 position 属性为 relative，absolute 或是 fixed；
- 元素在设置 z-index 的同时还设置了 `float` 浮动。解决：去除 float，改为 `display：inline-block`；

## CSS3 中的 transform 有哪些属性

- translate 位移
- rotate 旋转
- scale 缩放
- skew 斜切

## 常见的 CSS 布局单位

**像素px** `基本`布局单位
 **百分比%** ，相对于`父元素`的`百分比`，从而实现响应式的效果。
 **em** 相对于父元素的文本的`倍数`。如果父元素未设置 `font-size`，则相对于浏览器的`默认`字体尺寸(默认 16px)。
 **rem**  相对于根元素 `font-size` 的倍数。作用：利用 rem 可以实现简单的`响应式`布局，可以利用 html 元素中字体的大小与屏幕间的比值来设置 font-size 的值，以此实现当屏幕分辨率变化时让元素也随之变化。

**vw：** 相对于视窗的宽度，视窗宽度是 100vw；
 **vh：** 相对于视窗的高度，视窗高度是 100vh；
 **vmin：** vw 和 vh 中的较小值；
 **vmax：** vw 和 vh 中的较大值；

`vw` 和百分比的区别是: `vw` 相对于视窗, `%` 相对于父元素

## px、em、rem 的区别及使用场景

**三者的区别：**

- `px` 是固定的像素，一旦设置了就无法因为适应页面大小而改变。
- `em` 和 `rem` 相对于 px 更具有灵活性，他们是`相对`长度单位，其长度不是固定的，更适用于响应式布局。
- em 是相对于其`父元素`来设置字体大小，这样就会存在一个问题，进行任何元素设置，都有可能需要知道他父元素的大小。而 rem 是相对于`根元素`，这样就意味着，只需要在根元素确定一个参考值。

**使用场景：**

- 对于只需要适配`少部分`移动设备，且分辨率对页面影响不大的，使用 `px` 即可 。
- 对于需要适配`各种`移动设备，使用 `rem`，例如需要适配 iPhone 和 iPad 等分辨率差别比较挺大的设备。

## 如何根据设计稿进行移动端适配？

移动端适配主要有`两个`维度：

**适配不同像素密度**，针对不同的`像素密度`，使用 CSS `媒体查询`，选择不同精度的图片，以保证图片不会`失真`；
 **适配不同屏幕大小**，由于不同的屏幕有着不同的`逻辑像素`大小，所以如果直接使用 `px` 单位，会使得开发的页面在某一款手机上可以准确显示，但是在另一款手机上就会`失真`。为了适配不同屏幕的大小，应按照比例来还原设计稿的内容。

为了能让页面的尺寸自适应，可以使用 `rem`，`em`，`vw`，`vh` 等`相对单位`。

## 响应式设计的概念及基本原理

`响应式网站`是指一个网站能够`兼容多个终端`。

**关于原理：** 基本原理是通过媒体查询（@media）查询检测不同的设备屏幕尺寸做处理。

**关于兼容：** 页面头部必须有 `meta` 声明的 `viewport`。

```html
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0" />
复制代码
```

## 为什么需要清除浮动？清除浮动的方式

**浮动的定义**： 非 IE 浏览器下，容器不设高度且子元素浮动时，容器高度不能被内容撑开。 此时，内容会溢出到容器外面而影响布局。这种现象被称为浮动（溢出）。

**浮动的工作原理：**

- 浮动元素脱离文档流，不占据空间（引起“高度塌陷”现象）
- 浮动元素碰到包含它的边框或者其他浮动元素的边框停留

浮动元素可以左右移动，直到遇到另一个浮动元素或者遇到它外边缘的包含框。浮动框不属于文档流中的普通流，当元素浮动之后，不会影响块级元素的布局，只会影响内联元素布局。此时文档流中的普通流就会表现得该浮动框不存在一样的布局模式。当包含框的高度小于浮动框的时候，此时就会出现“高度塌陷”。

**浮动元素引起的问题？**

- 父元素的高度无法被撑开，影响与父元素同级的元素
- 与浮动元素同级的非浮动元素会跟随其后
- 若浮动的元素不是第一个元素，则该元素之前的元素也要浮动，否则会影响页面的显示结构

## 使用 clear 属性清除浮动的原理？

使用 clear 属性清除浮动，其语法如下：

```css
clear: none|left|right|both
复制代码
```

如果单看字面意思，clear:left 是“清除左浮动”，clear:right 是“清除右浮动”，实际上，这种解释是有问题的，因为浮动一直还在，并没有清除。

官方对 clear 属性解释：“元素盒子的边不能和前面的浮动元素相邻”，对元素设置 clear 属性是为了避免浮动元素对该元素的影响，而不是清除掉浮动。

还需要注意 clear 属性指的是元素盒子的边不能和前面的浮动元素相邻，注意这里“前面的”3 个字，也就是 clear 属性对“后面的”浮动元素是不闻不问的。考虑到 float 属性要么是 left，要么是 right，不可能同时存在，同时由于 clear 属性对“后面的”浮动元素不闻不问，因此，当 clear:left 有效的时候，clear:right 必定无效，也就是此时 clear:left 等同于设置 clear:both；同样地，clear:right 如果有效也是等同于设置 clear:both。由此可见，clear:left 和 clear:right 这两个声明就没有任何使用的价值，至少在 CSS 世界中是如此，直接使用 clear:both 吧。

一般使用伪元素的方式清除浮动：

```css
.clear::after{
  content: '';
  display: block;
  clear: both;
}
复制代码
```

clear 属性只有块级元素才有效的，而::after 等伪元素默认都是内联水平，这就是借助伪元素清除浮动影响时需要设置 display 属性值的原因。

## 对 BFC 的理解，如何创建 BFC

先来看两个相关的概念：

- Box: Box 是 CSS 布局的对象和基本单位，⼀个⻚⾯是由很多个 Box 组成的，这个 Box 就是我们所说的盒模型。
- Formatting context：块级上下⽂格式化，它是⻚⾯中的⼀块渲染区域，并且有⼀套渲染规则，它决定了其⼦元素将如何定位，以及和其他元素的关系和相互作⽤。

块格式化上下文（Block Formatting Context，BFC）是 Web 页面的可视化 CSS 渲染的一部分，是布局过程中生成块级盒子的区域，也是浮动元素与其他元素的交互限定区域。

通俗来讲：BFC 是一个独立的布局环境，可以理解为一个容器，在这个容器中按照一定规则进行物品摆放，并且不会影响其它环境中的物品。如果一个元素符合触发 BFC 的条件，则 BFC 中的元素布局不受外部影响。

**创建 BFC 的条件：**

- 根元素：body；
- 元素设置浮动：float 除 none 以外的值；
- 元素设置绝对定位：position (absolute、fixed)；
- display 值为：inline-block、table-cell、table-caption、flex 等；
- overflow 值为：hidden、auto、scroll；

**BFC 的特点：**

- 垂直方向上，自上而下排列，和文档流的排列方式一致。
- 在 BFC 中上下相邻的两个容器的 margin 会重叠
- 计算 BFC 的高度时，需要计算浮动元素的高度
- BFC 区域不会与浮动的容器发生重叠
- BFC 是独立的容器，容器内部元素不会影响外部元素
- 每个元素的左 margin 值和容器的左 border 相接触

**BFC 的作用：**

- 解决 margin 的重叠问题：由于 BFC 是一个独立的区域，内部的元素和外部的元素互不影响，将两个元素变为两个 BFC，就解决了 margin 重叠的问题。
- 解决高度塌陷的问题：在对子元素设置浮动后，父元素会发生高度塌陷，也就是父元素的高度变为 0。解决这个问题，只需要把父元素变成一个 BFC。常用的办法是给父元素设置overflow:hidden。
- 创建自适应两栏布局：可以用来创建自适应两栏布局：左边的宽度固定，右边的宽度自适应。

```css
<div class="left"></div>
<div class="right"></div>

.left{
     width: 100px;
     height: 200px;
     background: red;
     float: left;
 }
 .right{
     height: 300px;
     background: blue;
     overflow: hidden;
 }
复制代码
```

左侧设置float:left，右侧设置overflow: hidden。这样右边就触发了 BFC，BFC 的区域不会与浮动元素发生重叠，所以两侧就不会发生重叠，实现了自适应两栏布局。

## 什么是 margin 重叠问题？如何解决？

**问题描述：**

两个块级元素的上外边距和下外边距可能会合并（折叠）为一个外边距，其大小会取其中外边距值大的那个，这种行为就是外边距折叠。需要注意的是，浮动的元素和绝对定位这种脱离文档流的元素的外边距不会折叠。重叠只会出现在垂直方向。

**计算原则：**

折叠合并后外边距的计算原则如下：

- 如果两者都是正数，取大者
- 如果是一正一负，取正值减去负值的绝对值
- 两个都是负值时，取绝对值大者

**解决办法：**

对于折叠的情况，主要有两种：`兄弟之间重叠`和`父子之间重叠`

1. 兄弟之间重叠

- 底部元素变为行内盒子：display: inline-block
- 底部元素设置浮动：float
- 底部元素的 position 的值为absolute/fixed

1. 父子之间重叠

- 父元素加入：overflow: hidden
- 父元素添加透明边框：border:1px solid transparent
- 子元素变为行内盒子：display: inline-block
- 子元素加入浮动属性或定位

## 元素的层叠顺序

层叠顺序，英文称作 stacking order，表示元素发生层叠时有着特定的垂直显示顺序。下面是盒模型的层叠规则：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4fb831e69f6e449eafa1f80afbc48dd7~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

对于上图，由上到下分别是：

1. 背景和边框：建立当前层叠上下文元素的背景和边框。
2. 负的 z-index：当前层叠上下文中，z-index 属性值为负的元素。
3. 块级盒：文档流内非行内级非定位后代元素。
4. 浮动盒：非定位浮动元素。
5. 行内盒：文档流内行内级非定位后代元素。
6. z-index:0：层叠级数为 0 的定位元素。
7. 正 z-index：z-index 属性值为正的定位元素。

::: tip 提示 当定位元素 z-index:auto，生成盒在当前层叠上下文中的层级为 0，不会建立新的层叠上下文，除非是根元素。 :::

## position 的属性有哪些，区别是什么

| position | 有以下属性值：                                               |
| -------- | ------------------------------------------------------------ |
| 属性值   | 概述                                                         |
| absolute | 生成绝对定位的元素，相对于 static 定位以外的一个父元素进行定位。元素的位置通过 left、top、right、bottom 属性进行规定。 |
| relative | 生成相对定位的元素，相对于其原来的位置进行定位。元素的位置通过 left、top、right、bottom 属性进行规定。 |
| fixed    | 生成绝对定位的元素，指定元素相对于屏幕视⼝（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变，⽐如回到顶部的按钮⼀般都是⽤此定 |
| static   | 默认值，没有定位，元素出现在正常的文档流中，会忽略 top, bottom, left, right 或者 z-index 声明，块级元素从上往下纵向排布，⾏级元素从左 |
| inherit  | 规定从父元素继承 position 属性的值                           |

前面三者的定位方式如下：

**relative**： 元素的定位永远是相对于元素自身位置的，和其他元素没关系，也不会影响其他元素。

**fixed**： 元素的定位是相对于 window （或者 iframe）边界的，和其他元素没有关系。但是它具有破坏性，会导致其他元素位置的变化。

**absolute**： 元素的定位相对于前两者要复杂许多。如果为 `absolute` 设置了 `top`、`left`，浏览器会根据什么去确定它的纵向和横向的偏移量呢？答案是浏览器会递归查找该元素的所有父元素，如果找到一个设置了`position:relative/absolute/fixed`的元素，就以该元素为基准定位，如果没找到，就以浏览器边界定位。如下两个图所示：

## display、float、position 的关系

1. 首先判断 display 属性是否为 none，如果为 none，则 position 和 float 属性的值不影响元素最后的表现。
2. 然后判断 position 的值是否为 absolute 或者 fixed，如果是，则 float 属性失效，并且 display 的值应该被设置为 table 或者 block，具体转换需要看初始转换值。
3. 如果 position 的值不为 absolute 或者 fixed，则判断 float 属性的值是否为 none，如果不是，则 display 的值则按上面的规则转换。注意，如果 position 的值为 relative 并且 float 属性的值存在，则 relative 相对于浮动后的最终位置定位。
4. 如果 float 的值为 none，则判断元素是否为根元素，如果是根元素则 display 属性按照上面的规则转换，如果不是，则保持指定的 display 属性值不变。

总的来说，可以把它看作是一个类似优先级的机制，`position:absolute` 和 `position:fixed` 优先级最高，有它存在的时候，浮动不起作用，`display` 的值也需要调整；其次，元素的 `float` 特性的值不是 `none` 的时候或者它是根元素的时候，调整 `display` 的值；最后，非根元素，并且非浮动元素，并且非绝对定位的元素，`display` 特性值同设置值。

## absolute 与 fixed 共同点与不同点

**共同点：**

- 改变行内元素的呈现方式，将 display 置为 `inline-block`
- 使元素`脱离`普通文档流，不再占据文档物理空间
- 覆盖`非定位`文档元素

**不同点：**

- `absolute` 与 `fixed` 的根元素不同，`absolute` 的根元素可以设置，`fixed` 根元素是浏览器。
- 在有滚动条的页面中，`absolute` 会跟着父元素进行移动，`fixed` 固定在页面的具体位置。

## 对 sticky 定位的理解

`sticky` 英文字面意思是粘贴，所以可以把它称之为粘性定位。语法：position: sticky; 基于用户的`滚动位置`来定位。

粘性定位的元素是依赖于用户的滚动，在 `position:relative` 与 `position:fixed` 定位之间切换。它的行为就像 `position:relative`; 而当页面滚动超出目标区域时，它的表现就像 `position:fixed`;，它会固定在目标位置。元素定位表现为在跨越特定阈值前为相对定位，之后为固定定位。这个特定阈值指的是 top, right, bottom 或 left 之一，换言之，指定 top, right, bottom 或 left 四个阈值其中之一，才可使粘性定位生效。否则其行为与相对定位相同。


作者：教主鸽鸽
链接：https://juejin.cn/post/7080889197719994375
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。