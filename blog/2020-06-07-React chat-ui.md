id: chat-ui
title: chat-ui
author: Adrian Yang
author_title: Front End Engineer @ Facebook
author_url: https://github.com/Druidss
author_image_url: https://avatars2.githubusercontent.com/u/40681152?s=460&u=e324c1f3465c768888c1fcf798b5f5eb1be9d60d&v=4
tags: [React, chat-ui, docusaurus]

## React chat-ui

**#### 组件**

<APP /> 应用的入口组件

如何定义一个组件?

1. 创建 一个js文件
2. import React from "React"  引入React 依赖
3. 定义函数 (名字大写)
4. 导出组件 export default Button;

在 APP 组件中导入





#### **属性 props**

组件接收props

```js
function Button(props) {
return <button>{props.label}</button>;
}

// 解构label 省去通过点来获取属性值
function Button(label) {
return <button>{label}</button>;
}
//APP.js
function App() {
  return (
    <div> 
    <Button label="按钮" /> 
    <Button label="点我" /> 
    </div> 
  );
}
```

children 属性 

props 内置属性 在组件中 开始和结束标签里的任何内容



#### **事件监听**

事件监听函数

直接写在组件函数体内 // 但所有该组都有该函数

写在组件的父级组件中,在通过属性props 将函数传递进去



#### **状态 state**

props 是静态的 数据不会刷新,如果想要动态更改组减的数值,使用状态State

```
// 解构赋值  接收状态的默认值 返回一个数组 第一个元素是状态的值 第二个是改变状态值的函数


//style 接受一个对象形式
```

Hooks

用来定义可复用的逻辑

推荐Hooks 都以use开头