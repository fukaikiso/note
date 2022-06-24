# AJAX

**概念**：Asynchronous javascript and xml,异步的javascript和xml

**使用方法**：

      1. 创建xhr对象： ```var xhr = new XMLHttpRequest()```
      2. 打开服务器链接： ```xhr.open(method,url,asyn)```
      3. 响应消息的解决方案： ```xhr.onload = function(){}```
      4. 发送请求： ```xhr.send()```

**应用示例**:

- get

```javascript
let xhr = new XMLHttpRequest()
xhr.open('GET','/v2/user/check_name')
xhr.onload = function(){console.log(xhr.responseText)}
xhr.send()
```

- delete

```txt
与get同理，仅需修改method
```

- post

```javascript
let xhr = new XMLHttpRequest()
xhr.open('POST','/v2/user/check_name')
xhr.setRequestHeader('Content-type','application/x-www-form-urlencoded;charset=UTF-8')
xhr.onload = function(){console.log(xhr.responseText)}
// 若value有中文，需要对其进行编码,传入encodeURI(value)
// xhr.send(`key1=${encodeURI(value2)}&key1=${encodeURI(value2)}`)
xhr.send('key1=value2&key1=value2')
```

- put

```txt
与post同理，仅需修改method
```

**ajax响应消息类型**

1.简单的文本字符串

```txt
HTTP/1.1 200 OK
Content-Type:text/plain;charset=UTF-8

no-exists
```

处理方式：

```txt
msg.innerHTML = xhr.responseText
```

2.HTML片段（比较少用，数据量大，且服务器把前端显示的数据格式定死）

```html
HTTP/1.1 200 OK
Content-Type:text/html;charset=UTF-8

`<td>1</td><td>Macbook</td><td>3500</td>`
```

处理方式：

```txt
tr.innerHTML = xhr.responseText
```

3.XML（可扩展的标记语言）
XML语法上是一种

```xml
HTTP/1.1 200 OK
Content-Type:application/xml;charset=UTF-8

`<list>
    <product lid="1">
      <title>a</title>
      <price>11</price>
    </product>
    <product lid="2">
      <title>b</title>
      <price>12</price>
    </product>
    <product lid="3">
      <title>c</title>
      <price>13</price>
    </product>
</list>`
```

处理方式：用XML解释器程序，把上述数据转为js对象

```json
[{"lid":1,"title":"a","price":11},{...},{...}]
```

4.json（一种用于描述数据的语言）

```json
HTTP/1.1 200 OK
Content-Type:application/json;charset=UTF-8

[
  {"lid" : 1,
  "title" : "a",
  "price" : 11},
  {...},
  {...}
]
```



## 1 创建XMLHttpRequest 对象

- XMLHttpRequest 对象用于和服务器交换数据。

- 创建 XMLHttpRequest 对象的语法：

`variable=new XMLHttpRequest();`

- 老版本的 Internet Explorer （IE5 和 IE6）使用 ActiveX 对象：

`variable=new ActiveXObject("Microsoft.XMLHTTP");`

```js
var xmlhttp;
if (window.XMLHttpRequest)
{
    //  IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
    xmlhttp=new XMLHttpRequest();
}
else
{
    // IE6, IE5 浏览器执行代码
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
}
```



## 2 XHR请求

如需将请求发送到服务器，我们使用 **XMLHttpRequest** 对象的 **open()** 和 **send()** 方法：

```
xmlhttp.open("GET","ajax_info.txt",true);
xmlhttp.send();
```

| 方法                         | 描述                                                         |
| :--------------------------- | :----------------------------------------------------------- |
| open(*method*,*url*,*async*) | 规定请求的类型、URL 以及是否异步处理请求。*method*：请求的类型；GET 或 POST url*：文件在服务器上的位置*  async*：true（异步）或 false（同步） |
| send(*string*)               | 将请求发送到服务器。*string*：仅用于 POST 请求               |

### 2.1 GET 还是 POST

与 POST 相比，GET 更简单也更快，并且在大部分情况下都能用。

然而，在以下情况中，请使用 POST 请求：

- 不愿使用缓存文件（更新服务器上的文件或数据库）
- 向服务器发送大量数据（POST 没有数据量限制）
- 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠

#### 2.1.1 get

```js
xmlhttp.open("GET","/try/ajax/demo_get2.php?fname=Henry&lname=Ford",true);
xmlhttp.send();
```

#### 2.1.2 post

| 方法                             | 描述                                                         |
| :------------------------------- | :----------------------------------------------------------- |
| setRequestHeader(*header,value*) | 向请求添加 HTTP 头。*header*: 规定头的名称*value*: 规定头的值 |

```js
xmlhttp.open("POST","/try/ajax/demo_post2.php",true);
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send("fname=Henry&lname=Ford");
```

### 2.2 异步 - True 或 False

AJAX 指的是异步 JavaScript 和 XML（Asynchronous JavaScript and XML）。

XMLHttpRequest 对象如果要用于 AJAX 的话，其 open() 方法的 async 参数必须设置为 true：

```
xmlhttp.open("GET","ajax_test.html",true);
```

对于 web 开发人员来说，发送异步请求是一个巨大的进步。很多在服务器执行的任务都相当费时。AJAX 出现之前，这可能会引起应用程序挂起或停止。

通过 AJAX，JavaScript 无需等待服务器的响应，而是：

- 在等待服务器响应时执行其他脚本
- 当响应就绪后对响应进行处理

#### 2.2.1 Async=true

当使用 async=true 时，请规定在响应处于 onreadystatechange 事件中的就绪状态时执行的函数：

```js
xmlhttp.onreadystatechange=function()
{
    if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
}
xmlhttp.open("GET","/try/ajax/ajax_info.txt",true);
xmlhttp.send();
```

#### 2.2.2 Async = false

如需使用 async=false，请将 open() 方法中的第三个参数改为 false：

```js
xmlhttp.open("GET","test1.txt",false);
```

不推荐使用 async=false，但是对于一些小型的请求，也是可以的。

请记住，JavaScript 会等到服务器响应就绪才继续执行。如果服务器繁忙或缓慢，应用程序会挂起或停止。

**注意：**当您使用 async=false 时，请不要编写 onreadystatechange 函数 - 把代码放到 send() 语句后面即可

```js
不推荐使用 async=false，但是对于一些小型的请求，也是可以的。

请记住，JavaScript 会等到服务器响应就绪才继续执行。如果服务器繁忙或缓慢，应用程序会挂起或停止。

注意：当您使用 async=false 时，请不要编写 onreadystatechange 函数 - 把代码放到 send() 语句后面即可
```



## 3 XHR响应

如需获得来自服务器的响应，请使用 XMLHttpRequest 对象的esponseText 或 responseXML 属性。

| 属性         | 描述                       |
| :----------- | :------------------------- |
| responseText | 获得字符串形式的响应数据。 |
| responseXML  | 获得 XML 形式的响应数据。  |

responseText 属性返回字符串形式的响应:

```js
document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
```

如果来自服务器的响应是 XML，而且需要作为 XML 对象进行解析，请使用 responseXML 属性：

```js
xmlDoc=xmlhttp.responseXML;
txt="";
x=xmlDoc.getElementsByTagName("ARTIST");
for (i=0;i<x.length;i++)
{
    txt=txt + x[i].childNodes[0].nodeValue + "<br>";
}
document.getElementById("myDiv").innerHTML=txt;
```



## 4 onreadystatechange 事件

当请求被发送到服务器时，我们需要执行一些基于响应的任务。

每当 readyState 改变时，就会触发 onreadystatechange 事件。

readyState 属性存有 XMLHttpRequest 的状态信息。

下面是 XMLHttpRequest 对象的三个重要的属性：

| 属性               | 描述                                                         |
| :----------------- | :----------------------------------------------------------- |
| onreadystatechange | 存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。 |
| readyState         | 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。0: 请求未初始化1: 服务器连接已建立2: 请求已接收3: 请求处理中4: 请求已完成，且响应已就绪 |
| status             | 200: "OK" 404: 未找到页面                                    |

在 onreadystatechange 事件中，我们规定当服务器响应已做好被处理的准备时所执行的任务。

当 readyState 等于 4 且状态为 200 时，表示响应已就绪：

```js
xmlhttp.onreadystatechange=function()
{
    if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
}
```

**注意：** onreadystatechange 事件被触发 4 次（0 - 4）, 分别是： 0-1、1-2、2-3、3-4，对应着 readyState 的每个变化。

**使用回调函数**

回调函数是一种以参数形式传递给另一个函数的函数。

如果您的网站上存在多个 AJAX 任务，那么您应该为创建 XMLHttpRequest 对象编写一个*标准*的函数，并为每个 AJAX 任务调用该函数。

该函数调用应该包含 URL 以及发生 onreadystatechange 事件时执行的任务（每次调用可能不尽相同）：

```js
function myFunction()
{
    loadXMLDoc("/try/ajax/ajax_info.txt",function()
    {
        if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
            document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
        }
    });
}
```

