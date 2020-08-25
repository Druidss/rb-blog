---
id: JavascriptProblem
title: JavascriptProblem
author: Adrian Yang
author_title: Front End Engineer @ Facebook
author_url: https://github.com/Druidss
author_image_url: https://avatars2.githubusercontent.com/u/40681152?s=460&u=e324c1f3465c768888c1fcf798b5f5eb1be9d60d&v=4
tags: [JavaScript, Interview, JavascriptProblem]
---

## 07-01

## 1

```js
var F= function();
Object.prototype.a = function()
Function.prototype.b = function();
var f = new F();

//这里的f 可以取到a 但取不到b
```

new 操作符 创建出来的f 只是继承Object  所以继承与 Object.prototype

new 操作符号的 最后一步为 将构造函数的 prototype  属性关联到 实例的 __proto__

这里 F 才是 Function的实例

<!--truncate-->

## 2

装饰器语法

```js
@demo
class MyClass
======
demo = demo(Myclass)
```

## 3

分页

前端分页

- 一次性返回所有的数据, 由前端人员进行数据的切割 整理  划分页数
- 当数据量足够大时, 会产生页面卡顿或者 浏览器"假死"

后端分页

- 返回的是一部分的数据, 需要请求时指明, 每页显示多少条,你要哪一页, 交由服务器去进行数据的切割
- 后台需要明确,
  - 每页显示多少条
  - 客户端需要哪一页, 同时后台会返回数据一共有多少个, 用于交给前端显示,

## 4

```js
let a = {}
b = '0'  
c = 0   
a[b] = "Adrian"   a['0'] = "Adrian"
a[c] = "Druids"   a[0] = "Druids"
console.log(a[b]) // Druids
```

属性名 不能重复， 且 数字属性名 = 字符串属性名

对象 和 数组的区别？ 



```js
let a = {}
b = Symbol('1')
c = Symbol('1')   
a[b] = "Adrian"   a['0'] = "Adrian"
a[c] = "Druids"   a[0] = "Druids"
console.log(a[b]) // Adrian
```

Symbol 的特点是  创建了唯一值



```js
let a = {}
b = { n:'1'}
c = { m:'2'}
a[b] = "Adrian"   a['0'] = "Adrian"
a[c] = "Druids"   a[0] = "Druids"
console.log(a[b]) // Druids
```

引用类型的值都变成字符串来存储，调用toString()  -> [object Object]



## 5

```js
var test = (function (i) {
    return function(){
        alert(i*=2);
    }
})(2);  //立即执行的自适应函数
test(5);
```

'4' alert 弹出的结果为字符串



# 堆栈内存及闭包作用域

- JS 8 中数据类型 及区别
- JS 堆栈内存的运行机制
- 变量提升机制
- 作用域 和 作用域链
- 闭包的两大作用: 保存 / 保护
- JS 的编译机制: VO AO GO
- JS 高级编程技巧   惰性函数 合理化函数 高阶函数



# 面向对象OOP 和 this 处理 

- 单例设计模式
- 类和实例
- 原型和原型链
- new运算符的实现机制
- call apply bind
- constructor 构造函数模式
- JS 中this 的五种情况
- JS 中 四大数据类型检测方案
- JS 中 四大继承方案 +  深拷贝



# DOM BOM 及事件处理机制

- DOM BOM  的核心操作
- 事件对象
- 拖拽 以及 对于拖拽的封装
- 发布订阅设计模式
- 事件传播机制 和 事件代理
- DOM 2级 事件的核心运行机制
- 移动端 Touch / Gesture 事件 及 封装处理
- 浏览器底层渲染机制 和 DOM 重流重绘
- DIALOG 模态框组件的封装



# ES6 /7 核心知识

- let const var 的区别
- 箭头函数 ArrowFunction
- Set / Map 数据结构
- Promise 设计模式
- async / await 及 实现原理
- Generator 生成器函数
- JS 底层运行机制 单线程 和 同步异步编程
- JS 底层运行机制 微任务 宏任务 和 事件循环机制
- interator 迭代器 和 for of 循环



# AJAX HTTP 前后端交互

- AJAX 核心四步操作
- GET POST 核心机制 与 区别
- TCP 三次握手 四次挥手
- axios 库 和 源码解析
- fetch 基础 和 实战应用
- 9 种跨域方案
- HTTP 网络状态码 和 实战中的处理方案
- 前端性能优化汇总 (强缓存 和 弱缓存)