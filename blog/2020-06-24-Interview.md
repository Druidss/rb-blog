---
id: Interview
title: Interview
author: Adrian Yang
author_title: Front End Engineer @ Facebook
author_url: https://github.com/Druidss
author_image_url: https://avatars2.githubusercontent.com/u/40681152?s=460&u=e324c1f3465c768888c1fcf798b5f5eb1be9d60d&v=4
tags: [JavaScript, Interview, HTML, CSS]
---





#### **区分度问题**

"谈谈你的理解"

要讲自己的思维脉络  (keyword)

大体量的问题

"一个网页加载速度优化" 

面向切面提问?

不同框架 对于 一个问题的解决的方法



# **HTML**

##  三星题目

**水平垂直居中的方式？**



**DOCTYPE标签?**

- 标准模式 兼容模式?

**行内元素,块级元素. 非替换元素/替换元素?**

**BFC?**

- BFC 是什么?
- 触发条件?
- 特性以及作用?

<!--truncate-->

如何理解语义化?

ACU？

服务端渲染

HTML 5  新增了那些标签？

Metadata 作用？ 属性



## 两星题目

**img 的 title 和 alt 属性?**

title 是全局属性

**meta标签?**



##  一星题目

Script 标签的 defer 和 async?





# **CSS**

## 三星题目

**清除浮动的方法?**

**position 属性 ?他们的用法和区别？?**

绝对定位 相对定位 固定定位 sticky 粘性定位

**CSS 隐藏元素的方式?**

display:none 与 visibility:hidden 的区别 结合重排重绘

**Flex 布局?**

- **Flex 容器 和** 项目的 常见属性?
- 举例: 常用考察布局

**双栏布局,三栏布局?**

每种布局都要掌握多种方法

**CSS 盒子模型 哪两种？**

- boxsizing

**重排和重绘?**

## 二星题目

**常用css 选择器？**

**CSS  选择器权重 ?**

**CSS 实现三角形?**

**CSS Sprites?**

**CSS 动画?**

需要花时间攻克,最好写代码实践一下

- animation  属性
- transition 属性

## 一星问题

**px rem  em 单位的区别？vw vh?**

**CSS import 引入方式 link引入方式的区别？**

**伪类/ 伪元素?**

# **JS**

##　三星问题

**基本数据类型？ 哪些是在堆里 哪些实现栈里？**

- 基本类型
- 引用类型
- Symbol 的作用

**判断变量的类型 instanceof() 如何实现的??**

- typeof
- instanceof 及 原理
- Object.toString().call() 以及原理 [[class]]

**原型和原型链?**

- 给你一个构造函数 描述 构造函数 实例 以及原型之间的关系

构造函数的portotype 属性指向原型

**闭包以及优缺点?**



**call apply bind?**

**DOM 事件流 和 事件委托?**

DOM事件流 347页

- 捕获 冒泡

事件委托 402

- 事件委托以及好处

**Cookie / storage ?**

- Cookie的构成
- localStorage 和 sessionStorage

举例: cookie 的 HTTPOnly 加上之后无法通过js来获取cookie, 从而防止xss攻击

**let const var 的区别?**

**ES6 异步编程 Promise 和 async await?**

- 内部状态
- Promise.race 和 Promise.all

Javascript 运行机制

- 单线程 解释性语言
- 事件循环 什么是 eventloop
- 宏任务 / 微任务

## **二星问题**

**数据类型的转换?**

- 相等 == 与 全等 === 的区别
- 强制转换和隐式转换
- 包装类型

**浅拷贝，深拷贝？ 如何实现深拷贝？**

**数组和对象常用的方法,ES6 新增的数组方法?？**

- Array 这些方法会不会改变原始的数值?
- slice splice concar filter map reduce

- Object
- keys/assign(用于浅拷贝)

**requestAnimationFrame?**

相比使用setInterval 实现的动画效果,requestAnimationFrame 的优势是

**this 指向?**

**箭头函数?**

**实现继承的几种方式?**

162页



## **一星问题**

**new 内部做了什么?**

**防抖/节流?**

了解概念 并 手动实现

**作用域链?**

**垃圾回收?**

78页

**对于class 的理解? 新增的特性?**



# **框架 Vue**

Vue的生命周期? 请求后端数据在哪个声明周期?

Jquery 与 Vue 开发项目的区别?

watch 与 computer 的区别?

为什么我们需要Vuex 作为状态管理?

组合化开发的优点? 设计组件的考虑因素?

# **HTTP 协议**

get post 的区别? get的请求参数可不可以放到Body里面呢?

一次 HTTP 请求的过程?





```js
function addCurry () {
	var a =7;
     return function(b) {
         console.log(a + b);
     }
}
var add = addCurry();
add(5);
```

