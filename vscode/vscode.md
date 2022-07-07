# VSCODE

[toc]

## 右键菜单配置

编辑**注册列表**：

1. 新建 计算机\HKEY_CLASSES_ROOT\*\shell\VSCode

- 修改默认值  “open with vscode”

- 新增Icon  "code.exe地址"

2. 新建 计算机\HKEY_CLASSES_ROOT\*\shell\VSCode\Command

- 默认值 "code.exe地址" "%1"(注意有个空格)

3. 新建 计算机\HKEY_CLASSES_ROOT\Directory\shell\vscode和计算机\HKEY_CLASSES_ROOT\Directory\shell\vscode\Command，重复上述步骤

## 设置终端编码utf-8

在**settings.json**中加入
```json
"terminal.integrated.profiles.windows": {
        "Command Prompt": {
            "path": "C:\\Windows\\System32\\cmd.exe",
            "args": ["-NoExit", "/K", "chcp 65001 >nul"]
        },
        "PowerShell": {
            "source": "PowerShell",
            "args": ["-NoExit", "/C", "chcp 65001"]
        }
    },
    "terminal.integrated.defaultProfile.windows": "Command Prompt",
```

## 设置编辑界面

**自动换行**：设置 -- Editor: Word Wrap -- on

**设置垂直标尺**：设置 -- editor.rulers -- settings.json -- "editor.rulers": [80]

## 设置当前目录开启终端

- 安装插件code runner
- 设置openTerminal快捷键为   ctrl+`

## 快捷键

- 文件-首选项-键盘映射中设置

- [快捷键参考](https://blog.csdn.net/qq_41070393/article/details/106299333?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-5-106299333-blog-112059873.pc_relevant_without_ctrlist_v2&spm=1001.2101.3001.4242.4&utm_relevant_index=8)

**基础编辑**

|功能|快捷键|备注|
|:-|:-:|:-:|
|向上/下移动行|alt+上/下|
|向上/下复制行|alt+shift+上/下|
|在下面插入行|ctrl+Enter|
|在上面插入行|ctrl+shift+Enter|
|跳到匹配的括号|ctrl+shift+\|
|缩进|ctrl+]/[|
|展开/折叠语句块|ctrl+shift+]/[|
|行注释|ctrl+/|
|多行注释|shift++alt+a|

**多选和光标**

|功能|快捷键|备注|
|:-|:-:|:-:|
|在上/下插入光标|ctrl+alt+上/下|
|撤销上一个光标操作|ctrl+u|
|选定的每一行末尾加光标|shift+alt+i|
|选择当前行|ctrl+l|
|选择匹配项|ctrl+d|
|选择所有匹配项|ctrl+shift+l|
|展开/缩小选择|shift+alt+右/左|

**终端**

将C:\Program Files\Git\bin添加入环境变量，在终端中输入cmd、bash、powershell可以互相切换

|功能|快捷键|备注|
|:-|:-:|:-:|
|切换到终端视图|alt+t|自定义|
|切换终端组|alt+左键/右键|自定义|
|切换终端组中的终端|alt+上键/下键|
|新建默认终端|ctrl+`|自定义|
|分隔多个终端|ctrl+shift+5|

**聚焦**

|功能|快捷键|备注|
|:-|:-:|:-:|
|聚焦到编辑器|alt+e|自定义|
|切换文件|ctrl+shift+e|
|关闭当前编辑页面|ctrl+w|
|切换编辑器分组|alt+左键/右键|
|切换当前编辑器分组下的文件|ctrl+tab|
|切换选项卡移动焦点|ctrl+m|
|打开侧边栏|ctrl+b|
|打开面板|ctrl+j|
|打开资源管理器|ctrl+shift+e|
|打开搜索|ctrl+shift+f|
|打开源代码管理|ctrl+shift+g|
|打开运行和调试|ctrl+shift+d|
|打开扩展|ctrl+shift+x|
|打开调试控制台|ctrl+shift+y|
|打开输出|ctrl+shift+u|
|打开问题|ctrl+shift+m|
|打开第2/3组编辑器|ctrl+2/3|
|打开quick open|ctrl+p|
|打开命令面板|ctrl+shift+p|

**其他**

| 功能     | 快捷键 | 备注 |
| :------- | :----: | :--: |
| 代码提示 | ctrl+i |      |

## 插件

### （1）智能提示/修改、美化

| 插件名称                                 | 作用                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| Auto Close Tag                           | Automatically add HTML/XML close tag                         |
| Auto Rename Tag                          | Auto rename paired HTML/XML tag                              |
| Bracket Pair Colorizer                   | A customizable extension for colorizing matching brackets    |
| CSS Formatter                            | Formatter for CSS                                            |
| Chinese                                  | Language pack extension for Chinese (Simplified)             |
| Code Spell Checker                       | Spelling checker for source code                             |
| CSS Peek                                 | Allow peeking to css ID and class strings as definitions from html files to respective CSS. Allows peek and goto definition. |
| Error Gutters                            | Show error gutters to the right from line numbers            |
| ESLint                                   | Integrates ESLint JavaScript into VS Code.                   |
| filesize                                 | Show the current file size in the status bar                 |
| HTML CSS Support                         | CSS Intellisense for HTML                                    |
| HTML Snippets                            | Full HTML tags including HTML5 Snippets                      |
| Image preview                            | Shows image preview in the gutter and on hover               |
| Import Cost                              | Display import/require package size in the editor            |
| IntelliCode                              | AI-assisted development                                      |
| IntelliSense for CSS class names in HTML | CSS class name completion for the HTML class attribute based on the definitions found in your workspace. |
| JavaScript (ES6) code snippets           | Code snippets for JavaScript in ES6 syntax                   |
| Markdown All in One                      | All you need to write Markdown                               |
| npm                                      | npm support for VS Code                                      |
| npm Intellisense                         | Visual Studio Code plugin that autocompletes npm modules in import statements |
| Path Intellisense                        | Visual Studio Code plugin that autocompletes filenames       |
| Prettier - Code formatter                | Code formatter using prettier                                |
| Stylelint                                | Official Stylelint extension for Visual Studio Code          |
| CSScomb                                  | 格式化并自动排序css                                          |
| sass                                     | sass关键字高亮、提示                                         |
|                                          |                                                              |



### （2）调试插件

| 插件名称            | 作用                                                         | 快捷键                                      |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------- |
| Debugger for Chrome | Debug your JavaScript code in the Chrome browser.            |                                             |
| Code Runner         | Run C, C++, Java, JS, PHP, Python...                         | 启动：` Ctrl+Alt+N` <br> 停止：`Ctrl+Alt+M` |
| Live Server         | Launch a development local Server with live reload feature for static & dynamic pages |                                             |

### （3）功能插件

| 插件名称                  | 作用                                                         | 快捷键                                                       |
| ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| GitLens                   | Supercharge Git within VS Code                               |                                                              |
| HTML Preview              | Provides ability to preview HTML documents.                  | 外部预览：<br>` ctrl+shift+v`<br/>侧栏预览：`ctrl+k v`       |
| LeetCode                  | Solve LeetCode problems in VS Code                           |                                                              |
| Markdown Preview Enhanced | Markdown Preview Enhanced ported to vscode                   |                                                              |
| open in browser           | This allows you to open the current file in your default browser or application. | 默认浏览器预览：<br/>` alt+v`<br/>其他浏览器预览：<br>`ctrl+alt+v` |
| Polacode-2020             | Polaroid for your code                                       |                                                              |
| Regex Previewer           | Regex matches previewer for JavaScript, TypeScript, PHP and Haxe in Visual Studio Code. |                                                              |
| Minify                    | Minify your js, css and html files to save transmit bandwidth. |                                                              |
| 翻译（英汉词典）          | 划词后在状态栏显示翻译                                       |                                                              |
| Codelf                    | 右键codelf跳转至官网，查询常用变量命名                       |                                                              |
| code translate            | 划词翻译                                                     |                                                              |
| Bracket Jumper            | Bracket-based editor navigation and text selection           | ctrl+alt+上下左右                                            |
| Turbo Console Log         | 选择变量快速插入console.log()                                | ctrl+alt+L<br/>alt+shift+u/c/d                               |
| todo tree                 | 待办事项                                                     |                                                              |



## 配置文件

### **todo tree**

```JS
//TODO: 用来标记待办的地方。常常在有些地方，我们的功能并没有实现，使用ToDo标记我们可以快速定位需要实现的部分。

//HACK: 用来标记可能需要更改的地方。在写代码的时候，有的地方我们并不确定他是正确的，可能未来有所更改，这时候可以使用HACK标记。

//NOTE: 添加一些说明文字。

//INFO: 用来表达一些信息。

//TAG: 用来创建一些标记。

//XXX: 用来标记一些草率实现的地方。在写代码的时候，有些地方需要频繁修改，这时候使用XXX标记。

//BUG: 用来标记BUG~

//FIXME: 用来标记一些需要修复的位置，可以快速定位。

```

```json
//todo-tree settings
  "todo-tree.tree.showScanModeButton": false,
  "todo-tree.filtering.excludeGlobs": ["**/node_modules", "*.xml", "*.XML"],
  "todo-tree.filtering.ignoreGitSubmodules": true,
  "todohighlight.keywords": [
  ],
  "todo-tree.tree.showCountsInTree": true,
  "todohighlight.keywordsPattern": "TODO:|FIXME:|NOTE:|\\(([^)]+)\\)",
  "todohighlight.defaultStyle": {

  },
  "todohighlight.isEnable": false,
  "todo-tree.highlights.customHighlight": {
    "BUG": {
      "icon": "bug",
      "foreground": "#F56C6C",
      "type": "line"
    },
    "FIXME": {
      "icon": "flame",
      "foreground": "#FF9800",
      "type":"line"
    },
    "TODO":{
      "foreground": "#FFEB38",
      "type":"line"
    },
    "NOTE":{
      "icon": "note",
      "foreground": "#67C23A",
      "type":"line"
    },
    "INFO":{
      "icon": "info",
      "foreground": "#909399",
      "type":"line"
    },
    "TAG":{
      "icon": "tag",
      "foreground": "#409EFF",
      "type":"line"
    },
    "HACK":{
      "icon": "versions",
      "foreground": "#E040FB",
      "type":"line"
    },
    "XXX":{
      "icon": "unverified",
      "foreground": "#E91E63",
      "type":"line"
    }
  },
  "todo-tree.general.tags": [
    "BUG",
    "HACK",
    "FIXME",
    "TODO",
    "INFO",
    "NOTE",
    "TAG",
    "XXX"
  ],
  "todo-tree.general.statusBar": "total",


```

### **js自动格式化分号**

```json
//设置里搜索semicolon
```

### **格式化代码不换行**

```js
//prettier设置
Prettier: Jsx Bracket Same Line
Prettier: Print Width
```

### **csscomb配置**

```json
//CSScomb配置文件
//若不同sort-order分组间不想有空行，手动去除中间的[]分组
"csscomb.formatOnSave": true,
    "csscomb.preset": {
        "exclude": [
         ".git/**",
         "node_modules/**",
         "bower_components/**"
        ],
        "always-semicolon": true,
        "block-indent": "   ",
        "color-case": "lower",
        "color-shorthand": true,
        "element-case": "lower",
        "eof-newline": true,
        "leading-zero": false,
        "lines-between-rulesets": 1,
        "quotes": "single",
        "remove-empty-rulesets": true,
        "space-after-colon": " ",
        "space-after-combinator": " ",
        "space-after-opening-brace": "\n",
        "space-after-selector-delimiter": "\n",
        "space-before-closing-brace": "\n",
        "space-before-colon": "",
        "space-before-combinator": " ",
        "space-before-opening-brace": " ",
        "space-before-selector-delimiter": "",
        "space-between-declarations": "\n",
        "strip-spaces": true,
        "unitless-zero": true,
        "vendor-prefix-align": true,
        "sort-order": [
         [
          "font",
          "font-family",
          "font-size",
          "font-weight",
          "font-style",
          "font-variant",
          "font-size-adjust",
          "font-stretch",
          "font-effect",
          "font-emphasize",
          "font-emphasize-position",
          "font-emphasize-style",
          "font-smooth",
          "line-height"
         ],
         [
          "position",
          "z-index",
          "top",
          "right",
          "bottom",
          "left"
         ],
         [
          "display",
          "visibility",
          "float",
          "clear",
          "overflow",
          "overflow-x",
          "overflow-y",
          "-ms-overflow-x",
          "-ms-overflow-y",
          "clip",
          "zoom",
          "-webkit-align-content",
          "-ms-flex-line-pack",
          "align-content",
          "-webkit-box-align",
          "-moz-box-align",
          "-webkit-align-items",
          "align-items",
          "-ms-flex-align",
          "-webkit-align-self",
          "-ms-flex-item-align",
          "-ms-grid-row-align",
          "align-self",
          "-webkit-box-flex",
          "-webkit-flex",
          "-moz-box-flex",
          "-ms-flex",
          "flex",
          "-webkit-flex-flow",
          "-ms-flex-flow",
          "flex-flow",
          "-webkit-flex-basis",
          "-ms-flex-preferred-size",
          "flex-basis",
          "-webkit-box-orient",
          "-webkit-box-direction",
          "-webkit-flex-direction",
          "-moz-box-orient",
          "-moz-box-direction",
          "-ms-flex-direction",
          "flex-direction",
          "-webkit-flex-grow",
          "-ms-flex-positive",
          "flex-grow",
          "-webkit-flex-shrink",
          "-ms-flex-negative",
          "flex-shrink",
          "-webkit-flex-wrap",
          "-ms-flex-wrap",
          "flex-wrap",
          "-webkit-box-pack",
          "-moz-box-pack",
          "-ms-flex-pack",
          "-webkit-justify-content",
          "justify-content",
          "-webkit-box-ordinal-group",
          "-webkit-order",
          "-moz-box-ordinal-group",
          "-ms-flex-order",
          "order"
         ],
         [
          "-webkit-box-sizing",
          "-moz-box-sizing",
          "box-sizing",
          "width",
          "min-width",
          "max-width",
          "height",
          "min-height",
          "max-height",
          "margin",
          "margin-top",
          "margin-right",
          "margin-bottom",
          "margin-left",
          "padding",
          "padding-top",
          "padding-right",
          "padding-bottom",
          "padding-left"
         ],
         [
          "table-layout",
          "empty-cells",
          "caption-side",
          "border-spacing",
          "border-collapse",
          "list-style",
          "list-style-position",
          "list-style-type",
          "list-style-image"
         ],
         [
          "content",
          "quotes",
          "counter-reset",
          "counter-increment",
          "resize",
          "cursor",
          "-webkit-user-select",
          "-moz-user-select",
          "-ms-user-select",
          "user-select",
          "nav-index",
          "nav-up",
          "nav-right",
          "nav-down",
          "nav-left",
          "-webkit-transition",
          "-moz-transition",
          "-ms-transition",
          "-o-transition",
          "transition",
          "-webkit-transition-delay",
          "-moz-transition-delay",
          "-ms-transition-delay",
          "-o-transition-delay",
          "transition-delay",
          "-webkit-transition-timing-function",
          "-moz-transition-timing-function",
          "-ms-transition-timing-function",
          "-o-transition-timing-function",
          "transition-timing-function",
          "-webkit-transition-duration",
          "-moz-transition-duration",
          "-ms-transition-duration",
          "-o-transition-duration",
          "transition-duration",
          "-webkit-transition-property",
          "-moz-transition-property",
          "-ms-transition-property",
          "-o-transition-property",
          "transition-property",
          "-webkit-transform",
          "-moz-transform",
          "-ms-transform",
          "-o-transform",
          "transform",
          "-webkit-transform-origin",
          "-moz-transform-origin",
          "-ms-transform-origin",
          "-o-transform-origin",
          "transform-origin",
          "-webkit-animation",
          "-moz-animation",
          "-ms-animation",
          "-o-animation",
          "animation",
          "-webkit-animation-name",
          "-moz-animation-name",
          "-ms-animation-name",
          "-o-animation-name",
          "animation-name",
          "-webkit-animation-duration",
          "-moz-animation-duration",
          "-ms-animation-duration",
          "-o-animation-duration",
          "animation-duration",
          "-webkit-animation-play-state",
          "-moz-animation-play-state",
          "-ms-animation-play-state",
          "-o-animation-play-state",
          "animation-play-state",
          "-webkit-animation-timing-function",
          "-moz-animation-timing-function",
          "-ms-animation-timing-function",
          "-o-animation-timing-function",
          "animation-timing-function",
          "-webkit-animation-delay",
          "-moz-animation-delay",
          "-ms-animation-delay",
          "-o-animation-delay",
          "animation-delay",
          "-webkit-animation-iteration-count",
          "-moz-animation-iteration-count",
          "-ms-animation-iteration-count",
          "-o-animation-iteration-count",
          "animation-iteration-count",
          "-webkit-animation-direction",
          "-moz-animation-direction",
          "-ms-animation-direction",
          "-o-animation-direction",
          "animation-direction",
          "text-align",
          "-webkit-text-align-last",
          "-moz-text-align-last",
          "-ms-text-align-last",
          "text-align-last",
          "vertical-align",
          "white-space",
          "text-decoration",
          "text-emphasis",
          "text-emphasis-color",
          "text-emphasis-style",
          "text-emphasis-position",
          "text-indent",
          "-ms-text-justify",
          "text-justify",
          "letter-spacing",
          "word-spacing",
          "-ms-writing-mode",
          "text-outline",
          "text-transform",
          "text-wrap",
          "text-overflow",
          "-ms-text-overflow",
          "text-overflow-ellipsis",
          "text-overflow-mode",
          "-ms-word-wrap",
          "word-wrap",
          "word-break",
          "-ms-word-break",
          "-moz-tab-size",
          "-o-tab-size",
          "tab-size",
          "-webkit-hyphens",
          "-moz-hyphens",
          "hyphens",
          "pointer-events"
         ],
         [
          "opacity",
          "filter:progid:DXImageTransform.Microsoft.Alpha(Opacity",
          "-ms-filter:\\'progid:DXImageTransform.Microsoft.Alpha",
          "-ms-interpolation-mode",
          "color",
          "border",
          "border-width",
          "border-style",
          "border-color",
          "border-top",
          "border-top-width",
          "border-top-style",
          "border-top-color",
          "border-right",
          "border-right-width",
          "border-right-style",
          "border-right-color",
          "border-bottom",
          "border-bottom-width",
          "border-bottom-style",
          "border-bottom-color",
          "border-left",
          "border-left-width",
          "border-left-style",
          "border-left-color",
          "-webkit-border-radius",
          "-moz-border-radius",
          "border-radius",
          "-webkit-border-top-left-radius",
          "-moz-border-radius-topleft",
          "border-top-left-radius",
          "-webkit-border-top-right-radius",
          "-moz-border-radius-topright",
          "border-top-right-radius",
          "-webkit-border-bottom-right-radius",
          "-moz-border-radius-bottomright",
          "border-bottom-right-radius",
          "-webkit-border-bottom-left-radius",
          "-moz-border-radius-bottomleft",
          "border-bottom-left-radius",
          "-webkit-border-image",
          "-moz-border-image",
          "-o-border-image",
          "border-image",
          "-webkit-border-image-source",
          "-moz-border-image-source",
          "-o-border-image-source",
          "border-image-source",
          "-webkit-border-image-slice",
          "-moz-border-image-slice",
          "-o-border-image-slice",
          "border-image-slice",
          "-webkit-border-image-width",
          "-moz-border-image-width",
          "-o-border-image-width",
          "border-image-width",
          "-webkit-border-image-outset",
          "-moz-border-image-outset",
          "-o-border-image-outset",
          "border-image-outset",
          "-webkit-border-image-repeat",
          "-moz-border-image-repeat",
          "-o-border-image-repeat",
          "border-image-repeat",
          "outline",
          "outline-width",
          "outline-style",
          "outline-color",
          "outline-offset",
          "background",
          "filter:progid:DXImageTransform.Microsoft.AlphaImageLoader",
          "background-color",
          "background-image",
          "background-repeat",
          "background-attachment",
          "background-position",
          "background-position-x",
          "-ms-background-position-x",
          "background-position-y",
          "-ms-background-position-y",
          "-webkit-background-clip",
          "-moz-background-clip",
          "background-clip",
          "background-origin",
          "-webkit-background-size",
          "-moz-background-size",
          "-o-background-size",
          "background-size",
          "box-decoration-break",
          "-webkit-box-shadow",
          "-moz-box-shadow",
          "box-shadow",
          "filter:progid:DXImageTransform.Microsoft.gradient",
          "-ms-filter:\\'progid:DXImageTransform.Microsoft.gradient",
          "text-shadow"
         ]
        ]
       },


```

