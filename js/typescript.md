# TypeScript

# 1 安装与使用

## 1.1 安装

```shell
npm install -g typescript 
```

## 1.2 配置自动编译

(1) 初始化

```shell
tsc --init 
```

(2)配置文件

打开tsconfig.ison修改outDir 和 rootDir，修改tsc编译生成文件的输出目录和ts文件所在根目录的地址

```shell
{
    "outDir": "./dist",                     
    "rootDir": "./src",                     
}
```

(3)自动编译

```shell
tsc -w
```

## 1.3手动编译

```shell
tsc 文件名.ts
```

### 1.4 typescript特点

- 强类型语言，代码非常严格, 有任何错误 都会`静态报错`
- TS支持为变量声明数据类型
- 编译工具的原理: 把TS中的特殊语法去掉,转为JS
- TS语言不能直接运行, 必须转换成 JS 才能运行, 这就需要编译工具的配合
- TS会检测同时打开的文件中, 是否有同名的变量, 并报错
- TS语言不支持隐式类型转换, 必须手动转换



## 2 数据类型

### 2.1 基本数据类型

```typescript
var a: string
a = 'mike'
a = 22  //报错

var b: number
b = 12
b = 'mike'  //报错

var c: boolean
c = true  
c = 'true'  //报错

var d: null
var e: undefined

// any: 任意.  相当于弱类型
var f: any
f = true
f = 123
f = 'mike'

// 自选的多类型, 通过 |  间隔自定义的多个类型
var g: string | number
g = 'zz'
g = 123
g = true  //报错
```

### 2.2 引用数据类型

#### 2.2.1 数组

```typescript
// 希望数组中都是字符串
var names: Array<string | number> = [...]
// 简化写法
var names: (string | number)[] = [...]
// 规定每个数据的类型
var emp: [string, number, boolean]               emp = [...]                   
```

#### 2.2.2类

```typescript
// 协议/接口 interface
// 为对象类型制定协议: 规定对象有哪些属性 和 类型
interface Employee {
  ename: string
  age: number
  married: boolean
}

// 类似于 自定义了一个类型, emp1 是此类型的
var emp1: Employee = {
  ename: 'mike',
  age: true,
  married: 33,
}

// Java的class语法
// class就是 JS的构造函数
class Student {
  // 对象属性, 必须先声明, 才能进行赋值操作
  sname: string
  age: number

  // 固定的函数名, 称为 构造函数, 在new运算符时触发
  constructor(sname, age) {
    this.sname = sname
    this.age = age
  }
}

var a = { age: 19 }
a.age = 30
// JS的逻辑: 给一个属性赋值, 属性不存在则改为添加操作
// TS的逻辑: 属性名不存在 报错 而不是 帮你新增
a.aeg = 33

// 属性的权限词
class ZZ {
  // 默认不写, 是public, 代表公共区域可以访问
  public name = 'mike'
  // protected: 保护的. 公开区域无法访问
  protected money = '1500元'
  // 私有的: 子无法访问, 只有自身能使用
  private avi = 'video'
}
```



