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

运算中  +  号默认转换成字符串  - 号默认转换成数字

## 3

装饰器语法

```js
@demo
class MyClass
======
demo = demo(Myclass)
```

## 4

分页

前端分页

- 一次性返回所有的数据, 由前端人员进行数据的切割 整理  划分页数
- 当数据量足够大时, 会产生页面卡顿或者 浏览器"假死"

后端分页

- 返回的是一部分的数据, 需要请求时指明, 每页显示多少条,你要哪一页, 交由服务器去进行数据的切割
- 后台需要明确,
  - 每页显示多少条
  - 客户端需要哪一页, 同时后台会返回数据一共有多少个, 用于交给前端显示,

