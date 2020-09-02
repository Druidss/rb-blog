---
id: reactProblem
title: reactProblem
author: Adrian Yang
author_title: Front End Engineer
author_url: https://github.com/Druidss
author_image_url: https://avatars2.githubusercontent.com/u/40681152?s=460&u=e324c1f3465c768888c1fcf798b5f5eb1be9d60d&v=4
tags: [react, JavaScript, FrontEnd]
---

# 1 react中父组件调用子组件的方法

引用场景在进行上传这个业务的过程中， 将upload组件 作为上传组件的子组件。这个时候与服务器交互，父组件（上传组件）需要拿到upload组件中的上传的图片在服务器的图片名称。

这个场景下父组件需要直接调用子组件的方法（来获取到服务器response中的图片名称）

<!--truncate-->

父组件

```jsx
class AddUpdate extends Component {
  constructor() {
    super();
    this.picRef = React.createRef();
    this.richText = React.createRef();
  }
    
onFinish = async(values) => {
    let detail = this.richText.current.getRichText()
    console.log(detail)
}
    
   <Form.Item 
      label="商品详情"
      wrapperCol={{md:16}}
   >
      <RichTextEditor ref={this.richText} />
   </Form.Item>
}
```



子组件方法

```jsx
 getRichText = () => {
    const {editorState} = this.state
    return draftToHtml(convertToRaw(editorState.getCurrentContent()))
  }
```

> 1. 子组件需要获取父组件的信息，这通过`props`就可以解决；
> 2. 父组件需要知道子组件的信息，这可以通过`ref`解决。



### **MVVM** 

- model   数据模型
- view  页面
- viewmodel 作为桥梁沟通view 和 Model 

在JQery 时期, 如果需要刷新UI 那么要先取得DOM 再更新UI,这样 数据 和 业务逻辑就和 页面存在强耦合

View是指视图区域，用于页面渲染，展示数据。Model用于存储数据和数据的逻辑交互功能。ViewModel属于连接两者的纽带，

当数据变化时，ViewModel监听到数据变化响应给View更新视图，当页面节点变化时，ViewModel响应给Model进行数据的更新。利用双向数据绑定同步更新View和Model。(ViewModel只关心数据和业务的处理, 不关心View 如何处理数据),

这样的情况下, view 和 model都可以独立出来, 任何一方改变了也不一定需要改变另一方,并且可以将一些可复用的逻辑放在一个ViewModel 中,让多个View 复用这个ViewModel

在MVVM 最核心的就是`数据双向绑定`  ? 还是数据相应? (Angluar 脏数据检测 Vue 数据劫持)

**MVVM 与MVC  的区别**

MVVM 通过数据显示视图而不是节点操作

MVVM 解决了MVC 中大量DOM 操作的问题



### **Hooks 如何在函数内实现dataState ?**

const  [state,setState] = useState();

useState   : 一个结构赋值   state  setState(1) 为什么没有更新:   还会显示呢?   组件重新运行了

useEffect : 模拟类组件的声明周期 



### **路由原理**

本质就是监听URL 的变化,然后匹配路由规则, 然后显示相应的页面, 并且无需刷新

目前单页面路由两种实现方式

- Hash 模式  `www.test.com/##/`  当## 哈希值变化的时候 用过hashchange监听URL变化,不想服务端请求数据, 从而跳转页面
- history 模式  HTML5 推出



**受控组件 vs  非受控组件?**



**React 有哪些声明周期函数? 分别有什么用? (Ajax 请求放在那个阶段?)**





**React 如何实现组件之间的通信?**

通过props 传递

1. 一般数据: -> 父组件向子组件
2. 函数数据: 自组件向父组件传递
3. 只能一层一层传递, 兄弟组件必须借助父组件

使用消息订阅 发布机制

1. pubsub-js实现
2. 组件A 发布消息 相当于触发事件
3. 组件B 订阅消息 接收消息  处理消息 (相当于绑定事件监听)
4. 优点: 对于组件关系没有限制



**shouldComponentUpdate 有什么用?**

### **虚拟DOM 是什么?**

为什么 Virtual DOM 比 原生DOM 快?

当页面发生更新变化时，原生DOM更新的开销比较大，因此使用JS代码进行生成一个虚拟DOM，当数据发生更新时，会生成新的虚拟DOM，然后和之前的虚拟DOM进行对比，利用diff算法比较出两者的差异，然后将两者对应节点的不同结合到原生DOM树上完成更新。

使用虚拟DOM可以节约性能，提升操作效率，节省开销。避免使用原生DOM而带来的变化产生的回流与重绘。提升开发时的可维护性。

### **React diff 的原理是什么?**

利用diff算法来比较两个DOM树的差异。两棵DOM树完全比较的时间度为O（n^3），在前端过程中我们一般不跨层级的移动元素，为了将时间度降为最低，比较两棵树的同一层级的节点。首先会对两棵树进行一个深度遍历，并且对每个节点标上序号。当深度遍历一个DOM树的时候，当遍历到一个节点会对比另一个DOM树的节点，如果有差异就保存到一个对象中。



### **Redux 是什么?**

reducer action store 

**connect 的原理是什么?**

