---
id: interviewCss
title: interviewCss
author: Adrian Yang
author_title: Front End Engineer
author_url: https://github.com/Druidss
author_image_url: https://avatars2.githubusercontent.com/u/40681152?s=460&u=e324c1f3465c768888c1fcf798b5f5eb1be9d60d&v=4
tags: [interviewCss, interview , FrontEnd]
---

# **CSS**

## 三星题目

#### **position 属性 ?他们的用法和区别?**

绝对定位 相对定位 固定定位 sticky粘性定位

**static**

默认元素都是静态定位,此时 left right bottom top 四个定位偏移属性将不会生效

**relative**

相对定位,相对于自身原有位置进行偏移,元素图例常规流, 使用4个偏移属性的时候不影响文档流

**absolute**

绝对定位, 脱离文档流,此时的偏移属性参照里自己最近定位的祖先元素.(要求父元素必须定位 非 static)

其 margin 不与 任何其他的margin 进行折叠.

**fixed**

与 absolute 一致.  但偏移定位以窗口为参考.当出现滚动条时,对象不会随着滚动

**sticky**

对象在常态的时候( viewport中 )遵循常规流, 像是relative 和 fixed 的合体

当元素将要移出便宜范围的时候定位变成 fixed 

<!--truncate-->



#### **隐藏元素的方法和区别**





**CSS 隐藏元素的方式?**

display:none 与 visibility:hidden 的区别 结合重排重绘

display：none 不显示对应的元素，在文档布局中不再分配空间（重排+重绘)

visibility：hidden 隐藏对应元素，在文档布局中仍保留原来的空间（重绘）

```css
1.transform:scale(0,0)  //占空间
2.visibility:hidden  //占空间，无法点击
3.position绝对定位，left:-999999px; right:-99999px; //不占空间，无法点击
4.position绝对定位，z-index:-1000;  //不占空间无法点击
5.display:none  //不占空间，无法点击
```



#### **display 的 属性对比?**

display: block 

Block 块级元素独占一行 可设置宽高

display: inline

行内元素 不会独占一行 相邻的行内元素排列在同一行里,水平方向 产生边距效果, 数值方向不会产生边距效果

display: inline-block

上面二者结合 



**Flex 布局?**

- **Flex 容器 和** 项目的 常见属性?
- 举例: 常用考察布局

``` css
display: flex  //设置Flex模式
flex-direction: column  //决定元素是横排还是竖着排
flex-wrap: wrap     //决定元素换行格式
flex-shrink:0   //方式缩放后变瘦，1是默认值 0 不缩小
flex-grow:1     //占1份，一般写在导航栏，左边logo为0，右边头像为0，中间导航为1

justify-content: space-between  //主轴上对齐
align-items: center     // 交叉轴进行对齐
align-content: space-between    //多行对齐方式
```







#### **垂直居中**

1. 使用padding  只要设置上下内边距  但 父元素不能固定设置高度
2. line-height =  height(父元素的) ||  父元素可以设置高度  但只适合单行文字
3. 弹性布局flex-direction:columm;  justify-content = center;  align-items：center;
4. tale 设置导航栏： 父： display：table； 子元素：display：tale-cell； vertical-align：middle
5. 栅格布局  grid （替代table） 等分排列 +  居中  更适合多行多列的布局
6. 设置伪元素  设置 vertical-align: middle;  使得基线向上偏移

```css
// grid 等分排列并设置 居中
display: grid;
grid-template-columns: repeat(6,1fr);
aligns-items: center;
justify-content: center;

// 搜索框垂直居中 以span 为参考 基线上移  vertical 以 同行的兄弟元素为参考
div.search{
    display: inline-block;
    vertical-align: middle;
}
div.main::after{
    content: "";
    display: inline-block;
    background-color: gold;
    height: 100%;
    width: 0;
    vertical-align: middle;
}

自绝父相
div{
	position: relative;
}
i {
    height: 50px;
    width: 50px;
    position: absolute;
    top:50%;  但此时并没有完全居中
    margin-top：-25px;  再将元素自身的高度向上挪动50%
    
}
```







#### **水平居中?**

**（非浮动）元素居中:**  

块级元素水平居中：  

margin: 0 auto  并设置宽度   // 块级元素

设置块状元素的父元素为 flex justify-content： center；

行内元素：  为父元素设置：  text-align:  center

**浮动元素居中:** 

```css
.son {
    position: relative;
    float:left;
    left: 50%;  // 整体相对于最左边进行偏移
    margin-left: -(宽度的一半)
        or
    transform: translateX(-50%); 移动X轴的位置
}

// flex 布局
.parent {
    display:flex;
    justify-content:center;
}
.chlid{
    float: left;
    width: 200px;//有无宽度不影响居中
}
```



#### **水平垂直居中** 

**flex 布局**

```css

height:600px;  
display:flex;
justify-content:center;  //子元素水平居中
align-items:center;      //子元素垂直居中

```

- dispaly: table-cell

```css
本身该方案是控制文本水居中的
.fahther{
    display: table-cell;
    vertical-align: middle;
    text-align: center;
    //=> 宽高不能是百分比
}
```



- JavaScript 实现  (getBoundingClientRect)







####  **页面常见布局 双栏布局,三栏布局?**

每种布局都要掌握多种方法

#### **双飞翼布局 / 圣杯布局**

1. 三列布局 中间宽度自适应 两边定宽
2. 中间栏在浏览器中优先渲染
3. 允许任意列的高度最高
4. 只使用一个额外的div
5. 最简单css  csst hack

**双飞翼(double-wing) 和 圣杯布局(holy-grail-layout)的区别?**

圣杯布局:  

- 为了中间的 `div `不被遮挡 将中间 div 设置 `padding-left` 和` padding-right`后, 

- 将左右的两个div 设置 `relative`,并分别配合 right  和 left 属性.

[圣杯布局]:https://lhammer.cn/You-need-to-know-css/#/zh-cn/holy-grail-layout?v=1

双飞翼布局: 直接在中间(center )的div 内部创建自div 来防止内容, 并在该自div 中 用 Amargin-left 和 margin-right 为左右两栏留出位置.

[双飞翼布局]:https://lhammer.cn/You-need-to-know-css/#/zh-cn/double-wing-layout?v=1



**多栏布局**

modern solution 是 使用 flex / grid 布局.  适合 mobile-friendly

a 栏栅格系统 

使用浮动来实现多栏布局

b 多列布局

flex 布局

```css
.box {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
}

.box .box-item {
  width: 100px;
  margin-bottom: 10px;
  margin-right: 10px;
}
 justify-content: flex-start; 来实现元素的左对齐
然后在子元素上加 margin-right: 10px; 来保证同一行的元素之间有空隙

.box {
  display: grid;
  grid-template-columns: repeat(4, 100px);
  grid-column-gap: 10px;
  grid-row-gap: 10px;
}
```

**弹性布局 flexbox**

**瀑布流布局**

**响应式布局**



#### **Flex 弹性布局**

- Felx 容器  flex container 采用Flex布局的元素
- Felx 项目 flex item  容器的所有子元素
- 主轴 main axis
- 交叉轴 cross axis

容器属性

- flex-direction： row / column  决定主轴方向
- flex-wrap: wrap / nowrap  是否换行
- flex-flow  前两者的合并形式
- justify-content  主轴上的对齐方式
- align-items    交叉轴上的对齐方式

项目属性

- order
- flex-grow：放大倍数 缺省 0 0 代表不扩展  非零为·`比例扩展`  父容器存在剩余空间时候生效
- flex-shrink：缩小倍数 缺省 1   0 代表不压缩  非零代表 `比例压缩`  父容器超出总空间之后生效
- flex-basis： 占用宽度  缺省auto   auto 默认大小   分配剩余空间之前的预处理
- flex： flex-grow   felx-shrink  flex-basis





#### **Grid 布局**

Grid  容器/网格线/单元/区域/轨道

容器属性:

- Grid-template-rows
- Grid-template-columns： 100px 200px 300px
- Grid-template-ares

区域属性

- Grid-area

**Flex 与 Grid 布局的对比**

Flex 布局是轴线布局，只能指定"项目"轴线的位置, 可以看作是一维布局

Grid布局则是将容器划分为 行 和 列,产生单元格,然后指定项目所在的单元格. 看作二维布局







#### **实现页面通信有哪些方法?** 

- 获取句柄 定向通讯   window.open(url, name)   -> postMessage 完成通信
- 共享内存 结合 轮询 和 事件通知  Loacalstorage  -> storage事件

#### **websocket**

一种HTML5 新协议,基于HTTP/.   浏览器利用HTTP 协议与服务器握手  告知使用websock 进行通信, 创建一个TCP 连接

实现服务器 和 客户端的双向通信. 

应用场景为  多个用户相互交流 或者 实时展示服务器端经常变动的数据(社交应用, 在线教育等)





#### **CSS 盒子模型 哪两种？**

- 标准 W3C 盒子 margin - border - padding - content
- IE 盒子 (怪异盒子模型)  content 包括 border 和 padding  
- flex 弹性伸缩和模型
- colum 多列布局

```css
box-sizing：content-box;  width=内容区宽度
box-sizing：border-box;   优点 可以随意调整 border 和 padding 的大小,写样式更加方便
width=内容区宽度+padding宽度+margin宽度 (包含内边距和边框)
```





#### **浮动原因和带来的问题 清除浮动**

浮动元素脱离文档流.不占据空间. ||  浮动元素知道遇到父级边框 或 另一个浮动元素才停止浮动

问题

1. 父元素的高度无法被撑开，影响与父元素同级的元素
2. 与浮动元素同级的非浮动元素（内联元素）会跟随其后
3. 若一个元素浮动. 那么元素之前的元素也需要浮动

清除浮动:

1. 父级手动设置 height  // 因为高度塌陷 直接设置宽高
2. 添加伪元素 设置 clear:both  + display: bloclk
3. overflow: hidden oder auto // 让父元素具有包裹性

#浮动



#### **BFC?**

- **BFC 是什么?** 

  **block formatting context**

BFC 为格式化上下文,产生一个独立的隔绝容器,容器的元素不会被外面的元素所影响

- 触发条件?

```css
dispaly:inline-block
or
position: absolute / fixed
or
overflow的值不为visible（默认）
or
float的值不为none（默认）
```



- 特性以及作用?

  用于清除浮动, 防止 margin 重叠



#### **CSS 外边距塌陷**

为什么?

为了解决段落之间垂直方向上的空隙

发生在块级元素的垂直方向上

外边距计算

取绝对值最大的margin

绝对定位 / BFC 解决外边距塌陷





 



## 二星题目

#### **CSS 三大特性**

1. 层叠性  解决样式冲突 最后书写为准
2. 继承性    盒子模型属性、文本属性, 定位属性  浮动 不可继承
3. 优先级



#### **常用css 选择器？**

- 基础选择器  *  p   .info   #infoE
- 组合选择器  E,F  多元素  E F 所有后代   E>F 子元素 直接后代  E+F 
- 属性选择器   a[href]
- 伪类 伪元素



#### **CSS  选择器权重 ?**

1. 选择器越具体，优先级越高，比如： #xxx > .yyy 
2. 如果是同样的优先级，后面写的会覆盖前面的 
3. 权重：!important > 行内样式 > #xxx > .yyy / 伪类/ 属性> * > 继承 > 默认





#### **CSS 实现三角形?**

首先，需要把元素的宽度、高度设为0。然后设置边框样式。(利用边框均分原理)

```css
width : 0 ;
height : 0 ;
border -top : 40px solid transparent;
border -left : 40px solid transparent;
border -right : 40px solid transparent;
border -bottom : 40px solid #ff0000;
```



#### **CSS Sprites?**

将一个页面涉及到的所有图片都包含到一张大图中去

然后利用CSS的 background-image，background- repeat，background-position 的组合进行背景定位。利

用CSS Sprites能很好地减少网页的http请求，从而大大的提高页面的性能；CSS Sprites能减少图片的字节





#### **CSS 动画?**

需要花时间攻克,最好写代码实践一下

- animation  属性
- transition 属性

```css
animation: mymove 5s  infinite
@keyframes mymove{
    from{top:0px;}
    to {top:200px;}
}
```

#### **transition和animation的区别？**

Transition: 与事件相绑定  类似flash 补间动画  设置一个开始关键帧 和 一个结束关键帧

Animation： 是动画属性 可以定义多个关键帧 不需要事件的触发



## 一星问题

#### **px rem  em 单位的区别？vw vh?**

px: 固定长度单位 默认字高16px 

rem:  根据根(root)的font-size变化，而em是根据父级的font-size变化   

rem：相对于根元素html的font-size，假如html为font-size：12px，那么，在其当中的div设置为font-size：2rem,就是当中的div为24px

em：相对于父元素计算，假如某个p元素为font-size:12px,在它内部有个span标签，设置font-size：2em,那么，这时候的span字体大小为：12*2=24px

视口单位

vw = view width        vh = view height

**是利用视口单位实现，依赖于视口大小而自动缩放，**失去了最大最小宽度的限制。

**怎么让Chrome支持小于12px 的文字？**

设置缩放

```css
span {
    font-size: 12px;
	display: inline-block;
	-webkit-transform:scale(0.8);
}
//至于为什么要设置display:inline-block； 因为scale属性只对可以定义宽高的元素有效。

Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示
```







#### **CSS import 引入方式 link引入方式的区别？**

link 除了加载css 外  还可以定义其他事务  || 在页面载入的时候可以加载 || XHTML 标签  无兼容性问题 || 支持js修改DOM

@import 只用来加载CSS  ||  页面完全载入后才进行加载

! `<link>`会进行并行下载,不会停止对当前文档的处理



#### **伪类 / 伪元素?**

**::before 和 :after中双冒号和单冒号有什么区别?**

伪类使用:  :hover   :active

CSS1  :beore  // 创建一个伪元素 将成为匹配选中的元素的第一个子元素

CSS3:  ::before  来区分伪元素和伪类   ::first-letter

伪类 基于DOM 类似于太监  可相互拼接

伪元素:  创建一个新的对象  类似创建一个新的对象  不可以相互拼接





#### **CSS3 新特性?**

```css
选择器: E[attr]   E:nth-child
颜色: RGBA HSLA
背景:  图片尺寸...
伸缩盒子: 调整主轴对齐justify-content，调整侧轴对齐align-items，伸缩分配flex
transition：过渡
transform：旋转、缩放、移动或者倾斜
animation：动画   @keyframes 
gradient：渐变    linear-gradient 线性渐变  radial-gradient 径向渐变
text-shadow：阴影
border-radius：圆角
```

新增伪类:

- p:first-of-type 选择属于其父元素的首个元素
- last-of-type 选择属于其父元素的最后元素
- p:only-of-type 选择属于其父元素唯一的元素
- p:only-child 选择属于其父元素的唯一子元素

#### **sass 的 mixin?**

mixin 类似于对象,对象里面写好CSS 属性,那里用到了就引用这个对象,避免重复写CSS\

```css
/* 定义一个类 */
.roundedCorners(@radius: 5px) {
  -moz-border-radius: @radius;
  -webkit-border-radius: @radius;
  border-radius: @radius;
}
#header {
  .roundedCorners;
}
```





#### **什么是响应式设计?响应式设计的基本原理是什么?**

响应式网站设计(Responsive Web design)

一个网站能够兼容多个终端，而不是为每一个终端做一个特定的版本。基本原理是通过媒体查询检测不同的设备屏幕尺寸做处理。页面头部必须有meta声明的viewport

如何兼容低版本的IE？

```html
<meta name="’viewport’" content= "”width=device-width," initial -scale= "1." maximum -scale= "1,user-scalable=no ”"/>
```

#响应式

[viewport 和 移动端布局]:https://github.com/forthealllight/blog/issues/13



#### **全屏滚动的原理是什么?用到了CSS的哪些属性？**

原理：有点类似于轮播，整体的元素一直排列下去，假设有5个需要展示的全屏页面，那么高度是500%，只是展示100%，剩下的可以通过transform进行y轴定位，也可以通过margin-top实现

```css
overflow：hidden；  让视图中只包括一个分页;设置滑动分页的长宽都是 100%; 
transition：all 1000ms ease；
//外部容器设置 transition 过渡效果, 并设置为相对定位, 滚动是修改外部容器的 Top 值, 实现滚动效果
```



#### **什么是优雅降级 和 渐进增强?**

- 优雅降级  在不影响基本效果下 降低视觉体验
- 渐进增强  在不影响基本效果下, 增强视觉体验



#### **为什么要初始化样式?**

因为浏览器兼容问题,不同的浏览器如果不初始化会出现浏览器显示页面的差异.

但 初始化样式对SEO 有一定的影响

```css
body,div,p {
    padding:0;
    margin:0;
}
```