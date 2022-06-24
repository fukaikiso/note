# jQuery

> [jQuery官方文档](https://api.jquery.com/)

## 1 jQuery 参考手册

### 1.1 jQuery 选择器

| 选择器                                                       | 实例                          | 选取                                                         |
| :----------------------------------------------------------- | :---------------------------- | :----------------------------------------------------------- |
| [*](https://www.runoob.com/jquery/jq-sel-all.html)           | $("*")                        | 所有元素                                                     |
| [#*id*](https://www.runoob.com/jquery/jq-sel-id.html)        | $("#lastname")                | id="lastname" 的元素                                         |
| [.*class*](https://www.runoob.com/jquery/jq-sel-class.html)  | $(".intro")                   | class="intro" 的所有元素                                     |
| [.*class,*.*class*](https://www.runoob.com/jquery/sel-multiple-classes.html) | $(".intro,.demo")             | class 为 "intro" 或 "demo" 的所有元素                        |
| [*element*](https://www.runoob.com/jquery/jq-sel-element.html) | $("p")                        | 所有 <p> 元素                                                |
| [*el1*,*el2*,*el3*](https://www.runoob.com/jquery/sel-multiple-elements.html) | $("h1,div,p")                 | 所有 <h1>、<div> 和 <p> 元素                                 |
|                                                              |                               |                                                              |
| [:first](https://www.runoob.com/jquery/sel-first.html)       | $("p:first")                  | 第一个 <p> 元素                                              |
| [:last](https://www.runoob.com/jquery/sel-last.html)         | $("p:last")                   | 最后一个 <p> 元素                                            |
| [:even](https://www.runoob.com/jquery/sel-even.html)         | $("tr:even")                  | 所有偶数 <tr> 元素，索引值从 0 开始，第一个元素是偶数 (0)，第二个元素是奇数 (1)，以此类推。 |
| [:odd](https://www.runoob.com/jquery/sel-odd.html)           | $("tr:odd")                   | 所有奇数 <tr> 元素，索引值从 0 开始，第一个元素是偶数 (0)，第二个元素是奇数 (1)，以此类推。 |
|                                                              |                               |                                                              |
| [:first-child](https://www.runoob.com/jquery/jq-sel-firstchild.html) | $("p:first-child")            | 属于其父元素的第一个子元素的所有 <p> 元素                    |
| [:first-of-type](https://www.runoob.com/jquery/sel-firstoftype.html) | $("p:first-of-type")          | 属于其父元素的第一个 <p> 元素的所有 <p> 元素                 |
| [:last-child](https://www.runoob.com/jquery/sel-lastchild.html) | $("p:last-child")             | 属于其父元素的最后一个子元素的所有 <p> 元素                  |
| [:last-of-type](https://www.runoob.com/jquery/sel-lastoftype.html) | $("p:last-of-type")           | 属于其父元素的最后一个 <p> 元素的所有 <p> 元素               |
| [:nth-child(*n*)](https://www.runoob.com/jquery/sel-nthchild.html) | $("p:nth-child(2)")           | 属于其父元素的第二个子元素的所有 <p> 元素                    |
| [:nth-last-child(*n*)](https://www.runoob.com/jquery/sel-nthlastchild.html) | $("p:nth-last-child(2)")      | 属于其父元素的第二个子元素的所有 <p> 元素，从最后一个子元素开始计数 |
| [:nth-of-type(*n*)](https://www.runoob.com/jquery/sel-nthoftype.html) | $("p:nth-of-type(2)")         | 属于其父元素的第二个 <p> 元素的所有 <p> 元素                 |
| [:nth-last-of-type(*n*)](https://www.runoob.com/jquery/sel-nthlastoftype.html) | $("p:nth-last-of-type(2)")    | 属于其父元素的第二个 <p> 元素的所有 <p> 元素，从最后一个子元素开始计数 |
| [:only-child](https://www.runoob.com/jquery/sel-onlychild.html) | $("p:only-child")             | 属于其父元素的唯一子元素的所有 <p> 元素                      |
| [:only-of-type](https://www.runoob.com/jquery/sel-onlyoftype.html) | $("p:only-of-type")           | 属于其父元素的特定类型的唯一子元素的所有 <p> 元素            |
|                                                              |                               |                                                              |
| [parent > child](https://www.runoob.com/jquery/sel-parent-child.html) | $("div > p")                  | <div> 元素的直接子元素的所有 <p> 元素                        |
| [parent descendant](https://www.runoob.com/jquery/sel-parent-descendant.html) | $("div p")                    | <div> 元素的后代的所有 <p> 元素                              |
| [element + next](https://www.runoob.com/jquery/sel-previous-next.html) | $("div + p")                  | 每个 <div> 元素相邻的下一个 <p> 元素                         |
| [element ~ siblings](https://www.runoob.com/jquery/sel-previous-siblings.html) | $("div ~ p")                  | <div> 元素同级的所有 <p> 元素                                |
|                                                              |                               |                                                              |
| [:eq(*index*)](https://www.runoob.com/jquery/sel-eq.html)    | $("ul li:eq(3)")              | 列表中的第四个元素（index 值从 0 开始）                      |
| [:gt(*no*)](https://www.runoob.com/jquery/sel-gt.html)       | $("ul li:gt(3)")              | 列举 index 大于 3 的元素                                     |
| [:lt(*no*)](https://www.runoob.com/jquery/sel-lt.html)       | $("ul li:lt(3)")              | 列举 index 小于 3 的元素                                     |
| [:not(*selector*)](https://www.runoob.com/jquery/jq-sel-not.html) | $("input:not(:empty)")        | 所有不为空的输入元素                                         |
|                                                              |                               |                                                              |
| [:header](https://www.runoob.com/jquery/sel-header.html)     | $(":header")                  | 所有标题元素 <h1>, <h2> ...                                  |
| [:animated](https://www.runoob.com/jquery/sel-animated.html) | $(":animated")                | 所有动画元素                                                 |
| [:focus](https://www.runoob.com/jquery/jq-sel-focus.html)    | $(":focus")                   | 当前具有焦点的元素                                           |
| [:contains(*text*)](https://www.runoob.com/jquery/sel-contains.html) | $(":contains('Hello')")       | 所有包含文本 "Hello" 的元素                                  |
| [:has(*selector*)](https://www.runoob.com/jquery/sel-has.html) | $("div:has(p)")               | 所有包含有 <p> 元素在其内的 <div> 元素                       |
| [:empty](https://www.runoob.com/jquery/jq-sel-empty.html)    | $(":empty")                   | 所有空元素                                                   |
| [:parent](https://www.runoob.com/jquery/sel-parent.html)     | $(":parent")                  | 匹配所有含有子元素或者文本的父元素。                         |
| [:hidden](https://www.runoob.com/jquery/sel-hidden.html)     | $("p:hidden")                 | 所有隐藏的 <p> 元素                                          |
| [:visible](https://www.runoob.com/jquery/sel-visible.html)   | $("table:visible")            | 所有可见的表格                                               |
| [:root](https://www.runoob.com/jquery/jq-sel-root.html)      | $(":root")                    | 文档的根元素                                                 |
| [:lang(*language*)](https://www.runoob.com/jquery/jq-sel-lang.html) | $("p:lang(de)")               | 所有 lang 属性值为 "de" 的 <p> 元素                          |
|                                                              |                               |                                                              |
| [[*attribute*\]](https://www.runoob.com/jquery/jq-sel-attribute.html) | $("[href]")                   | 所有带有 href 属性的元素                                     |
| [[*attribute*=*value*\]](https://www.runoob.com/jquery/sel-attribute-equal-value.html) | $("[href='default.htm']")     | 所有带有 href 属性且值等于 "default.htm" 的元素              |
| [[*attribute*!=*value*\]](https://www.runoob.com/jquery/sel-attribute-notequal-value.html) | $("[href!='default.htm']")    | 所有带有 href 属性且值不等于 "default.htm" 的元素            |
| [[*attribute*$=*value*\]](https://www.runoob.com/jquery/sel-attribute-end-value.html) \| | $ ("[href$='.jpg']")          | 所有带有 href 属性且值以 ".jpg" 结尾的元素                   |
| [[*attribute*\|=*value*\]](https://www.runoob.com/jquery/sel-attribute-prefix-value.html) | $("[title\|='Tomorrow']")     | 所有带有 title 属性且值等于 'Tomorrow' 或者以 'Tomorrow' 后跟连接符作为开头的字符串 |
| [[*attribute*^=*value*\]](https://www.runoob.com/jquery/sel-attribute-beginning-value.html) | $("[title^='Tom']")           | 所有带有 title 属性且值以 "Tom" 开头的元素                   |
| [[*attribute*~=*value*\]](https://www.runoob.com/jquery/sel-attribute-contains-value.html) | $("[title~='hello']")         | 所有带有 title 属性且值包含单词 "hello" 的元素               |
| [[*attribute**=*value*\]](https://www.runoob.com/jquery/sel-attribute-contains-string-value.html) | $("[title*='hello']")         | 所有带有 title 属性且值包含字符串 "hello" 的元素             |
| [[*name*=*value*\][*name2*=*value2*]](https://www.runoob.com/jquery/sel-multipleattribute-equal-value.html) | $( "input[id][name$='man']" ) | 带有 id 属性，并且 name 属性以 man 结尾的输入框              |
|                                                              |                               |                                                              |
| [:input](https://www.runoob.com/jquery/sel-input.html)       | $(":input")                   | 所有 input 元素                                              |
| [:text](https://www.runoob.com/jquery/sel-input-text.html)   | $(":text")                    | 所有带有 type="text" 的 input 元素                           |
| [:password](https://www.runoob.com/jquery/sel-input-password.html) | $(":password")                | 所有带有 type="password" 的 input 元素                       |
| [:radio](https://www.runoob.com/jquery/sel-input-radio.html) | $(":radio")                   | 所有带有 type="radio" 的 input 元素                          |
| [:checkbox](https://www.runoob.com/jquery/sel-input-checkbox.html) | $(":checkbox")                | 所有带有 type="checkbox" 的 input 元素                       |
| [:submit](https://www.runoob.com/jquery/sel-input-submit.html) | $(":submit")                  | 所有带有 type="submit" 的 input 元素                         |
| [:reset](https://www.runoob.com/jquery/sel-input-reset.html) | $(":reset")                   | 所有带有 type="reset" 的 input 元素                          |
| [:button](https://www.runoob.com/jquery/sel-input-button.html) | $(":button")                  | 所有带有 type="button" 的 input 元素                         |
| [:image](https://www.runoob.com/jquery/sel-input-image.html) | $(":image")                   | 所有带有 type="image" 的 input 元素                          |
| [:file](https://www.runoob.com/jquery/sel-input-file.html)   | $(":file")                    | 所有带有 type="file" 的 input 元素                           |
| [:enabled](https://www.runoob.com/jquery/sel-input-enabled.html) | $(":enabled")                 | 所有启用的元素                                               |
| [:disabled](https://www.runoob.com/jquery/sel-input-disabled.html) | $(":disabled")                | 所有禁用的元素                                               |
| [:selected](https://www.runoob.com/jquery/sel-input-selected.html) | $(":selected")                | 所有选定的下拉列表元素                                       |
| [:checked](https://www.runoob.com/jquery/sel-input-checked.html) | $(":checked")                 | 所有选中的复选框选项                                         |
| .selector                                                    | $(selector).selector          | 在jQuery 1.7中已经不被赞成使用。返回传给jQuery()的原始选择器 |
| [:target](https://www.runoob.com/jquery/jq-sel-target.html)  | $( "p:target" )               | 选择器将选中ID和URI中一个格式化的标识符相匹配的<p>元素       |

### 1.2 jQuery 事件方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [bind()](https://www.runoob.com/jquery/event-bind.html)      | 向元素添加事件处理程序                                       |
| [blur()](https://www.runoob.com/jquery/event-blur.html)      | 添加/触发失去焦点事件                                        |
| [change()](https://www.runoob.com/jquery/event-change.html)  | 添加/触发 change 事件                                        |
| [click()](https://www.runoob.com/jquery/event-click.html)    | 添加/触发 click 事件                                         |
| [dblclick()](https://www.runoob.com/jquery/event-dblclick.html) | 添加/触发 double click 事件                                  |
| [delegate()](https://www.runoob.com/jquery/event-delegate.html) | 向匹配元素的当前或未来的子元素添加处理程序                   |
| [die()](https://www.runoob.com/jquery/event-die.html)        | 在版本 1.9 中被移除。移除所有通过 live() 方法添加的事件处理程序 |
| [error()](https://www.runoob.com/jquery/event-error.html)    | 在版本 1.8 中被废弃。添加/触发 error 事件                    |
| [event.currentTarget](https://www.runoob.com/jquery/jq-event-currenttarget.html) | 在事件冒泡阶段内的当前 DOM 元素                              |
| [event.data](https://www.runoob.com/jquery/event-data.html)  | 包含当前执行的处理程序被绑定时传递到事件方法的可选数据       |
| [event.delegateTarget](https://www.runoob.com/jquery/event-delegatetarget.html) | 返回当前调用的 jQuery 事件处理程序所添加的元素               |
| [event.isDefaultPrevented()](https://www.runoob.com/jquery/event-isdefaultprevented.html) | 返回指定的 event 对象上是否调用了 event.preventDefault()     |
| [event.isImmediatePropagationStopped()](https://www.runoob.com/jquery/event-isimmediatepropagationstopped.html) | 返回指定的 event 对象上是否调用了 event.stopImmediatePropagation() |
| [event.isPropagationStopped()](https://www.runoob.com/jquery/event-ispropagationstopped.html) | 返回指定的 event 对象上是否调用了 event.stopPropagation()    |
| [event.namespace](https://www.runoob.com/jquery/event-namespace.html) | 返回当事件被触发时指定的命名空间                             |
| [event.pageX](https://www.runoob.com/jquery/event-pagex.html) | 返回相对于文档左边缘的鼠标位置                               |
| [event.pageY](https://www.runoob.com/jquery/event-pagey.html) | 返回相对于文档上边缘的鼠标位置                               |
| [event.preventDefault()](https://www.runoob.com/jquery/event-preventdefault.html) | 阻止事件的默认行为                                           |
| [event.relatedTarget](https://www.runoob.com/jquery/jq-event-relatedtarget.html) | 返回当鼠标移动时哪个元素进入或退出                           |
| [event.result](https://www.runoob.com/jquery/event-result.html) | 包含由被指定事件触发的事件处理程序返回的最后一个值           |
| [event.stopImmediatePropagation()](https://www.runoob.com/jquery/event-stopimmediatepropagation.html) | 阻止其他事件处理程序被调用                                   |
| [event.stopPropagation()](https://www.runoob.com/jquery/event-stoppropagation.html) | 阻止事件向上冒泡到 DOM 树，阻止任何父处理程序被事件通知      |
| [event.target](https://www.runoob.com/jquery/jq-event-target.html) | 返回哪个 DOM 元素触发事件                                    |
| [event.timeStamp](https://www.runoob.com/jquery/jq-event-timestamp.html) | 返回从 1970 年 1 月 1 日到事件被触发时的毫秒数               |
| [event.type](https://www.runoob.com/jquery/jq-event-type.html) | 返回哪种事件类型被触发                                       |
| [event.which](https://www.runoob.com/jquery/event-which.html) | 返回指定事件上哪个键盘键或鼠标按钮被按下                     |
| [event.metaKey](https://www.runoob.com/jquery/event_metakey.html) | 事件触发时 META 键是否被按下                                 |
| [focus()](https://www.runoob.com/jquery/event-focus.html)    | 添加/触发 focus 事件                                         |
| [focusin()](https://www.runoob.com/jquery/event-focusin.html) | 添加事件处理程序到 focusin 事件                              |
| [focusout()](https://www.runoob.com/jquery/event-focusout.html) | 添加事件处理程序到 focusout 事件                             |
| [hover()](https://www.runoob.com/jquery/event-hover.html)    | 添加两个事件处理程序到 hover 事件                            |
| [keydown()](https://www.runoob.com/jquery/event-keydown.html) | 添加/触发 keydown 事件                                       |
| [keypress()](https://www.runoob.com/jquery/event-keypress.html) | 添加/触发 keypress 事件                                      |
| [keyup()](https://www.runoob.com/jquery/event-keyup.html)    | 添加/触发 keyup 事件                                         |
| [live()](https://www.runoob.com/jquery/event-live.html)      | 在版本 1.9 中被移除。添加一个或多个事件处理程序到当前或未来的被选元素 |
| [load()](https://www.runoob.com/jquery/event-load.html)      | 在版本 1.8 中被废弃。添加一个事件处理程序到 load 事件        |
| [mousedown()](https://www.runoob.com/jquery/event-mousedown.html) | 添加/触发 mousedown 事件                                     |
| [mouseenter()](https://www.runoob.com/jquery/event-mouseenter.html) | 添加/触发 mouseenter 事件                                    |
| [mouseleave()](https://www.runoob.com/jquery/event-mouseleave.html) | 添加/触发 mouseleave 事件                                    |
| [mousemove()](https://www.runoob.com/jquery/event-mousemove.html) | 添加/触发 mousemove 事件                                     |
| [mouseout()](https://www.runoob.com/jquery/event-mouseout.html) | 添加/触发 mouseout 事件                                      |
| [mouseover()](https://www.runoob.com/jquery/event-mouseover.html) | 添加/触发 mouseover 事件                                     |
| [mouseup()](https://www.runoob.com/jquery/event-mouseup.html) | 添加/触发 mouseup 事件                                       |
| [off()](https://www.runoob.com/jquery/event-off.html)        | 移除通过 on() 方法添加的事件处理程序                         |
| [on()](https://www.runoob.com/jquery/event-on.html)          | 向元素添加事件处理程序                                       |
| [one()](https://www.runoob.com/jquery/event-one.html)        | 向被选元素添加一个或多个事件处理程序。该处理程序只能被每个元素触发一次 |
| [$.proxy()](https://www.runoob.com/jquery/event-proxy.html)  | 接受一个已有的函数，并返回一个带特定上下文的新的函数         |
| [ready()](https://www.runoob.com/jquery/event-ready.html)    | 规定当 DOM 完全加载时要执行的函数                            |
| [resize()](https://www.runoob.com/jquery/event-resize.html)  | 添加/触发 resize 事件                                        |
| [scroll()](https://www.runoob.com/jquery/event-scroll.html)  | 添加/触发 scroll 事件                                        |
| [select()](https://www.runoob.com/jquery/event-select.html)  | 添加/触发 select 事件                                        |
| [submit()](https://www.runoob.com/jquery/event-submit.html)  | 添加/触发 submit 事件                                        |
| [toggle()](https://www.runoob.com/jquery/event-toggle.html)  | 在版本 1.9 中被移除。添加 click 事件之间要切换的两个或多个函数 |
| [trigger()](https://www.runoob.com/jquery/event-trigger.html) | 触发绑定到被选元素的所有事件                                 |
| [triggerHandler()](https://www.runoob.com/jquery/event-triggerhandler.html) | 触发绑定到被选元素的指定事件上的所有函数                     |
| [unbind()](https://www.runoob.com/jquery/event-unbind.html)  | 从被选元素上移除添加的事件处理程序                           |
| [undelegate()](https://www.runoob.com/jquery/event-undelegate.html) | 从现在或未来的被选元素上移除事件处理程序                     |
| [unload()](https://www.runoob.com/jquery/event-unload.html)  | 在版本 1.8 中被废弃。添加事件处理程序到 unload 事件          |
| [contextmenu()](https://www.runoob.com/jquery/event-contextmenu.html) | 添加事件处理程序到 contextmenu 事件                          |
| [$.holdReady()](https://www.runoob.com/jquery/event-holdready.html) | 用于暂停或恢复.ready() 事件的执行                            |

### 1.3 jQuery 效果方法

| 方法                                                         | 描述                                         |
| :----------------------------------------------------------- | :------------------------------------------- |
| [animate()](https://www.runoob.com/jquery/eff-animate.html)  | 对被选元素应用"自定义"的动画                 |
| [clearQueue()](https://www.runoob.com/jquery/eff-clearqueue.html) | 对被选元素移除所有排队函数（仍未运行的）     |
| [delay()](https://www.runoob.com/jquery/eff-delay.html)      | 对被选元素的所有排队函数（仍未运行）设置延迟 |
| [dequeue()](https://www.runoob.com/jquery/eff-dequeue.html)  | 移除下一个排队函数，然后执行函数             |
| [fadeIn()](https://www.runoob.com/jquery/eff-fadein.html)    | 逐渐改变被选元素的不透明度，从隐藏到可见     |
| [fadeOut()](https://www.runoob.com/jquery/eff-fadeout.html)  | 逐渐改变被选元素的不透明度，从可见到隐藏     |
| [fadeTo()](https://www.runoob.com/jquery/eff-fadeto.html)    | 把被选元素逐渐改变至给定的不透明度           |
| [fadeToggle()](https://www.runoob.com/jquery/eff-fadetoggle.html) | 在 fadeIn() 和 fadeOut() 方法之间进行切换    |
| [finish()](https://www.runoob.com/jquery/eff-finish.html)    | 对被选元素停止、移除并完成所有排队动画       |
| [hide()](https://www.runoob.com/jquery/eff-hide.html)        | 隐藏被选元素                                 |
| [queue()](https://www.runoob.com/jquery/eff-queue.html)      | 显示被选元素的排队函数                       |
| [show()](https://www.runoob.com/jquery/eff-show.html)        | 显示被选元素                                 |
| [slideDown()](https://www.runoob.com/jquery/eff-slidedown.html) | 通过调整高度来滑动显示被选元素               |
| [slideToggle()](https://www.runoob.com/jquery/eff-slidetoggle.html) | slideUp() 和 slideDown() 方法之间的切换      |
| [slideUp()](https://www.runoob.com/jquery/eff-slideup.html)  | 通过调整高度来滑动隐藏被选元素               |
| [stop()](https://www.runoob.com/jquery/eff-stop.html)        | 停止被选元素上当前正在运行的动画             |
| [toggle()](https://www.runoob.com/jquery/eff-toggle.html)    | hide() 和 show() 方法之间的切换              |

### 1.4 jQuery HTML / CSS 方法

| 方法                                                         | 描述                                              |
| :----------------------------------------------------------- | :------------------------------------------------ |
| [addClass()](https://www.runoob.com/jquery/html-addclass.html) | 向被选元素添加一个或多个类名                      |
| [after()](https://www.runoob.com/jquery/html-after.html)     | 在被选元素后插入内容                              |
| [append()](https://www.runoob.com/jquery/html-append.html)   | 在被选元素的结尾插入内容                          |
| [appendTo()](https://www.runoob.com/jquery/html-appendto.html) | 在被选元素的结尾插入 HTML 元素                    |
| [attr()](https://www.runoob.com/jquery/html-attr.html)       | 设置或返回被选元素的属性/值                       |
| [before()](https://www.runoob.com/jquery/html-before.html)   | 在被选元素前插入内容                              |
| [clone()](https://www.runoob.com/jquery/html-clone.html)     | 生成被选元素的副本                                |
| [css()](https://www.runoob.com/jquery/css-css.html)          | 为被选元素设置或返回一个或多个样式属性            |
| [detach()](https://www.runoob.com/jquery/html-detach.html)   | 移除被选元素（保留数据和事件）                    |
| [empty()](https://www.runoob.com/jquery/html-empty.html)     | 从被选元素移除所有子节点和内容                    |
| [hasClass()](https://www.runoob.com/jquery/html-hasclass.html) | 检查被选元素是否包含指定的 class 名称             |
| [height()](https://www.runoob.com/jquery/css-height.html)    | 设置或返回被选元素的高度                          |
| [html()](https://www.runoob.com/jquery/html-html.html)       | 设置或返回被选元素的内容                          |
| [innerHeight()](https://www.runoob.com/jquery/html-innerheight.html) | 返回元素的高度（包含 padding，不包含 border）     |
| [innerWidth()](https://www.runoob.com/jquery/html-innerwidth.html) | 返回元素的宽度（包含 padding，不包含 border）     |
| [insertAfter()](https://www.runoob.com/jquery/html-insertafter.html) | 在被选元素后插入 HTML 元素                        |
| [insertBefore()](https://www.runoob.com/jquery/html-insertbefore.html) | 在被选元素前插入 HTML 元素                        |
| [offset()](https://www.runoob.com/jquery/css-offset.html)    | 设置或返回被选元素的偏移坐标（相对于文档）        |
| [offsetParent()](https://www.runoob.com/jquery/css-offsetparent.html) | 返回第一个定位的祖先元素                          |
| [outerHeight()](https://www.runoob.com/jquery/html-outerheight.html) | 返回元素的高度（包含 padding 和 border）          |
| [outerWidth()](https://www.runoob.com/jquery/html-outerwidth.html) | 返回元素的宽度（包含 padding 和 border）          |
| [position()](https://www.runoob.com/jquery/css-position.html) | 返回元素的位置（相对于父元素）                    |
| [prepend()](https://www.runoob.com/jquery/html-prepend.html) | 在被选元素的开头插入内容                          |
| [prependTo()](https://www.runoob.com/jquery/html-prependto.html) | 在被选元素的开头插入 HTML 元素                    |
| [prop()](https://www.runoob.com/jquery/html-prop.html)       | 设置或返回被选元素的属性/值                       |
| [remove()](https://www.runoob.com/jquery/html-remove.html)   | 移除被选元素（包含数据和事件）                    |
| [removeAttr()](https://www.runoob.com/jquery/html-removeattr.html) | 从被选元素移除一个或多个属性                      |
| [removeClass()](https://www.runoob.com/jquery/html-removeclass.html) | 从被选元素移除一个或多个类                        |
| [removeProp()](https://www.runoob.com/jquery/html-removeprop.html) | 移除通过 prop() 方法设置的属性                    |
| [replaceAll()](https://www.runoob.com/jquery/html-replaceall.html) | 把被选元素替换为新的 HTML 元素                    |
| [replaceWith()](https://www.runoob.com/jquery/html-replacewith.html) | 把被选元素替换为新的内容                          |
| [scrollLeft()](https://www.runoob.com/jquery/css-scrollleft.html) | 设置或返回被选元素的水平滚动条位置                |
| [scrollTop()](https://www.runoob.com/jquery/css-scrolltop.html) | 设置或返回被选元素的垂直滚动条位置                |
| [text()](https://www.runoob.com/jquery/html-text.html)       | 设置或返回被选元素的文本内容                      |
| [toggleClass()](https://www.runoob.com/jquery/html-toggleclass.html) | 在被选元素中添加/移除一个或多个类之间切换         |
| [unwrap()](https://www.runoob.com/jquery/html-unwrap.html)   | 移除被选元素的父元素                              |
| [val()](https://www.runoob.com/jquery/html-val.html)         | 设置或返回被选元素的属性值（针对表单元素）        |
| [width()](https://www.runoob.com/jquery/css-width.html)      | 设置或返回被选元素的宽度                          |
| [wrap()](https://www.runoob.com/jquery/html-wrap.html)       | 在每个被选元素的周围用 HTML 元素包裹起来          |
| [wrapAll()](https://www.runoob.com/jquery/html-wrapall.html) | 在所有被选元素的周围用 HTML 元素包裹起来          |
| [wrapInner()](https://www.runoob.com/jquery/html-wrapinner.html) | 在每个被选元素的内容周围用 HTML 元素包裹起来      |
| [$.escapeSelector()](https://www.runoob.com/jquery/html-escapeSelector.html) | 转义CSS选择器中有特殊意义的字符或字符串           |
| [$.cssHooks](https://www.runoob.com/jquery/html-csshooks.html) | 提供了一种方法通过定义函数来获取和设置特定的CSS值 |

### 1.5 jQuery 遍历方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [add()](https://www.runoob.com/jquery/traversing-add.html)   | 把元素添加到匹配元素的集合中                                 |
| addBack()                                                    | 把之前的元素集添加到当前集合中                               |
| andSelf()                                                    | 在版本 1.8 中被废弃。addBack() 的别名                        |
| [children()](https://www.runoob.com/jquery/traversing-children.html) | 返回被选元素的所有直接子元素                                 |
| [closest()](https://www.runoob.com/jquery/traversing-closest.html) | 返回被选元素的第一个祖先元素                                 |
| [contents()](https://www.runoob.com/jquery/traversing-contents.html) | 返回被选元素的所有直接子元素（包含文本和注释节点）           |
| [each()](https://www.runoob.com/jquery/traversing-each.html) | 为每个匹配元素执行函数                                       |
| end()                                                        | 结束当前链中最近的一次筛选操作，并把匹配元素集合返回到前一次的状态 |
| [eq()](https://www.runoob.com/jquery/traversing-eq.html)     | 返回带有被选元素的指定索引号的元素                           |
| [filter()](https://www.runoob.com/jquery/traversing-filter.html) | 把匹配元素集合缩减为匹配选择器或匹配函数返回值的新元素       |
| [find()](https://www.runoob.com/jquery/traversing-find.html) | 返回被选元素的后代元素                                       |
| [first()](https://www.runoob.com/jquery/traversing-first.html) | 返回被选元素的第一个元素                                     |
| [has()](https://www.runoob.com/jquery/traversing-has.html)   | 返回拥有一个或多个元素在其内的所有元素                       |
| [is()](https://www.runoob.com/jquery/traversing-is.html)     | 根据选择器/元素/jQuery 对象检查匹配元素集合，如果存在至少一个匹配元素，则返回 true |
| [last()](https://www.runoob.com/jquery/traversing-last.html) | 返回被选元素的最后一个元素                                   |
| map()                                                        | 把当前匹配集合中的每个元素传递给函数，产生包含返回值的新 jQuery 对象 |
| [next()](https://www.runoob.com/jquery/traversing-next.html) | 返回被选元素的后一个同级元素                                 |
| [nextAll()](https://www.runoob.com/jquery/traversing-nextall.html) | 返回被选元素之后的所有同级元素                               |
| [nextUntil()](https://www.runoob.com/jquery/traversing-nextuntil.html) | 返回介于两个给定参数之间的每个元素之后的所有同级元素         |
| [not()](https://www.runoob.com/jquery/traversing-not.html)   | 从匹配元素集合中移除元素                                     |
| [offsetParent()](https://www.runoob.com/jquery/traversing-offsetparent.html) | 返回第一个定位的父元素                                       |
| [parent()](https://www.runoob.com/jquery/traversing-parent.html) | 返回被选元素的直接父元素                                     |
| [parents()](https://www.runoob.com/jquery/traversing-parents.html) | 返回被选元素的所有祖先元素                                   |
| [parentsUntil()](https://www.runoob.com/jquery/traversing-parentsuntil.html) | 返回介于两个给定参数之间的所有祖先元素                       |
| [prev()](https://www.runoob.com/jquery/traversing-prev.html) | 返回被选元素的前一个同级元素                                 |
| [prevAll()](https://www.runoob.com/jquery/traversing-prevall.html) | 返回被选元素之前的所有同级元素                               |
| [prevUntil()](https://www.runoob.com/jquery/traversing-prevuntil.html) | 返回介于两个给定参数之间的每个元素之前的所有同级元素         |
| [siblings()](https://www.runoob.com/jquery/traversing-siblings.html) | 返回被选元素的所有同级元素                                   |
| [slice()](https://www.runoob.com/jquery/traversing-slice.html) | 把匹配元素集合缩减为指定范围的子集                           |

### 1.6 jQuery AJAX 方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [$.ajax()](https://www.runoob.com/jquery/ajax-ajax.html)     | 执行异步 AJAX 请求                                           |
| $.ajaxPrefilter()                                            | 在每个请求发送之前且被$.ajax() 处理之前，处理自定义 Ajax 选项或修改已存在选项 |
| [$.ajaxSetup()](https://www.runoob.com/jquery/ajax-ajaxsetup.html) | 为将来的 AJAX 请求设置默认值                                 |
| $.ajaxTransport()                                            | 创建处理 Ajax 数据实际传送的对象                             |
| [$.get()](https://www.runoob.com/jquery/ajax-get.html)       | 使用 AJAX 的 HTTP GET 请求从服务器加载数据                   |
| [$.getJSON()](https://www.runoob.com/jquery/ajax-getjson.html) | 使用 HTTP GET 请求从服务器加载 JSON 编码的数据               |
| [$.getScript()](https://www.runoob.com/jquery/ajax-getscript.html) | 使用 AJAX 的 HTTP GET 请求从服务器加载并执行 JavaScript      |
| [$.param()](https://www.runoob.com/jquery/ajax-param.html)   | 创建数组或对象的序列化表示形式（可用于 AJAX 请求的 URL 查询字符串） |
| [$.post()](https://www.runoob.com/jquery/ajax-post.html)     | 使用 AJAX 的 HTTP POST 请求从服务器加载数据                  |
| [ajaxComplete()](https://www.runoob.com/jquery/ajax-ajaxcomplete.html) | 规定 AJAX 请求完成时运行的函数                               |
| [ajaxError()](https://www.runoob.com/jquery/ajax-ajaxerror.html) | 规定 AJAX 请求失败时运行的函数                               |
| [ajaxSend()](https://www.runoob.com/jquery/ajax-ajaxsend.html) | 规定 AJAX 请求发送之前运行的函数                             |
| [ajaxStart()](https://www.runoob.com/jquery/ajax-ajaxstart.html) | 规定第一个 AJAX 请求开始时运行的函数                         |
| [ajaxStop()](https://www.runoob.com/jquery/ajax-ajaxstop.html) | 规定所有的 AJAX 请求完成时运行的函数                         |
| [ajaxSuccess()](https://www.runoob.com/jquery/ajax-ajaxsuccess.html) | 规定 AJAX 请求成功完成时运行的函数                           |
| [load()](https://www.runoob.com/jquery/ajax-load.html)       | 从服务器加载数据，并把返回的数据放置到指定的元素中           |
| [serialize()](https://www.runoob.com/jquery/ajax-serialize.html) | 编码表单元素集为字符串以便提交                               |
| [serializeArray()](https://www.runoob.com/jquery/ajax-serializearray.html) | 编码表单元素集为 names 和 values 的数组                      |

**应用实例**

1.get

```html
<body>
    <div id="box"></div>

    <script src="./vendor/jquery-3.6.0.min.js"></script>
    <script>
        const url = 'https://api.xin88.top/game/items.json'

        $.get(url, data => {
            //console.log(data);
            const els = data.items.map(i => {
                const { name, iconPath, price } = i
                return `<div>
                    <img src="${iconPath}" alt="">
                    <span>${name}</span>
                    <span>${price}</span>
                </div>`
            })

            $('#box').append(els)
        })
    </script>
</body>
```



### 1.7 jQuery 杂项方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [data()](https://www.runoob.com/jquery/misc-data.html)       | 向被选元素附加数据，或者从被选元素获取数据                   |
| [each()](https://www.runoob.com/jquery/misc-each.html)       | 为每个匹配元素执行函数                                       |
| [get()](https://www.runoob.com/jquery/misc-get.html)         | 获取由选择器指定的 DOM 元素                                  |
| [index()](https://www.runoob.com/jquery/misc-index.html)     | 从匹配元素中搜索给定元素                                     |
| [$.noConflict()](https://www.runoob.com/jquery/misc-noconflict.html) | 释放变量 $ 的 jQuery 控制权                                  |
| [$.param()](https://www.runoob.com/jquery/misc-param.html)   | 创建数组或对象的序列化表示形式（可在生成 AJAX 请求时用于 URL 查询字符串中） |
| [removeData()](https://www.runoob.com/jquery/misc-removedata.html) | 移除之前存放的数据                                           |
| [size()](https://www.runoob.com/jquery/misc-size.html)       | 在版本 1.8 中被废弃。返回被 jQuery 选择器匹配的 DOM 元素的数量 |
| [toArray()](https://www.runoob.com/jquery/misc-toarray.html) | 以数组的形式检索所有包含在 jQuery 集合中的所有 DOM 元素      |
| [pushStack()](https://www.runoob.com/jquery/misc-pushstack.html) | 将一个DOM元素集合加入到jQuery栈                              |
| [$.when()](https://www.runoob.com/jquery/misc-when.html)     | 提供一种方法来执行一个或多个对象的回调函数                   |

### 1.8 jQuery 属性

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [context](https://www.runoob.com/jquery/prop-context.html)   | 在版本 1.10 中被废弃。包含被传递到 jQuery 的原始上下文       |
| [jquery](https://www.runoob.com/jquery/prop-jquery.html)     | 包含 jQuery 的版本号                                         |
| [jQuery.fx.interval](https://www.runoob.com/jquery/prop-jquery-fx-interval.html) | 改变以毫秒计的动画运行速率                                   |
| [jQuery.fx.off](https://www.runoob.com/jquery/prop-jquery-fx-off.html) | 对所有动画进行全局禁用或启用                                 |
| [jQuery.support](https://www.runoob.com/jquery/prop-jquery-support.html) | 包含表示不同浏览器特性或漏洞的属性集（主要用于 jQuery 的内部使用） |
| [length](https://www.runoob.com/jquery/prop-length.html)     | 包含 jQuery 对象中元素的数目                                 |
| [jQuery.cssNumber](https://www.runoob.com/jquery/prop-cssnumber.html) | 包含所有可以不使用单位的CSS属性的对象                        |



## 2 jQuery重点

> jQuery: 是通过封装技巧 把原生的 DOM 操作封装成一个对象
>
> - 理念: `write less, do more` -- 写的少,做的多
> - 一款生产力工具, 利用其实际工作 编写代码

- 封装的核心理念
  - 简化代码: 比如用 `$` 代替 `document.querySelectorAll`
  - 自带遍历: 提供了很多方法, 都自带遍历
  - 函数重载: 参数的 个数/类型 不同, 执行不同的逻辑
- 选择元素: `$(css选择器)`
- `eq(n)`: 可以从查询出来的元素中, 获取序号n的
- style操作
  - `css(属性名, 值)`: 设置单个
  - `css({ 属性名:值, 属性名:值 })`:设置多个
  - `css(属性名)`: 读取属性的值
- class操作
  - addClass: 添加
  - removeClass: 删除
  - toggleClass: 切换
  - hasClass: 判断有没有
- siblings(): 查询到所有兄弟元素
- 事件
  - `click( function(){} ) `

- 显示与隐藏

  - 普通方式: show 和 hide
  - 滑动方式: slide...  带有收起或展开的动画
  - 透明度: fade...  
  - 自定义动画: animate   `不支持颜色和transform`

- 属性的读取

  - 系统属性: `prop` 和 attr
  - 自定义属性: data

- 选择器, 利用序号从查询结果中选择

  - lt: 小于
  - gt: 大于
  - eq: 等于

- 兄弟关系

  - next:下一个兄弟
  - prev:上一个兄弟

- index: 获取一个元素在 子元素中的序号

- 更多的选择器

  - 上方的兄弟们: `prevAll`
  - 下方的兄弟们: `nextAll`
  - 内容中包含: `contains`
- 准备就绪

  - 当在外部JS文件中书写, 需要把代码放在 `$(function(){  })` 中执行
  - 使用外部JS文件, `理论上` 应该在body的最后进行引入.
  - 防止使用者 在`head`中引入, 导致DOM未加载前 就使用了JS的情况

- 输入框事件

  - 焦点 focus
  - 失去焦点 blur
  - 变化 change
  - 实时变化 input
    - 作者没有封装对应函数, 需要使用通用事件绑定语法: `on`
  - 键盘 keyup
    - 通过事件参数 读取按键编号 keyCode 区分按键,  13是回车

- 新增子元素: `append`

- 委托: 通过on 携带3个参数实现

  - `on(事件名, '选择器,选中指定的子元素', 回调函数)`
  - this指向:修改为触发事件的当事元素
  - 委托模式适合场景: 动态新增的子元素

- 删除元素: remove

- 克隆: clone 复制元素

- 替换: replaceWith

- ajax: 

  - get请求:  `$.get(请求地址, 回调函数)`   回调函数接收到数据

- Ajax
  - get请求: 适合`从`服务器获取数据
  - post请求: 适合`向`服务器发送数据
  - load: 加载其他的HTML文件
    - 大型网页中, html需要拆分到外部复用的场景   -- `模块化`


- Express服务器

  - 通过 Express 服务器制作接口 配合 ajax 使用


  - `跨域`: 如果网页通过ajax请求数据, 数据所在的接口服务器和当前网页非同一个, 就会触发`浏览器`的`同源策略`

    解决方案:

    - CORS: `最推荐` -- 在服务器上添加一个`白名单`, 如果发送请求的来源 属于白名单范围, 就能正常访问, 不会被拒绝
    - PROXY: 代理 -- 适合服务器代码不可修改的场景
      - 例如: 使用斗鱼的接口, 但是遭遇跨域报错 -- 无法修改

## 基础使用

```js
// app.js
// 引入模块 -> 调用得到服务器对象app
const express = require('express')

const app = express()

// 监听3000端口 -- 可以自行修改, 有冲突的可能
app.listen(3000, ()=>{
  console.log('服务器开启成功!');
})

// 启动有两种方式: 在my-server 目录下打开命令行
// 方式1: node app.js
//     -- 特点: 每次app.js代码有修改, 必须重新启动

// 方式2: nodemon app.js
//    -- 特点: app.js代码有修改, 自动重启.  前提要安装nodemon模块


// 服务器分两类功能
// 1. 静态托管服务器  - 管理静态文件(html 图片 视频 音频之类.. 文件类型)

// 配置 public 文件夹作为静态托管的
app.use(express.static('public'))
// 访问 localhost:3000 查看静态文件 index.html
// 注意1: node方式启动, 需要重启服务器才能生效
// 注意2: 根据你的端口来访问对应路径
// 凡是存储在 public 目录下的东西, 都能通过服务器直接访问
// 例如 localhost:3000/heros/Zoe.png 可以看到图


// 2. 接口服务器 -- 与数据库进行交互
// 接口: 用来连接数据库操作
// 前端通过地址访问接口, 接口帮你到数据库查数据

// 一个提供数据给前端的接口: 用get请求
// localhost:3000/zz_info
app.get('/zz_info', (req, res)=>{
  // 理论上: 用sql 查询数据库得到数据
  // 做假数据
  const data = {
    name:"...",
    nickname:"...",
    skills:['...', '...', '...'],
    hobby:'...',
    photo:'Galio.png'
  }
  // 发送给用户   response:响应
  res.send(data)
})
```

## 跨域

```js
const express = require('express')

const app = express()
app.listen(3000, ()=>{
  console.log('服务器开启成功!');
})

app.use(express.static('public'))

// 在所有的接口前, 添加一个拦截器 -- 中间件
// 理解成: 小区卡口, 来访人员必须扫码登记 才能通过
// all: 全部; 所有类型的请求, 例如 get post 等
// * : 通配符, 匹配所有的接口地址
// 即: 所有的请求,所有的接口 都会进入当前拦截器
app.all('*', (req, res, next)=>{
  // 响应头中,添加一个设置:
  // (允许来自特殊指定来源的访问, '具体地址')
  // res.header('Access-Control-Allow-Origin', 'http://127.0.0.1:3000')
  // 利用 * 可以统配所有来源的访问
  res.header('Access-Control-Allow-Origin', '*')
  
  // 那允许某几个访问怎么办?  需要第三方模块 cors 才能实现
  // -- 下回分解!

  // 下一步:  拦截器放行;   相当于扫码完毕 可以进入办公楼
  next()
})


app.get('/zz_info', (req, res)=>{
  const data = {
    name:"...",
    nickname:"...",
    skills:['...', '...', '...'],
    hobby:'...',
    photo:'Galio.png'
  }
  // 发送给用户   response:响应
  res.send(data)
})
```

## cors模块

```js
const express = require('express')
// 安装cors模块: npm i cors    在my-server目录下执行
const cors = require('cors')

const app = express()
app.listen(3000, ()=>{
  console.log('服务器开启成功!');
})

app.use(express.static('public'))

// 在所有接口前书写:
// app.use(cors())  //解决跨域: 允许所有来源

// 白名单: 指定某几个
app.use(cors({
  // 把允许的域名放在数组里即可
  origin:['http://127.0.0.1:3000', 'http://127.0.0.1:5500']
}))


app.get('/zz_info', (req, res)=>{
  const data = {
    name:"...",
    nickname:"...",
    skills:['...', '...', '...'],
    hobby:'...',
    photo:'Galio.png'
  }
  // 发送给用户   response:响应
  res.send(data)
})
```

## 制作服务器

- 创建文件夹 `my-server`
- 在`my-server`下执行: `npm init -y` 初始化
- 再执行: `npm i express` 安装express模块
- 再执行: `npm i cors` 安装跨域模块
- 再执行: `npm i express-http-proxy`  代理模块

## 代理

```js
const express = require('express')
// 跨域
const cors = require('cors')
// 代理
const proxy = require('express-http-proxy')

const app = express()

// 启动代理服务器:  nodemon app.js  或 node app.js
app.listen(3000, ()=>{ 
  console.log('服务器启动完毕!');
})

app.use(cors())

// 代理负责转发请求, 必须放在跨域 下方书写
// 所有访问 /dy 接口的请求, 都进行转发
// 即 localhost:3000/dy 
app.use('/xyz', proxy('http://dy.xin88.top'))

//http://localhost:3000/xz/data/product/index.php
app.use('/xz', proxy('http://www.codeboy.com:9999'))

// 范式:
// app.use('接口地址', proxy(要代理到的网站))
```

