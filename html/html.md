# HTML

**参考链接**
- [MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTML)
- [菜鸟教程](https://www.runoob.com/tags/html-reference.html)

[toc]

## 基本结构
```html
<!DOCTYPE html>
<html lang="zh-CN">
    <head>
        <meta charset="utf-8">
        <title>Document</title>
    </head>
    <body>
        
    </body>
</html>
```

## 标签一览

[菜鸟参考手册](https://www.runoob.com/tags/ref-byfunc.html)

**基础**

|标签|描述|属性|备注|
|:-|:-|:-|:-|
|!DOCTYPE|定义文档类型|html,单|
|html|定义一个html文档|manifest|
|title|定义html文档标题|
|body|定义文档主体|
|h1 to h6|定义 HTML 标题|
|p|定义简单的折行|
|br|定义简单的折行|
|hr|定义简单的折行|

**格式**

|标签|描述|属性|备注|
|:-|:-|:-|:-|
|abbr|定义一个缩写|
|address|定义文档作者或拥有者的联系信息|
|b|定义粗体文本|
|bdi|允许您设置一段文本，使其脱离其父元素的文本方向设置||new,edge不支持|
|bdo|定义文本的方向|dir="ltr"/"rtl"(必须)|
|blockquote|定义摘自另一个源的块引用|cite=url|
|cite|标签定义作品（比如书籍、歌曲、电影、电视节目、绘画、雕塑等等）的标题|
|code|定义计算机代码文本||短语标签|
|del|定义文档中已删除的文本|cite=url;datetime="..."|
|dfn|定义一个定义项目||短语标签|
|em|呈现为被强调的文本||短语标签|
|i|斜体文本|
|ins|定义已经被插入文档中的文本|cite=url;datetime="..."|
|kbd|定义键盘文本样式||短语标签|
|mark|定义带有记号的文本||new|
|meter|定义度量衡,仅用于已知最大和最小值的度量||new,新版浏览器才支持|
|pre|定义预格式化的文本|
|progress|定义运行中的任务进度|max;value|new|
|q|定义一个短的引用|cite=url|
|rp|定义不支持 ruby 元素的浏览器所显示的内容||new|
|rt|定义字符（中文注音或字符）的解释或发音||new|
|ruby|定义 ruby 注释（中文注音或字符）||new|
|s|对那些不正确、不准确或者没有用的文本进行标识|
|samp|定义计算机程序的样本文本||短语标签|
|small|定义小型文本（和旁注）|
|strong|定义重要的文本||短语标签|
|sub|定义下标文本|
|sup|定义上标文本|
|time|定义公历的时间（24 小时制）或日期|datetime;pubdate|new,新版浏览器才支持|
|u|定义与常规文本风格不同的文本，像拼写错误的单词或者汉语中的专有名词|
|var|定义变量||短语标签|
|wbr|规定在文本中的何处适合添加换行符||new|

**表单**

| 标签     | 描述                                     | 属性                                                         | 备注                                                         |
| :------- | :--------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| form     | 用于创建供用户输入的 HTML 表单           | accept-charset;action;autocomplete;enctype;method;name;novalidate;target |                                                              |
| input    | 定义一个输入控件                         | accept;alt;autocomplete;autofocus;checked;  disabled;form;      formaction;;formmethod;formnovalidate; <br>formtarget;height;list;max;maxlength; min;multiple;name;pattern;placeholder;readonly; required;size;src;step;type;value;width | type=button;checkbox;color;date;<br>datetime;datetime-local;email;<br>file;hidden;image;month;number;<br/>password;radio;range;reset;search;submit;<br/>tel;text;time;url;week |
| textarea | 定义一个多行的文本输入控件               | autofocus;cols;disabled;form;maxlength;<br>name;placeholder;readonly;require;rows;wrap |                                                              |
| button   | 定义一个按钮                             | ...                                                          | 如果在 HTML 表单中使用 button>元素，不同的浏览器可能会提交不同的按钮值。请使用 input 在 HTML 表单中创建按钮 |
| select   | 创建下拉列表                             | autofocus;disabled;form;multiple;name;required;size          |                                                              |
| optgroup | 经常用于把相关的选项组合在一起           | disabled;label                                               |                                                              |
| option   | 定义下拉列表中的一个选项（一个条目）     | disabled;selected;value                                      |                                                              |
| label    | 为 input 元素定义标注（标记）            | for;form                                                     |                                                              |
| fieldset | 将表单内的相关元素分组                   | disabled;form;name                                           |                                                              |
|          | legend                                   | 为 fieldset元素定义标题                                      |                                                              |
| datalist | 规定了input元素可能的选项列表            |                                                              | new,新版浏览器才支持                                         |
| output   | 作为计算结果输出显示(比如执行脚本的输出) | for;form;name                                                | new,新版浏览器才支持                                         |

**框架**

|标签|描述|属性|备注|
|:-|:-|:-|:-|
|iframe|规定一个内联框架|height;sandbox;seamless;src;srcdoc;width|

**图像**

|标签|描述|属性|备注|
|:-|:-|:-|:-|
|img|定义 HTML 页面中的图像|loading;alt;border;crossorigin;height;ismap;src;usemap;width||
|map|用于客户端图像映射|name||
|area|定义图像映射内部的区域|alt;coords;href;hreflang;media;rel;shape;target;type||
|canvas|通过脚本来绘制图形|height;width||
||figcaption|为figure元素定义标题||
||figure|标记文档中的一个图像||

**Audio/Video**

|标签|描述|属性|备注|
|:-|:-|:-|:-|
|audio|定义声音，比如音乐或其他音频流|autoplay;controls;loop;muted;preload;src|new|
|source|媒体元素定义媒体资源|media;src;type;srcset|new|
|track|规定外部文本轨道，也就是字幕|default;kind;label;src;srclang|new|
|video|定义视频|autoplay;controls;loop;muted;<br>preload;src;height;poster;width|new|

**链接**

|标签|描述|属性|备注|
|:-|:-|:-|:-|
|a|定义一个链接|download;href;herflang;media;rel;target;type|
|link|定义文档与外部资源的关系|href;hreflang;media;rel;sizes;type|
|main|指定文档的主体内容||唯一|
|nav|定义导航链接的部分|

**样式**

|标签|描述|属性|备注|
|:-|:-|:-|:-|
|style|定义 HTML 文档的样式信息|media;scoped;type||
||div|定义文档中的节||
||span|定义文档中的节||
|header|New	定义一个文档头部部分||new|
|footer|定义一个文档底部||new|
|section|定义了文档的某个区域||new|
|article|定义一个文章内容||new|
|aside|定义其所处内容之外的内容||new|
|details|定义了用户可见的或者隐藏的需求的补充细节||new|
|dialog|定义一个对话框或者窗口||new,仅chrom和safari支持|
|summary|为detaila定义一个可见的标题,当用户点击标题时会显示出详细信息|open|new,edge不支持|

**元信息**

|标签|描述|属性|备注|
|:-|:-|:-|:-|
|head|定义关于文档的信息|
|meta|定义关于文档的信息|charset;content;http-equiv;name|
|base|定义页面中所有链接的默认地址或默认目标|href;target|

**程序**

|标签|描述|属性|备注|
|:-|:-|:-|:-|
|script|定义客户端脚本|async;charset;defer;src;type||
||noscript|定义针对不支持客户端脚本的用户的替代内容||
|embed|定义了一个容器，用来嵌入外部应用或者互动程序（插件）|...|new,不建议使用|
|param|定义对象的参数|name;value||

**列表**

|标签|描述|属性|备注|
|:-|:-|:-|:-|
|ul|定义一个无序列表|
|ol|定义一个有序列表|
|li|定义一个列表项|
|dl|定义一个定义列表|
|dt|定义一个定义定义列表中的项目|
|dd|定义定义列表中项目的描述|

**表格**

|标签|描述|属性|备注|
|:-|:-|:-|:-|
|table|定义一个表格|
|caption|定义表格标题|
|th|定义表格标题|
|tr|定义表格中的行|
|td|定义表格中的单元|colspan;rowspan|
|thead|定义表格中的表头内容|
|tbody|定义表格中的主体内容|
|tfoot|定义表格中的表注内容（脚注）|
|col|定义表格中一个或多个列的属性值|span|
|colgroup|定义表格中供格式化的列组|span|

## 全局属性

[菜鸟全局属性](https://www.runoob.com/tags/ref-standardattributes.html)

|属性|描述|备注|
|:-|:-|:-|
|accesskey|规定激活（使元素获得焦点）元素的快捷键|alt+accesskey激活|
|class|元素的类名|
|contenteditable|规定是否可编辑元素的内容|
|data-*|用于存储私有页面后应用的自定义数据|new|
|dir|规定元素内容的文本方向|
|draggable|规定元素是否可拖动|new,链接和图像默认是可拖动|
|hidden|规定对元素进行隐藏|new|
|id|规定元素的唯一 id|
|lang|设置元素中内容的语言代码|
|spellcheck|检测元素是否拼写错误|new|
|title|规定元素的额外信息（可在工具提示中显示）|


## 事件

[菜鸟事件](https://www.runoob.com/tags/ref-eventattributes.html)

**由窗口触发事件（适用于body标签）**

|属性|描述|备注|
|:-|:-|:-|
|onblur|当窗口失去焦点时运行脚本|
|onfocus|当窗口获得焦点时运行脚本|
|onload|当文档加载时运行脚本|
|...|

**表单事件**

|属性|描述|备注|
|:-|:-|:-|
|onblur|当窗口失去焦点时运行脚本|
|onfocus|当窗口获得焦点时运行脚本|
|onchange|当元素改变时运行脚本|
|onselect|当选取元素时运行脚本|
|onsubmit|当提交表单时运行脚本|
|...|

**键盘事件**

|属性|描述|备注|
|:-|:-|:-|
|onkeydown|当按下按键时运行脚本|
|onkeypress|当按下并松开按键时运行脚本|
|onkeyup|当松开按键时运行脚本|

**鼠标事件**

|属性|描述|备注|
|:-|:-|:-|
|onclick|当单击鼠标时运行脚本|
|ondblclick|当双击鼠标时运行脚本|
|onmousedown|当按下鼠标按钮时运行脚本|
|onmousemove|当鼠标指针移动时运行脚本|
|onmouseout|当鼠标指针移出元素时运行脚本|
|onmouseover|当鼠标指针移至元素之上时运行脚本|
|onmouseup|当松开鼠标按钮时运行脚本|
|...|

**多媒体事件**

|属性|描述|备注|
|:-|:-|:-|
|onabort|当发生中止事件时运行脚本|
|onended|当媒介已抵达结尾时运行脚本|new|
|onerror|当在元素加载期间发生错误时运行脚本|new|
|...|

**其他事件**

|属性|描述|备注|
|:-|:-|:-|
|onshow|当menu元素在上下文显示时触发|new|
|ontoggle|当用户打开或关闭details元素时触发|new|


## 画布

[菜鸟画布](https://www.runoob.com/tags/ref-canvas.html)

HTML5 <canvas> 标签用于绘制图像（通过脚本，通常是 JavaScript）。

不过，<canvas> 元素本身并没有绘制能力（它仅仅是图形的容器） ，必须使用脚本来完成实际的绘图任务。

getContext() 方法可返回一个对象，该对象提供了用于在画布上绘图的方法和属性。

### 颜色、样式和阴影

| 属性                                                         | 描述                                       |
| :----------------------------------------------------------- | :----------------------------------------- |
| [fillStyle](https://www.runoob.com/tags/canvas-fillstyle.html) | 设置或返回用于填充绘画的颜色、渐变或模式。 |
| [strokeStyle](https://www.runoob.com/tags/canvas-strokestyle.html) | 设置或返回用于笔触的颜色、渐变或模式。     |
| [shadowColor](https://www.runoob.com/tags/canvas-shadowcolor.html) | 设置或返回用于阴影的颜色。                 |
| [shadowBlur](https://www.runoob.com/tags/canvas-shadowblur.html) | 设置或返回用于阴影的模糊级别。             |
| [shadowOffsetX](https://www.runoob.com/tags/canvas-shadowoffsetx.html) | 设置或返回阴影与形状的水平距离。           |
| [shadowOffsetY](https://www.runoob.com/tags/canvas-shadowoffsety.html) | 设置或返回阴影与形状的垂直距离。           |

| 方法                                                         | 描述                                      |
| :----------------------------------------------------------- | :---------------------------------------- |
| [createLinearGradient()](https://www.runoob.com/tags/canvas-createlineargradient.html) | 创建线性渐变（用在画布内容上）。          |
| [createPattern()](https://www.runoob.com/tags/canvas-createpattern.html) | 在指定的方向上重复指定的元素。            |
| [createRadialGradient()](https://www.runoob.com/tags/canvas-createradialgradient.html) | 创建放射状/环形的渐变（用在画布内容上）。 |
| [addColorStop()](https://www.runoob.com/tags/canvas-addcolorstop.html) | 规定渐变对象中的颜色和停止位置。          |

### 线条样式

| 属性                                                         | 描述                                       |
| :----------------------------------------------------------- | :----------------------------------------- |
| [lineCap](https://www.runoob.com/tags/canvas-linecap.html)   | 设置或返回线条的结束端点样式。             |
| [lineJoin](https://www.runoob.com/tags/canvas-linejoin.html) | 设置或返回两条线相交时，所创建的拐角类型。 |
| [lineWidth](https://www.runoob.com/tags/canvas-linewidth.html) | 设置或返回当前的线条宽度。                 |
| [miterLimit](https://www.runoob.com/tags/canvas-miterlimit.html) | 设置或返回最大斜接长度。                   |

### 矩形

| 方法                                                         | 描述                           |
| :----------------------------------------------------------- | :----------------------------- |
| [rect()](https://www.runoob.com/tags/canvas-rect.html)       | 创建矩形。                     |
| [fillRect()](https://www.runoob.com/tags/canvas-fillrect.html) | 绘制"被填充"的矩形。           |
| [strokeRect()](https://www.runoob.com/tags/canvas-strokerect.html) | 绘制矩形（无填充）。           |
| [clearRect()](https://www.runoob.com/tags/canvas-clearrect.html) | 在给定的矩形内清除指定的像素。 |

### 路径

| 方法                                                         | 描述                                                      |
| :----------------------------------------------------------- | :-------------------------------------------------------- |
| [fill()](https://www.runoob.com/tags/canvas-fill.html)       | 填充当前绘图（路径）。                                    |
| [stroke()](https://www.runoob.com/tags/canvas-stroke.html)   | 绘制已定义的路径。                                        |
| [beginPath()](https://www.runoob.com/tags/canvas-beginpath.html) | 起始一条路径，或重置当前路径。                            |
| [moveTo()](https://www.runoob.com/tags/canvas-moveto.html)   | 把路径移动到画布中的指定点，不创建线条。                  |
| [closePath()](https://www.runoob.com/tags/canvas-closepath.html) | 创建从当前点回到起始点的路径。                            |
| [lineTo()](https://www.runoob.com/tags/canvas-lineto.html)   | 添加一个新点，然后在画布中创建从该点到最后指定点的线条。  |
| [clip()](https://www.runoob.com/tags/canvas-clip.html)       | 从原始画布剪切任意形状和尺寸的区域。                      |
| [quadraticCurveTo()](https://www.runoob.com/tags/canvas-quadraticcurveto.html) | 创建二次贝塞尔曲线。                                      |
| [bezierCurveTo()](https://www.runoob.com/tags/canvas-beziercurveto.html) | 创建三次贝塞尔曲线。                                      |
| [arc()](https://www.runoob.com/tags/canvas-arc.html)         | 创建弧/曲线（用于创建圆形或部分圆）。                     |
| [arcTo()](https://www.runoob.com/tags/canvas-arcto.html)     | 创建两切线之间的弧/曲线。                                 |
| [isPointInPath()](https://www.runoob.com/tags/canvas-ispointinpath.html) | 如果指定的点位于当前路径中，则返回 true，否则返回 false。 |

### 转换

| 方法                                                         | 描述                                             |
| :----------------------------------------------------------- | :----------------------------------------------- |
| [scale()](https://www.runoob.com/tags/canvas-scale.html)     | 缩放当前绘图至更大或更小。                       |
| [rotate()](https://www.runoob.com/tags/canvas-rotate.html)   | 旋转当前绘图。                                   |
| [translate()](https://www.runoob.com/tags/canvas-translate.html) | 重新映射画布上的 (0,0) 位置。                    |
| [transform()](https://www.runoob.com/tags/canvas-transform.html) | 替换绘图的当前转换矩阵。                         |
| [setTransform()](https://www.runoob.com/tags/canvas-settransform.html) | 将当前转换重置为单位矩阵。然后运行 transform()。 |

### 文本

| 属性                                                         | 描述                                       |
| :----------------------------------------------------------- | :----------------------------------------- |
| [font](https://www.runoob.com/tags/canvas-font.html)         | 设置或返回文本内容的当前字体属性。         |
| [textAlign](https://www.runoob.com/tags/canvas-textalign.html) | 设置或返回文本内容的当前对齐方式。         |
| [textBaseline](https://www.runoob.com/tags/canvas-textbaseline.html) | 设置或返回在绘制文本时使用的当前文本基线。 |

| 方法                                                         | 描述                         |
| :----------------------------------------------------------- | :--------------------------- |
| [fillText()](https://www.runoob.com/tags/canvas-filltext.html) | 在画布上绘制"被填充的"文本。 |
| [strokeText()](https://www.runoob.com/tags/canvas-stroketext.html) | 在画布上绘制文本（无填充）。 |
| [measureText()](https://www.runoob.com/tags/canvas-measuretext.html) | 返回包含指定文本宽度的对象。 |

### 图像绘制

| 方法                                                         | 描述                           |
| :----------------------------------------------------------- | :----------------------------- |
| [drawImage()](https://www.runoob.com/tags/canvas-drawimage.html) | 向画布上绘制图像、画布或视频。 |

### 像素操作

| 属性                                                         | 描述                                                  |
| :----------------------------------------------------------- | :---------------------------------------------------- |
| [width](https://www.runoob.com/tags/canvas-imagedata-width.html) | 返回 ImageData 对象的宽度。                           |
| [height](https://www.runoob.com/tags/canvas-imagedata-height.html) | 返回 ImageData 对象的高度。                           |
| [data](https://www.runoob.com/tags/canvas-imagedata-data.html) | 返回一个对象，其包含指定的 ImageData 对象的图像数据。 |

| 方法                                                         | 描述                                                        |
| :----------------------------------------------------------- | :---------------------------------------------------------- |
| [createImageData()](https://www.runoob.com/tags/canvas-createimagedata.html) | 创建新的、空白的 ImageData 对象。                           |
| [getImageData()](https://www.runoob.com/tags/canvas-getimagedata.html) | 返回 ImageData 对象，该对象为画布上指定的矩形复制像素数据。 |
| [putImageData()](https://www.runoob.com/tags/canvas-putimagedata.html) | 把图像数据（从指定的 ImageData 对象）放回画布上。           |

### 合成

| 属性                                                         | 描述                                     |
| :----------------------------------------------------------- | :--------------------------------------- |
| [globalAlpha](https://www.runoob.com/tags/canvas-globalalpha.html) | 设置或返回绘图的当前 alpha 或透明值。    |
| [globalCompositeOperation](https://www.runoob.com/tags/canvas-globalcompositeoperation.html) | 设置或返回新图像如何绘制到已有的图像上。 |

### 其他

| 方法          | 描述                             |
| :------------ | :------------------------------- |
| save()        | 保存当前环境的状态。             |
| restore()     | 返回之前保存过的路径状态和属性。 |
| createEvent() |                                  |
| getContext()  |                                  |
| toDataURL()   |                                  |



## Emmet语法

| 效果                     | 代码                  | 备注                                  |
| ------------------------ | --------------------- | ------------------------------------- |
| 新建HTML                 | ！                    |                                       |
| 自动完成标签             | 直接Tab/Enter         |                                       |
| 文本操作符{}             | span{test}            | ```<span>test</span>```               |
| 属性操作符.class         | span.Sp               | ```<span class="Sp"></span>```        |
| #id                      | span#sp               | ```<span id="sp"></span>```           |
|                          |                       |                                       |
| 标签+多个class           | span.Sp1.Sp2          | ```<span class="Sp1 Sp2"></span>```   |
| 文本操作符{}             | span{test}            | ```<span>test</span>```               |
| 多个同级标签             | span+div              | ```<span></span><div></div>```        |
| 父子标签                 | ul>li                 | ```<ul><li></li></ul>```              |
| 子元素的父元素的同级元素 | div>p>span^ul>li      | p和ul同级                             |
| 超链接的href值           | a:mail,a:link         | mailto/http                           |
| 标签+属性值              | span[style=color:red] | ```<span style="color:red"></span>``` |
| 多个同级相同标签         | li*3                  | ```<li></li><li></li><li></li>```     |
| 假文                     | lorem                 | 快速输入一段用于测试的字符串          |

