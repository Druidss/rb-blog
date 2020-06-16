---
id: smallProject
title: chat-ui
author: Adrian Yang
author_title: Front End Engineer @ Facebook
author_url: https://github.com/Druidss
author_image_url: https://avatars2.githubusercontent.com/u/40681152?s=460&u=e324c1f3465c768888c1fcf798b5f5eb1be9d60d&v=4
tags: [JavaScript, chat-ui, docusaurus]
---

##  贪吃蛇

#### 案例目标

游戏的目的是用来体会JavaScript高级语法的使用 不需要具备抽象对象的能力，使用面向对象的方式分析问题，需要一个漫长的过程。

### 功能实现

#### 搭建页面

放一个容器盛放游戏场景 div#map，设置样式

```css
#map {
  width: 800px;
  height: 600px;
  background-color: #ccc;
  position: relative;
}
```

#### 分析对象

- 游戏对象   //控制整个游戏的逻辑 在蛇 和 食物之后写
- 蛇对象  
- 食物对象

#### 创建食物对象

- Food

  - 属性

    - x       
    - y
    - width
    - height
    - color       

  - 方法

    - render       随机创建一个食物对象，并输出到map上

- 创建Food的构造函数，并设置属性

```js
var position = 'absolute';
var elements = [];
function Food(x, y, width, height, color) {
  this.x = x || 0;
  this.y = y || 0;
  // 食物的宽度和高度(像素)
  this.width = width || 20;
  this.height = height || 20;
  // 食物的颜色
  this.color = color || 'green';
}
```

- 通过原型设置render方法，实现随机产生食物对象，并渲染到map上

```js
Food.prototype.render = function (map) {
  // 随机食物的位置，map.宽度/food.宽度，总共有多少分food的宽度，随机一下。然后再乘以food的宽度
  this.x = parseInt(Math.random() * map.offsetWidth / this.width) * this.width;
  this.y = parseInt(Math.random() * map.offsetHeight / this.height) * this.height;

  // 动态创建食物对应的div
  var div = document.createElement('div');
  map.appendChild(div);
  div.style.position = position;
  div.style.left = this.x + 'px';
  div.style.top = this.y + 'px';
  div.style.width = this.width + 'px';
  div.style.height = this.height + 'px';
  div.style.backgroundColor = this.color;
  elements.push(div);
}
```

- 通过自调用函数，进行封装，通过window暴露Food对象

```js
window.Food = Food;
```

#### 创建蛇对象

