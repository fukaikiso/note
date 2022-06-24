## JSON

**概念**：JavaScript Object Notation,js对象表示法，是一种语言，借鉴了js对象语法的一部分，用于描述数据，把数据转换为字符串格式，在不同系统间交换

**语法规则**

1. json格式的数据本质上是一段字符串
2. 一段json字符串中只能有一个根,这个根要么是对象，要么是数组
3. 一个json对象中，可以包含多个键值对，格式：key:value
4. value可以是"字符串" 数字 true/false 对象 数组 null
5. json中的键名和字符串键值必须用双引号括起来
6. json中两个数据间的分隔符用逗号表示，但是最后一个数据后不能加逗号
7. json中没有注释

**json的序列化与反序列化**

1.序列化：把服务器编程语言中的数据转换为JSON格式的字符串

```javascript
// js对象 --> json字符串
let jsonString = JSON.stringify(obj)
```

2.反序列化： 把浏览器中接收到的JSON格式的字符串转回JS对象

```javascript
// json字符串 --> js对象
let objData = JSON.parse(json.String)
```

