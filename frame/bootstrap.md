# Bootstrap5

## 1. 概述

Bootstrap是有Twitter公司的两名工程师，基于html、css、js开发的简洁的，开源、强大、优雅的ui框架。至今经历了5个大版本，现在学习的第五个版本是最新的版本。

Bootstrap内置了大量的css类，供元素使用，相当于一个预先设置好的类库，供需要标签直接用，直接就会被渲染。

> 学习UI框架的终极意义，学会如何查文档，运用文档
>
> 市面上的UI框架很多很多，企业会用哪个不一定。工作中百分之八十用框架

### 1.1 Bootstrap文档

学习UI框架的终极意义，学会如何查文档，运用文档。如何查阅文档，如何运用文档的案例。

* Bootstrap5文档查阅：https://v5.bootcss.com/docs/5.1/getting-started/introduction/

* 其他版本的文档查阅：https://v5.bootcss.com/docs/versions/

### 1.3 下载生产文件

下载css的样式文件库，和js的功能文件库，图标文件库（单独下载）

### 1.4 各个版本的区别

任何的框架都会升级，框架升级后会有一些改动。可能对内容进行增删改，所以一定要查看对应版本的手册。

工作中，一定要先看公司使用的项目中的框架版本，会在开发手册中体现。

版本5的改动比较大，原来js依赖jQuery，现在不依赖了，也不再兼容IE。

对很多类名也有改动，最大的改动就是左、右，如：`float-left`到5版本`float-start`，所有的左都变成了`start`所有的右都变成了`end`



## 2. 布局

### 2.1 断点

https://v5.bootcss.com/docs/layout/breakpoints/

Bootstrap5中，为我们设计了5+1个断点，写好了媒体查询，使用类中缀可以直接对应某个响应式范围，用于响应式构建。

> 打开源码，按ctrl+f 搜索关键词，关键类名

```css
/*没写类中缀的就是手机端小于576px*/
/*屏幕宽度在576px以上含576px*/
@media (min-width: 576px) {/*类中缀sm 小号，pad*/}
/*屏幕宽度在768px以上含768px*/
@media (min-width: 768px) {/*类中缀md 中号 平板*/}
/*屏幕宽度在992px以上含992px*/
@media (min-width: 992px) {/*类中缀lg 普通 小屏幕的pc*/}
/*屏幕宽度在1200px以上含1200px*/
@media (min-width: 1200px) {/*类中缀xl 大号 大屏显示器*/}
/*屏幕宽度在1400px以上含1400px*/
@media (min-width: 1400px) {/*类中缀xxl 超大号 超大屏幕*/}
```

### 2.2 天沟（gutter）

天沟指容器中左右两侧的内间距。让内容不至于紧贴元素的两侧，默认时共1.5em（24px）间距宽，左右0.75em。

### 2.3 容器

https://v5.bootcss.com/docs/layout/containers/

容器`container`类名，容器就是一个响应式的“版心”。这个版心会根据页面宽度的变化而变化，就是个自动版心。会根据页面宽度放大缩小，改变版心的宽度。

* sm：页面宽度576-768之间，版心最大宽度540px
* md：页面宽度768-992之间，版心最大宽度720px
* lg：页面宽度992-1200之间，版心最大宽度960px
* xl：页面宽度1200-1400之间，版心最大宽度1140px
* xxl：页面宽度1400以上，版心最大宽度1320px

```css
@media (min-width: 576px) {
  .container-sm, .container {
    max-width: 540px;
  }
}
@media (min-width: 768px) {
  .container-md, .container-sm, .container {
    max-width: 720px;
  }
}
@media (min-width: 992px) {
  .container-lg, .container-md, .container-sm, .container {
    max-width: 960px;
  }
}
@media (min-width: 1200px) {
  .container-xl, .container-lg, .container-md, .container-sm, .container {
    max-width: 1140px;
  }
}
@media (min-width: 1400px) {
  .container-xxl, .container-xl, .container-lg, .container-md, .container-sm, .container {
    max-width: 1320px;
  }
}
```

可以使用 **.container-sm|md|lg|xl** 类来创建响应式容器。

容器的 max-width 属性值会根据屏幕的大小来改变。

| Class            | 超小屏幕 <576px | 小屏幕 ≥576px | 中等屏幕 ≥768px | 大屏幕 ≥992px | 特大屏幕 ≥1200px | 超级大屏幕 ≥1400px |
| :--------------- | :-------------- | :------------ | :-------------- | :------------ | :--------------- | :----------------- |
| `.container-sm`  | 100%            | 540px         | 720px           | 960px         | 1140px           | 1320px             |
| `.container-md`  | 100%            | 100%          | 720px           | 960px         | 1140px           | 1320px             |
| `.container-lg`  | 100%            | 100%          | 100%            | 960px         | 1140px           | 1320px             |
| `.container-xl`  | 100%            | 100%          | 100%            | 100%          | 1140px           | 1320px             |
| `.container-xxl` | 100%            | 100%          | 100%            | 100%          | 100%             | 1320px             |

 在bootstrap中容器有三种写法：

* `.container` ,它会自动适配断点，叫做定宽容器。会按照响应式中的最大宽度体现，并且居中，左右的天沟
* `.container-fluid`全宽适配，变宽容器。撑满整个展示的全部宽度，也具有左右两侧的天沟
* `.container-{*}`,直接制定断点的类，用的较少，如：`.container-sm`



在写布局的时候，容器类是一定要写的，否则无法限定响应式的部分。UI框架本来就是响应式框架。



## 3. 基础内容

### 3.1  颜色

| 颜色   | 背景颜色       | 字体颜色       | 链接(有hover效果) |
| ------ | -------------- | -------------- | ----------------- |
| 蓝色   | bg-primary     | text-primary   | link-primary      |
| 灰色   | bg-secondary   | text-secondary | link-secondary    |
| 绿色   | bg-success     | text-success   | link-success      |
| 红色   | bg-danger      | text-danger    | link-danger       |
| 黄色   | bg-warning     | text-warning   | link-warning      |
| 蓝绿色 | bg-info        | text-info      | link-info         |
| 亮色   | bg-light       | text-light     | link-light        |
| 深色   | bg-dark        | text-dark      | link-dark         |
| 白色   | bg-white       | text-white     | link-white        |
| 透明   | bg-transparent | —              | —                 |
| 50度黑 | —              | text-black-50  | —                 |
| 50度白 | —              | text-white-50  | —                 |

```html
<div class="container">
  <h2>代表指定意义的文本颜色</h2>
  <p class="text-muted">柔和的文本。</p>
  <p class="text-primary">重要的文本。</p>
  <p class="text-success">执行成功的文本。</p>
  <p class="text-info">代表一些提示信息的文本。</p>
  <p class="text-warning">警告文本。</p>
  <p class="text-danger">危险操作文本。</p>
  <p class="text-secondary">副标题。</p>
  <p class="text-dark">深灰色文字。</p>
  <p class="text-body">默认颜色，为黑色。</p>
  <p class="text-light">浅灰色文本（白色背景上看不清楚）。</p>
  <p class="text-white">白色文本（白色背景上看不清楚）。</p>
  <p class="text-black-50">透明度为 50% 的黑色文本，背景为白色。</p>
  <p class="text-white-50 bg-dark">透明度为 50% 的白色文本，背景为黑色。</p>
</div>
```



### 3.2 文字排版

https://v5.bootcss.com/docs/content/typography/

> Bootstrap 5 默认的 **font-size** 为 16px, **line-height** 为 1.5。
>
> 默认的 **font-family** 为 "Helvetica Neue", Helvetica, Arial, sans-serif。
>
> 此外，所有的 **<p>** 元素 **margin-top: 0** 、 **margin-bottom: 1rem** (16px)。

* 使用`.h1.h6`类可以同标签h1~h6大小样式一致

```html
<h1>大标题</h1>
<div class="h1">我也想大标题</div>
```

* 使用一种更大的标题样式`.display-1`~`.display-6`没有加粗效果，比标题更大，从1～6逐步变小，1号最大。

```html
<div class="display-1">更大号的字体1</div>
<div class="display-2">更大号的字体2</div>
```

下表提供了 Bootstrap5 更多排版类的实例：

| 类名                 | 描述                                                         |
| :------------------- | :----------------------------------------------------------- |
| **.lead**            | 让段落更突出                                                 |
| **.small**           | 指定更小文本 (为父元素的 85% )                               |
| **.text-start**      | 左对齐                                                       |
| **.text-center**     | 居中                                                         |
| **.text-end**        | 右对齐                                                       |
| **.text-justify**    | 设定文本对齐,段落中超出屏幕部分文字自动换行                  |
| **.text-nowrap**     | 段落中超出屏幕部分不换行                                     |
| **.text-lowercase**  | 设定文本小写                                                 |
| **.text-uppercase**  | 设定文本大写                                                 |
| **.text-capitalize** | 设定单词首字母大写                                           |
| **.initialism**      | 显示在 <abbr> 元素中的文本以小号字体展示，且可以将小写字母转换为大写字母 |
| **.list-unstyled**   | 移除默认的列表样式，列表项中左对齐 ( <ul> 和 <ol> 中)。 这个类仅适用于直接子列表项 (如果需要移除嵌套的列表项，你需要在嵌套的列表中使用该样式) |
| **.list-inline**     | 将所有列表项放置同一行                                       |

### 3.3 列表

列表一般情况下更多使用ul和ol，默认有标识符。去掉列表的标识符`.list-unstyled`。

```html
    <!-- 去掉列表的标识符 -->
    <ul class="list-unstyled">
      <li>aaaa</li>
      <li>bbbb</li>
    </ul>
```



## 4. 表格和表单

### 4.1 表格

https://v5.bootcss.com/docs/content/tables/

* `.table`基础类，写给`<table>`标签必须写，又了基础类其他的辅助类才生效。
* `.table-sm`用于通过减少内边距来设置较小的表格:
* `.table-{color}`表格颜色，表格颜色的类除了可以加到`<table>`标签也可以加到`<tr>`和`<td>`
* `.table-striped`条形纹，加到`<table>`标签上，使得`<tbody>`里的行，隔行变色
* `.table-hover`鼠标悬停行变色效果，加到`<table>`标签上，使得`<tbody>`里的行，发生悬停变色
* `.table-bordered`给table加边框，有了这个属性再可以改边框的颜色`.border-{color}`
* 表头主题有两个`table-dark`深色主题，`table-light`亮色主题，这两个类写给`<thead>`修改表头的主题样式。无边框使用`.table-borderless`
* `.table-responsive` 类用于创建响应式表格

下表列出了表格颜色类的说明:

| 类名                 | 描述                             |
| :------------------- | :------------------------------- |
| **.table-primary**   | 蓝色: 指定这是一个重要的操作     |
| **.table-success**   | 绿色: 指定这是一个允许执行的操作 |
| **.table-danger**    | 红色: 指定这是可以危险的操作     |
| **.table-info**      | 浅蓝色: 表示内容已变更           |
| **.table-warning**   | 橘色: 表示需要注意的操作         |
| **.table-active**    | 灰色: 用于鼠标悬停效果           |
| **.table-secondary** | 灰色: 表示内容不怎么重要         |
| **.table-light**     | 浅灰色，可以是表格行的背景       |
| **.table-dark**      | 深灰色，可以是表格行的背景       |

你可以通过以下类设定在指定屏幕宽度下显示滚动条：

| 类名                      | 屏幕宽度 |
| :------------------------ | :------- |
| **.table-responsive-sm**  | < 576px  |
| **.table-responsive-md**  | < 768px  |
| **.table-responsive-lg**  | < 992px  |
| **.table-responsive-xl**  | < 1200px |
| **.table-responsive-xxl** | < 1400px |

### 4.2 表单

https://v5.bootcss.com/docs/forms/overview/

> 表单元素 **<input>**, **<textarea>**, 和 **<select>** elements 在使用 **.form-control** 类的情况下，宽度都是设置为 100%。



#### （1）文本输入框和表述文字

* `.form-control`加给`input`标签的，让`input`标签有样式上的变化
* `.form-label`加在`label`标签上的，有间距，非必要
* `.form-text`对表单进行描述，并且是块元素，字体大小和间距的变化，非必要

```html
    <div>
      <label class="form-label" for="user">用户名</label>
      <input type="text" id="user" class="form-control">
      <div class="form-text">用户名可以为数字+字母，也可以为汉字</div>
    </div>
```



#### （2）下拉菜单

* `.form-select`下拉菜单必写的类，基础类，写给`select`标签
* `.form-select-lg`下拉菜单的文字大一点，`.form-select-sm`下拉菜单的文字小一点

```html
    <select class="form-select form-select-lg">
      <option>请选择城市</option>
      <option value="0">北京</option>
      <option value="1">郑州</option>
      <option value="2">深圳</option>
      <option value="3">重庆</option>
      <option value="4">南京</option>
    </select>
```



#### （3）单选复选框

* `.form-check`单选框和复选框外层包裹元素，有些边距的样式
* `.form-check-input`单选和复选框的样式，会根据属性`type`改变样式
* `.form-check-label`是单选和复选的说明文字

```html
   <div>
      <div class="form-check">
        <input type="radio" value="0" class="form-check-input" name="sex">
        <label class="form-check-label">男</label>
      </div>
      <div class="form-check">
        <input type="radio" value="1" class="form-check-input" name="sex">
        <label class="form-check-label">女</label>
      </div>
    </div>
```



####  （4）表单组

* `.input-group`表单组的外层包裹元素
* `.input-group-text`表单标签前面的文字提示，使用内联元素
* `.form-control`输入框就用表单控件

```html
    <div class="input-group">
      <span class="input-group-text bg-primary text-white">北京刘冉</span>
      <input type="text" class="form-control">
    </div>
```



## 5. 工具类

### 5.1 尺寸

#### （1）宽度和高度

https://v5.bootcss.com/docs/utilities/sizing/

宽度和高度，boot中提供宽度和高度的类是百分比的类。

* 宽度 `.w-{number}`支持25、50、75、100、auto，分别代表百分比
* 高度 `.h-{number}`支持25、50、75、100、auto，分别代表百分比。注意高度是父级元素的百分比，前提是父元素要有高度才行

#### （2）相对视口的尺寸

* 相对视口的宽度`vw-100`支持100，全屏宽度
* 相对视口的高度`vh-100`支持100，全屏高度

```html
   <div class="bg-warning">
      <div class="zdy-h w-25 bg-danger">父级宽度的25%</div>
      <div class="zdy-h w-50 bg-primary">父级宽度的50%</div>
      <div class="vh-100 w-75 bg-success"></div>
    </div>
```



### 5.2 边框

https://v5.bootcss.com/docs/utilities/borders/

#### （1）边框样式

* `border`边框的基础类，默认四个方向一像素边框
  * `border-bottom`下边框
  * `border-top`上边框
  * `border-start`左边框
  * `border-end`右边框
* 边框的宽度`border-{number}`0-5数字，0是去掉边框，1-5是1px-5px
* 边框的颜色`border-{color}`颜色使用boot提供的颜色



#### （2）圆角

* `.rounded`圆角的基础类，默认四个方向圆角
* `.rounded-{number}`圆角的弧度0-3
* `.rounded-circle`圆形
* `.rounded-pill`胶囊型



### 5.3 间距

间距包括内间距和外间距，内间距使用`p-*`，外间距使用`m-*`

* 间距的宽度（距离）
  * `m-{number}`0-5，外间距,1是0.25rem，四个方向共同使用一个距离的外间距
  * `p-{number}`0-5,内间距,1是0.25rem，四个方向共同使用一个距离的外间距
* 间距的方向
  * 上内、外间距`pt-{number}`和`mt-{number}`
  * 下内、外间距`pb-{number}`和`mb-{number}`
  * 左内、外间距`ps-{number}`和`ms-{number}`
  * 右内、外间距`pe-{number}`和`me-{number}`
  * 垂直方向的内、外间距`py-{number}`和`my-{number}`
  * 水平方向的内、外间距`px-{number}`和`mx-{number}`
  * 特殊值，外间距的`auto`值，`mx-auto`

* 响应式的内外间距需要加类中缀，响应式写法会随着`.container`的变化而变化
  * `.p-{类中缀}-{number}` 响应式写法的内间距
  * `.m-{类中缀}-{number}` 响应式写法的内间距



### 5.4 display显示

使用`display`属性，可以改变元素的展示效果

* `.d-none`就是元素消失`display:none`
* `.d-block`以块级形式显示
* `.d-inline`以内联形式显示
* `.d-inline-block`以行内块显示
* `.d-flex`弹性
* 显示方式都有响应式的写法，如：`.d-{类中缀}-none`



#### flex布局相关属性

https://v5.bootcss.com/docs/utilities/flex/

* flex主轴排序 
  * 行模式`.flex-row` 和`.flex-row-reverse`
  * 列模式`.flex-column`和`.flex-column-reverse`
  * 可以写响应式 `.flex-{类中缀}-row`

* 主轴的对齐方式
  * `.justify-content-start` 起点
  * `.justify-content-end`终点
  * `.justify-content-center`居中
  * `.justify-content-between`两端对齐
  * `.justify-content-around`两臂间隔
  * `.justify-content-evenly`平均分布
  * 响应式的效果`.justify-content-{类中缀}-{对齐方式}`
* 项目交叉轴对齐
  * `.align-items-start`交叉轴起点对齐
  * `.align-items-end`交叉轴终点对齐
  * `.align-items-center`交叉轴居中对齐
  * 响应式的效果`.align-items-{类中缀}-{方式}`
* 项目的收缩和增长
  * `.flex-{grow|shrink}-0`项目不可放大/不可收缩
  * `.flex-{grow|shrink}-1`可放大/可收缩

### 5.5 浮动

https://v5.bootcss.com/docs/utilities/float/

* `.float-start`左浮动
* `.float-end`右浮动
* `.float-none`不浮动
* 响应式浮动显示`.float-{类中缀}-{浮动方式}`
* `.clearfix`清除父元素高度坍塌，放到父元素中

### 5.6 定位

#### （1）定位方式

* `.position-relative`相对定位
* `.position-absolute`绝对定位
* `.position-fixed`固定定位

> 注意：boot5新增了定位方向，5版本以前没有定位方向，因此5版本以前定位尽量自己写

#### （2）位移方向

* `top-{number}`对于顶部的位移位置0、50、100，分别值0%,50%,100%
* `bottom-{number}`对于底部的位移位置0、50、100，分别值0%,50%,100%
* `start-{number}`对于左侧的位移位置0、50、100，分别值0%,50%,100%
* `end-{number}`对于右侧的位移位置0、50、100，分别值0%,50%,100%

#### （3）中心位置位移

* `.translate-middle`使用位移x轴y轴居中
* `.translate-middle-x`水平方向居中
* `.translate-middle-y`垂直方向居中

```html
    <div class="baba position-relative">
      <div class="erzi position-absolute start-50 top-50 translate-middle"></div>
    </div>
  </div>
```

### 5.7 文本

#### （1）文本对齐方式

写给外层父元素（块级），具有继承性的

* `.text-start`文本、内联左对齐
* `.text-end`文本、内联右对齐
* `.text-center`文本、内联居中对齐
* 响应式的对齐方式`.text-{类中缀}-{方式}`

#### （2）字体

* `.fw-bold`加粗体
* `.fw-bolder`特粗体
* `.fw-normal`正常体
* `.fw-light`细体
* `.fw-lighter`特细体
* `.fst-italic`斜体

#### （3）文本修饰线

* `.text-decoration-underline`下划线
* `.text-decoration-line-through`删除线
* `.text-decoration-none`无线条



## 6. 栅格系统

### 6.1 行和列

父子布局，父元素包裹子元素。父元素使用`.row`行，子元素是父元素的列使用`.col-{number}`。

一行可以分为12份，最多可以容纳12个列，每个列`.col-1`。

在栅格布局中可以调整每个列所占的份额，如一行四列

```html
<div class="row">
  <div class="col-3">占3个份额也就是3/12</div>	
  <div class="col-3">占3个份额也就是3/12</div>	
  <div class="col-3">占3个份额也就是3/12</div>	
  <div class="col-3">占3个份额也就是3/12</div>	
</div>
```

栅格布局的底层是flexbox，也就是说，你使用栅格同时也可以使用flex的相关属性。

每一个列不允许有额外的外间距，本身存在12px左右内间距（天沟）。

### 6.2 响应式栅格布局

* `.col-{类中缀}-{number}`列的响应式写法
* 注意列都是挨着的不能加外间距，可以考虑天沟，也就是在列中嵌套元素
* 当一行12份已满会自动换行

### 6.3 栅格布局的嵌套

行`.row`类嵌套列`.col-{number}`，行列布局底层是flex，容器使用容器属性，项目使用项目属性。

保证行和列清晰区分。如果需要嵌套`.row>.col>.row>.col`

发生嵌套之后，只要是行`.row`里就会分12列。列只会和上层行（父级发生分块关系），简单说子元素只分父元素的份数。

```html
 <!-- 最外层行：分为两块，一左一右 -->
      <div class="row">
        <!-- 左侧块 嵌套内容-->
        <div class="vh-100 bg-warning col-xl-9 col-12">
          <!-- 在列中嵌套，一定要加行row -->
          <div class="row">
            <div class="col-lg-4 col-sm-6 col-12"></div>
          </div>
        </div>
        <!-- 右侧块 -->
        <div class="vh-100 bg-danger col-xl-3 d-none d-xl-block"></div>
      </div>
```



## 7 组件

### 7.1 按钮

* `.btn`按钮的基础类，必写
* `.btn-{color}`按钮的颜色
* `.btn-outline-{color}`带轮廓线的按钮
* 按钮的尺寸`.btn-lg`大按钮，`.btn-sm`小按钮
* 按钮组`.btn-group`，用一个div包裹多个按钮

```html
    <!-- 按钮组 -->
    <div class="btn-group">
      <button class="btn btn-outline-success">编辑</button>
      <button class="btn btn-outline-danger">删除</button>
    </div>
```

### 7.2 navbar

#### 最外层包裹元素navbar

* `.navbar`基础类，创建了一个flexbox空间，有多种对齐方式，允许在内部有定位
* `.navbar-expand{-sm|-md|-lg|-xl|-xxl}`响应式断点，大小菜单切换展示

* `.navbar-dark`暗色主题，和小菜单的颜色有关，`.navbar-light`亮色主题。

#### logo区域

* `.navbar-brand`logo区域的类

#### 小菜单

* 小菜单的出现会在断点以下的区域产生，如：`.navbar-expand-md`小菜单会在md以下出现
* 小菜单的按钮可以使用`button`标签
* `.navbar-toggler`修饰小菜单样式
* 小菜单里的三条横线 `.navbar-toggler-icon`可以使用`span`标签

* js属性:折叠功能`data-bs-toggle="collapse"`
* js属性：使用功能的针对目标`data-bs-target="#id值"`大菜单的id值

```html
<!-- 小菜单 -->
      <button class="navbar-toggler" data-bs-toggle="collapse" data-bs-target="#menu">
        <span class="navbar-toggler-icon"></span>
      </button>
```



#### 大菜单

* `.collapse`消失和显示的切换
* `.navbar-collapse`样式
* 菜单列表一般使用列表标签`.navbar-nav`
* 列表中的项目`.nav-item`
* 如果项目中有链接`.nav-link`,被激活的link，加`.active`只能有一个激活项
* 大菜单要让小菜单控制需要写`id`属性 

```html
      <!-- 大菜单 -->
      <div class="collapse navbar-collapse" id="menu">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a href="#" class="nav-link active">首页</a>
          </li>
        </ul>
      </div>
```



### 7.3 徽章【11:38】

* `.badge`徽章的基础类，一般会长都适用内联元素
* 可以添加徽章的背景色`.bg-{color}`
* 可以改变徽章的圆角形状
* 徽章也可以在父级元素中参与定位

```html
    <button class="btn btn-danger position-relative">
      收件箱
      <span class="badge bg-success rounded-pill position-absolute top-0 start-100 translate-middle">10</span>
    </button>
```



#### 图标的使用

https://icons.bootcss.com/

* 图标其实就是文字
* 在图表库中找到自己需要的图标名称
* 使用内联元素`.bi-envelope`在图标名称前加`bi-`
* 因为是文字所以可以使用文字的类去修改小图标的颜色，大小等



### 7.4 下拉菜单

https://v5.bootcss.com/docs/components/dropdowns/

* 外层父元素包裹按钮和下拉菜单，外层父元素需要`.dropdown`有一个相对定位的属性
* `.dropdown-toggle`负责渲染按钮中的小三角
* 下拉菜单可以使用列表或者其他包裹的快元素`.dropdown-menu`下拉区，是带有消失这个属性
* 下拉项`.dropdown-item`选项具有hover样式
* js属性：给按钮加`data-bs-toggle="dropdown"`



### 7.5 模态框【14:35】

* 分成两个部分	
  * 被点击对象
    * `data-bs-toggle="modal"`触发模态框的显示与隐藏
    * `data-bs-target="#模态框id"`
  * 弹出层
    * `.modal`先消失，灰色遮罩
    * `id`属性与点击的被触发元素相关联
* 模态区域
  * `.modal-dialog`弹窗的区域
  * `.modal-content`弹窗区域里要加主体部分（白色框）里面加内容

```html
 <!-- 被点击对象 -->
    <a href="javascript:;" data-bs-toggle="modal" data-bs-target="#motai">点击弹出</a>
    <!-- 弹出框的内容 -->
    <!-- 半透明遮罩层 -->
    <div class="modal" id="motai">
      <!-- 模态区域 -->
      <div class="modal-dialog">
        <!-- 白色框样式 -->
        <div class="modal-content">123123</div>
      </div>
    </div>
```



* 白色模态框内容
  * `.modal-header`模态框的头部样式
  * 头部样式里可以增加一个按钮用于关闭模态框`.btn-close`
  * js属性：关闭的按钮还要有js功能关闭模态框`data-bs-dismiss="modal"`
  * body写主体说明内容区域`.modal-body`
  * 尾部有美观需要可以加，也可以不加`.modal-footer`



### 7.6 手风琴效果

* 手风琴最外层`.accordion`手风琴外层样式
* 最外层需要`id`属性，由最外层元素监督控制折叠项
* 最外包裹元素里的第一层是手风琴的项目`.accordion-item`
* 在每一个组里有展示头和展示主体
  * 展示头`.accordion-header`放按钮标题
    * 展示头里放展示的点击按钮，有小箭头属性和相关的js功能
    * `.accordion-button`按钮样式
    * `data-bs-toggle="collapse"`折叠打开属性
    * `data-bs-target="#a"`折叠/打开的对象，#后放对象的id
  * 展示主体`.accordion-collapse`
    * 展示主体，还有一个专门负责消失的类`.collapse`
    * 只要展示主体具有`.show`类的时候，才能显示
    * 通过js开合`data-bs-parent="#最上层父元素的id"`关联最上层父级，听它的指示关闭
    * 展示主体里还有一层，具体内容区，有个内间距，为了好看`.accordion-body`

### 7.7 列表组

https://v5.bootcss.com/docs/components/list-group/

- 可以使用ul li标签
- `.list-group`列表标签外层类，去掉标识符间距等
- `.list-group-flush`根据不同列表组的效果选取的文档上对应的样式（可以改）
- `.list-group-item`列表组项

```html
<ul class="list-group list-group-flush">
    <li class="list-group-item">商品列表</li>
    <li class="list-group-item">多条件搜索</li>
    <li class="list-group-item">添加商品</li>
</ul>
```



### 7.8 导航和选项卡

https://v5.bootcss.com/docs/components/navs-tabs/

#### （1）导航

```html
 <ul class="nav">
        <li class="nav-item">
          <a href="#" class="nav-link">首页</a>
        </li>
        <li class="nav-item">
          <a href="#" class="nav-link">学习用品</a>
        </li>
        <li class="nav-item">
          <a href="#" class="nav-link">私人定制</a>
        </li>
      </ul>
```



####  （2）tab面板

* `.nav`控制区外层
* `.nav-tabs`控制区的样式
* `.nav-link`触发按钮每一个的样式
* js属性：`data-bs-toggle="tab"`tab的切换
* js属性：`data-bs-target="#对应关联展示区的id"`
* `.tab-content`展示区的最外层
* `.tab-pane`消失，对应显示应具有`.active`显示
* `.fade`过渡，过渡的样式`.show`

```html
  <div class="container">
      <!-- 触发区按钮区 -->
      <div class="nav nav-tabs">
        <button class="nav-link active" data-bs-toggle="tab" data-bs-target="#one">商品详情</button>
        <button class="nav-link" data-bs-toggle="tab" data-bs-target="#two">商品评价</button>
      </div>
      <!-- 展示区 -->
      <div class="tab-content">
        <div class="tab-pane fade show active" id="one">默认打开的对应第一个按钮的</div>
        <div class="tab-pane fade" id="two">第二块点击商品评价展示的内容</div>
      </div>
    </div>
```

#### （3）面包屑导航

* `.breadcrumb`外层列表基础类
* `.breadcrumb-item`面包屑导航项
* 改变面包屑的分隔符`style="--bs-breadcrumb-divider:'>';"`

```html
    <ol class="breadcrumb" style="--bs-breadcrumb-divider:'>';">
      <li class="breadcrumb-item">
        <a href="#" class="text-decoration-none text-dark">首页</a>
      </li>
      <li class="breadcrumb-item">
        <a href="#" class="text-decoration-none text-dark">学习用品</a>
      </li>
      <li class="breadcrumb-item">
        <a href="#" class="text-decoration-none text-dark">笔记本电脑</a>
      </li>
    </ol>
```



### 7.9 分页

https://v5.bootcss.com/docs/components/pagination/

* `.pagination`最外层列表基础类
* `.page-item`分页项
  * `.disabled`禁用状态
  * `.active`激活状态
* `.page-link`分页链接样式，有间距和字体样式

```html
    <ul class="pagination">
      <li class="page-item disabled">
        <span class="page-link">上一页</span>
      </li>
      <li class="page-item active"><a href="#" class="page-link">1</a></li>
      <li class="page-item"><a href="#" class="page-link">2</a></li>
      <li class="page-item"><a href="#" class="page-link">3</a></li>
      <li class="page-item"><a href="#" class="page-link">4</a></li>
      <li class="page-item">
        <span class="page-link">下一页</span>
      </li>
    </ul>
```



### 7.10 卡片

https://v5.bootcss.com/docs/components/card/

* `.card`卡片的外层父级基础类，有边框有圆角
* 图片`.card-img-top`顶部图片，`.card-img-bottom`底部图片

* `.card-body`卡片的文字部分外包裹标签，有间距
* 卡片的 内容区域可以加`.card-title`和`.card-text`文字描述等



### 7.11 轮播图

https://v5.bootcss.com/docs/components/carousel/

* `.carousel`最外层基础类
* `.slide`自动轮播了，平滑过渡样式
* js属性：`data-bs-ride="carousel"`自动轮播定时器
* `data-bs-interval="2000"`轮播图定时器的时间
* 图片区`.carousel-inner`最外层
  * `.carousel-item`图片组，都是消失状态
  * `.active`只有一个能显示，js切换这个类

```html
     <div class="carousel slide" data-bs-ride="carousel">
        <!-- 图片区 -->
        <div class="carousel-inner">
          <div class="carousel-item active">
            <img src="./img/xz-img/index/banner1.png" class="d-block w-100">
          </div>
          <div class="carousel-item">
            <img src="./img/xz-img/index/banner2.png" class="d-block w-100">
          </div>
          <div class="carousel-item">
            <img src="./img/xz-img/index/banner3.png" class="d-block w-100">
          </div>
          <div class="carousel-item">
            <img src="./img/xz-img/index/banner4.png" class="d-block w-100">
          </div>
        </div>
        <!-- 向左区 -->
        <!-- 向右区 -->
        <!-- 控制区 -->
      </div>
```



#### 左右控制

* `.carousel-control-prev`后退区域
* `.carousel-control-prev-icon`后退符号
* `data-bs-slide="prev"`后退按钮js控制轮播图倒退
* `.carousel-control-next`向前区域
* `.carousel-control-next-icon`向前符号
* `data-bs-slide="next"`前进按钮js控制轮播图前进
* 控制前进和后退必须有目标，是整个轮播图的`id`,`data-bs-target="#lbt"`左右控制符的目标都是轮播图本身

```html
        <!-- 向左区 -->
        <button class="carousel-control-prev" data-bs-slide="prev" data-bs-target="#lbt">
          <span class="carousel-control-prev-icon"></span>
        </button>
        <!-- 向右区 -->
        <button class="carousel-control-next" data-bs-slide="next" data-bs-target="#lbt">
          <span class="carousel-control-next-icon"></span>
        </button>
```

#### 控制符号

* `.carousel-indicators`控制符号的最外层
* `.active`当前激活项
* js属性：`data-bs-target="#lbt"`关联轮播图id
* js属性：`data-bs-slide-to="0"`控制图片的索引

```html
<!-- 控制区 -->
        <ul class="carousel-indicators">
          <li class="active" data-bs-target="#lbt" data-bs-slide-to="0"></li>
          <li data-bs-target="#lbt" data-bs-slide-to="1"></li>
          <li data-bs-target="#lbt" data-bs-slide-to="2"></li>
          <li data-bs-target="#lbt" data-bs-slide-to="3"></li>
        </ul>
```

