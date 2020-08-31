---
id: InterviewHtml
title: InterviewHtml
author: Adrian Yang
author_title: Front End Engineer @ Facebook
author_url: https://github.com/Druidss
author_image_url: https://avatars2.githubusercontent.com/u/40681152?s=460&u=e324c1f3465c768888c1fcf798b5f5eb1be9d60d&v=4
tags: [JavaScript, Interview, HTML, CSS]
---

# **HTML**

##  三星题目

#### **水平垂直居中的方式？**

<!--truncate-->

#### **DOCTYPE标签?**

- 标准模式 兼容模式?

**作用:**

**告知浏览器应该用什么文档标准解析当前文档**

DOCTYPE 不存在或者格式不正确会导致文档以兼容模式展现

标准模式:  排版 和 JS运作模式 都是以该浏览器支持的最高标准运行

兼容模式:  页面以宽松的方式向后兼容显示  

区别:

- width 宽度: 兼容模式下为元素的实际宽度(margin + border + padding)  严格模式下 width 为内容宽度 
- 兼容模式下 span 等行内元素可以设置宽高
- margi: 0 auto 居中方式失效 要采用 text-align

HTML5为什么只需要写`<!DOCTYPE HTML>`?

1. 因为HTML5不是SGML的子集，所以不需要DTD引用，但是需要DOCTYPE来规范行为；
2. 而HTML4.01是基于SGML，所以需要DTD引用，来告诉浏览器文档所使用的文档类型

// SGML 标准通用标记语言  (Standard Generalized)

// DTD 类型定义 DocumentTypeDefination





#### **非替换元素/替换元素?**

**可替换元素**
可替换元素就是浏览器根据元素的标签和属性，来决定元素的具体显示内容。

例如浏览器会根据`<img>`标签的src属性的值来读取图片信息并显示出来，而如果查看(x)html代码，则看不到图片的实际内容；

又例如根据`<input>`标签的type属性来决定是显示输入框，还是单选按钮等。

对于可替换元素中的行内元素  一般有内在的宽高比  也可以自定义宽高

**不可替换元素**
(x)html 的大多数元素是不可替换元素，即其内容直接表现给用户端（例如浏览器）。

例如：`<p>段落的内容</p>`
段落`<p>`是一个不可替换元素，文字“段落的内容”全被显示。

对于不可替换中的行内元素: 通过 line-height 属性设置行高



#### **line-height**

行距 = line-height > font-size

![](https://wx1.sbimg.cn/2020/07/17/CxeyA.png)

```css
行高中  有 顶线 中线  基线  底线
certical-align属性中有top、middle、baseline、bottom，就是和这四条线相关。
```



line-height  垂直居中







#### **如何理解语义化?**

1. 让页面能够结构化的展示  header  主要内容:main  侧边栏:side
2. 易于阅读 方便开发人员快速了解页面结构,更具有可读性,利于开发与维护
3. 有利于搜索引擎 SEO
4. 无网络的情况下 不会导
5. 致排版混乱

header  nav  article  footer

27个元素

1. section 用于区域章节的描述
2. nav
3. article
4. video  audio  embed
5. header footer 



**如何区分HTML5 与HTML?**

1. 文件的声明类型不同
2. HTML 没有语义化的结构标签
3. 音视频的支持
4. HTML 5 拥有canvas 画图接口 可以通过js 绘制画像



#### **HTML 5  新增了那些标签 和 API？**

- 语义化标签
- 音视频处理
- 表单属性 color  data email  range
- 存储 localStorage
- canvas dragAPI webSocket
- requestAnimationFrame
- web socket
- 地理位置

**API**

1. History
2. command
3. Media

放弃了 HTML 4 中的 frame frameSet big center



**HTML 与 XHTML 的区别?**

XHTML 使用xml 的语法来 规范的HTMLI

- XHTML 元素必须正确嵌套
- XHTML 元素必须被关闭
- 标签名必须使用小写字母
- 必须拥有根元素



#### **如何处理HTML 5 新签标签的浏览器兼容问题?**







**浏览器的运行机制**

1. 构建DOM树( parse ): 仅仅是解析了DOM Node
2. 构建渲染树( construct CSSDOM):  解析CSS   render Tree 中不包含隐藏节点(display: none)和head
3. 布局渲染树(reflow / layout):  从根节点递归调用, 计算逆元素大小和位置 给出每个节点在屏幕上的精确坐标
4. 绘制渲染树 (paint / repaint): 遍历渲染树 使用UI层来绘制 每一个节点 

页面文档完全加载并解析完毕之后会触发 DOMContentLoaded 事件

#### **重排 repaint 和重绘 redraw (回流)?**

**重绘 repaint redraw**

`重绘`是 一个元素**外观的改变**所触发的浏览器行为

触发条件: 改变元素的外观属性: color background-color

注意: Table 及其内部的元素需多次激素三才能确定好在其渲染树节点的属性值,比同等的元素要花费更多时间,所以避免使用Table 布局页面.



**重排 (重构 回流 reflow):**

当渲染树的一部分 因为元素的规模尺寸,布局,隐藏等改变而需要重新构建,这就成为回流(reflow). 每个页面至少需要一次回流,就是在页面加载的时候.

触发重排的条件:

1. 页面渲染的初始化 无法避免
2. 添加和删除DOM 元素
3. 元素的位置改变 or 使用动画
4. 元素的尺寸改变  -- 大小 外边距 边框 
5. 浏览器窗口尺寸的变化(resize   事件)
6. 填充内容的改变  文本 或 图片大小 
7. 读取某些元素的属性  offsetLeft/Top/Height/Width

**重绘和重排的关系**

在回流的时候,浏览器会使得渲染树中受到影响的部分 失效, 并重新构造这部分渲染树,完成回流后,浏览器会重新绘制受影响的部分到屏幕中.该过程为重绘

 **所以,重排必定引起重绘, 重绘不一定会引发重排**



**优化**

浏览器自己的优化

浏览器会维护一个队列,把 所有引起回流 重绘的操作都放到一个队列中, 等队列中的操作到了一定数量 or 到了一定的时间间隔,那么浏览器就会flush 队列, 进行一个批处理,这样将多次回流 和 重绘 编程一次

自己进行的优化

1.  直接改变元素的 className
2. display:none 然后 进行页面布局等操作, 设置完成后将元素设置为display: block 这样的话 只引起两次重拍 和 重绘
3. 使用 cloneNode 和 replaceChild 引发一个重排和重绘
4. 将多次需要重排的元素 position: 设置为absolute 或者 flex 脱离文档流 不影响其他元素
5. 如果需要创建多个DOM 节点 使用DocumentFragment  创建完成后一次性加入document.

阻碍DOM 解析资源

1. 内联css
2. 内联js
3. 普通外联js
4. 外联defer js 
5. js之前的外联css



#### **前端优化 性能优化**

1. 降低请求量:    合并资源 ,减少HTTP 请求数  gzip压缩  webP
2. 加快请求速度:  预解析DNS  减少域名数 并行加载 CDN
3. 缓存:   HTTP协议缓存请求  离线缓存manifest   离线数据缓存 localStorage
4. 渲染:  CSS/JS 优化  加载顺序 服务端渲染

前端优化

1. 减少重绘和重排
2. 加载优化 异步加载
3. 减少直接操作DOM
4. css 样式 扁平化

## 两星题目

**img 的 title 和 alt 属性?**

title 是全局属性   鼠标滑倒元素上的时候进行展示

alt   用于照片无法加载的时候显示

**meta标签? 是做什么用的?**

控制页面在移动端不要缩小显示

```html
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
```



####  **Src 与 href**

src 

为引入文件 相对路径  用于 img script iframe  || 当浏览器解析到该元素的时候 会暂停其他资源的下载和处理

来自于源 要下载到本地

href 

是链接跳转 url  link  /  a  -> 会进行并行下载,不会停止对当前文档的处理



##  一星题目

#### **Script 标签的 defer 和 async?**

定义了 derfer 的标签按照先后顺序进行请求

1.脚本之间没有依赖关系的，使用sync  并行下载完就执行

2.脚本之间有依赖关系的，使用defer  等HTML 全部渲染完成后 执行



**Noscript 标签的作用：**

用来定义再脚本未被执行的时候的替代内容



#### **iframe 有那些缺点?**

定义: iframe 元素会创建 包含另一个文档的内联框架

1. 阻塞 页面的 onload 事件
2. 不利于SEO
3. 代码复杂 产生HTTP 请求 不利于管理  基本被Ajax 取代

#iframe

#### **正则表达式**

```js
var res = "75team2017".match(/\d+\w*/g)
```

| 正则 | 定义                                    |
| ---- | --------------------------------------- |
| \d   | 匹配一个数字  等价于0-9                 |
| \w   | 匹配 字母 数字  或者下划线 A-Z a-Z 0-9_ |
| +    | 匹配前面一个表达式1次 或 多次           |
| -    | 匹配前面一个表达手机0 次或多次          |
| \g   | 全局匹配                                |

+号 和 * 都是贪婪匹配  \d+ 匹配 75     \w 匹配前面一个表达式 team2017  /g ...



#### **对于 SVG 的理解?**

可缩放矢量模型 用于描述矢量图形的一种图形格式

1. 可任意缩放 不失真
2. 下载速度 大于 jpg png

HTML5 drag API

拖放是一种常见的特性,在 HTML5 中拖放是标准的一部分  draggable = "true"








# **框架 Vue**

Vue的生命周期? 请求后端数据在哪个声明周期?

Jquery 与 Vue 开发项目的区别?

watch 与 computer 的区别?

为什么我们需要Vuex 作为状态管理?

组合化开发的优点? 设计组件的考虑因素?

Vue Router? 其中两个重要的标签?

router-link 



# **框架 React**

#### **React / Vue 框架的基本原理是什么?**

**Vue:** 

(MVVM  双向绑定)   最强调的是 `数据响应`

Vue 是一个以数据响应式为为核心的UI 框架,核心思想是 把所有的数据放到一个对象里面, 然后去操作对象,对象就会改变这个数据, 监听这个改变,再去改变UI

// 不需要DOM Diff 

**React:**  

单向数据流, UI=f(data)  核心是`函数式`  - 引用透明  纯函数 数据不可变



React 是指用有个函数来表示一个一个组件, 我将数据放进去,就将数据渲染到组件里面. 然后我们在放数据的时候做到不可变,如果我更新 不是修改之前的数据,而是新生成一个不一样的数据.函数得到一个新的UI 这个新的UI和旧的UI 做一个DOM Diff, 得到patch 然后将patch 更新到 DOM 树.



**MVC** 

model 

 view 页面层 渲染数据

 controller 接受页面层的数据 调用模型层进行业务逻辑的处理

**MVVM** 

- model   数据模型
- view  页面
- viewmodel 作为桥梁沟通view 和 Model 

在JQery 时期, 如果需要刷新UI 那么要先取得DOM 再更新UI,这样 数据 和 业务逻辑就和 页面存在强耦合

在MVVM 中 UI 通过数据驱动, 数据一旦改变就会相应的刷新UI. UI 如果改变就会改变其中的数据, 这种方式就可以在业务处理中只关系数据的流转,而无需与页面直接打交道. (ViewModel只关心数据和业务的处理, 不关心View 如何处理数据),这样的情况下, view 和 model都可以独立出来, 任何一方改变了也不一定需要改变另一方,并且可以将一些可复用的逻辑放在一个ViewModel 中,让多个View 复用之歌ViewModel

在MVVM 最核心的就是`数据双向绑定`  ? 还是数据相应? (Angluar 脏数据检测 Vue 数据劫持)

**MVVM 与MVC  的区别**

MVVM 通过数据显示视图而不是节点操作

MVVM 解决了MVC 中大量DOM 操作的问题



#### **Hooks 如何在函数内实现dataState ?**

const  [state,setState] = useState();

useState   : 一个结构赋值   state  setState(1) 为什么没有更新:   还会显示呢?   组件重新运行了

useEffect : 模拟类组件的声明周期 



#### **路由原理**

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

**虚拟DOM 是什么?**

**React diff 的原理是什么?**

**Redux 是什么?**

reducer action store 

**connect 的原理是什么?**



# **TypeScript**

#### **TypeScript 比起 JavaScript 有什么优点?**

具有更加严格的类型要求



never 类型是什么?








#  





# 算法 

#### **两数之和**

```js
var nums = [2, 7, 11, 15];
var target = 26;
var twoSum = function (nums, target) {
    var box = new Map();
    for (var i =0; i < nums.length; i++){
        if(box[target - nums[i]] >= 0){
            return [box[target - nums[i]], i]
        }
        box[nums[i]] = i;
    }
}
```

#### **递归**

一个细胞 一个小时分裂一次 生命周期是三个小时 求 n小时后容器内 有多少个细胞？

```js
// 黄色细胞由绿色细胞决定   绿色细胞由白色细胞决定
// 最新的白色细胞 可能由 白色 绿色 黄色来决定.
function total(n){
	var yellow = function(n){
		if(n === 0 || n === 1){return 0};
		return green(n - 1);
	}
	var green = function(n){
		if(n === 0){return 0};
		return white(n - 1);
	}	
	var white = function(n){
		if(n === 0){return 1};
		return white(n - 1) + green(n - 1) + yellow(n - 1);
	}	
	return yellow(n) + green(n) + white(n);
}
```



# 开放性问题

###   如果你新接手一个项目的维护和开发，你会怎么做？

###  开发工作和用户体验是一种什么关系？

### 在你看来，如何养成好的编程习惯？

### **请问你熟悉哪些框架？为什么选择他们？**

### 你怎么看待WEB前端工程师在公司业务中的角色？

