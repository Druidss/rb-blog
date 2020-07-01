---
id: JavascriptProblem
title: Interview
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

## 2

运算中  +  号默认转换成字符串  - 号默认转换成数字