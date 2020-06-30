---
id: Interview
title: Interview
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

#### **行内元素,块级元素. 非替换元素/替换元素?**

#### **BFC?**

- BFC 是什么? 

BFC 为格式化上下文,产生一个独立的隔绝容器,容器的元素不会被外面的元素所影响

- 触发条件?

```css
dispaly:inline-block
position: absolute / fixed
```



- 特性以及作用?



#### **如何理解语义化?**

1. 让页面能够结构化的展示  header  主要内容:main  侧边栏:side

2. 易于阅读 方便开发人员快速了解页面结构,更具有可读性,利于开发与维护

   

**ACU？**

**服务端渲染**

**HTML 5  新增了那些标签？**

**浏览器的运行机制**

1. 构建DOM树( parse ): 仅仅是解析了DOM Node
2. 构建渲染树( construct ):  解析CSS   render Tree 中不包含隐藏节点(display: none)和head
3. 布局渲染树(reflow / layout):  从根节点递归调用, 计算逆元素大小和位置 给出每个节点在屏幕上的精确坐标
4. 绘制渲染树 (paint / repaint): 遍历渲染树 使用UI层来绘制 每一个节点 

页面文档完全加载并解析完毕之后会触发 DOMContentLoaded 事件

#### **重排 repaint 和重绘 redraw (回流)?**

**重绘 repaint redraw**

`重绘`是 一个元素**外观的改变**所触发的浏览器行为

触发条件: 改变元素的外观属性: color background-color

注意: Table 及其内部的元素需多次激素三才能确定好在其渲染树节点的属性值,比同等的元素要花费更多时间,所以避免使用Table 布局页面

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

## 两星题目

**img 的 title 和 alt 属性?**

title 是全局属性

**meta标签? 是做什么用的?**

控制页面在移动端不要缩小显示

```html
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
```



##  一星题目

#### **Script 标签的 defer 和 async?**





# **CSS**

## 三星题目

**清除浮动的方法?**

**position 属性 ?他们的用法和区别？?**

绝对定位 相对定位 固定定位 sticky 粘性定位

**CSS 隐藏元素的方式?**

display:none 与 visibility:hidden 的区别 结合重排重绘

```css
1.transform:scale(0,0)  //占空间
2.visibility:hidden  //占空间，无法点击
3.position绝对定位，left:-999999px; right:-99999px; //不占空间，无法点击
4.position绝对定位，z-index:-1000;  //不占空间无法点击
5.display:none  //不占空间，无法点击
```



**Flex 布局?**

- **Flex 容器 和** 项目的 常见属性?
- 举例: 常用考察布局

``` css
display: flex  //设置Flex模式
flex-direction: column  //决定元素是横排还是竖着排
flex-wrap: wrap     //决定元素换行格式
flex-shrink:0   //方式缩放后变瘦，1是默认值，缩放后一起变
flex-grow:1     //占1份，一般写在导航栏，左边logo为0，右边头像为0，中间导航为1

justify-content: space-between  //同一排下对齐方式，空格如何隔开各个元素
align-items: center     //同一排下元素如何对齐
align-content: space-between    //多行对齐方式
```



**双栏布局,三栏布局?**

每种布局都要掌握多种方法

**CSS 盒子模型 哪两种？**

```css
box-sizing：content-box;  width=内容区宽度
box-sizing：border-box;   
width=内容区宽度+padding宽度+margin宽度 (包含内边距和边框)

```

#### **清除浮动**

```css
 .clearfix:after{
     content: '';
     display: block; /*或者 table*/
     clear: both;
 }
 .clearfix{
     zoom: 1; /* IE 兼容*/
 }
```



#### **transition和animation的区别？**

Transition: 与事件相绑定  类似flash 补间动画  设置一个开始关键帧 和 一个结束关键帧

Animation： 是动画属性 可以定义多个关键帧 不需要事件的触发

 



## 二星题目

#### **常用css 选择器？**

#### **CSS  选择器权重 ?**

1. 选择器越具体，优先级越高，比如： #xxx > .yyy 
2. 如果是同样的优先级，后面写的会覆盖前面的 
3. 权重：!important > 行内样式 > #xxx > .yyy > 继承 > 默认

#### **CSS 实现三角形?**

#### **CSS Sprites?**

#### **CSS 动画?**

需要花时间攻克,最好写代码实践一下

- animation  属性
- transition 属性

## 一星问题

**px rem  em 单位的区别？vw vh?**

rem是根据根的font-size变化，而em是根据父级的font-size变化 

rem：相对于根元素html的font-size，假如html为font-size：12px，那么，在其当中的div设置为font-size：2rem,就是当中的div为24px

em：相对于父元素计算，假如某个p元素为font-size:12px,在它内部有个span标签，设置font-size：2em,那么，这时候的span字体大小为：12*2=24px

**CSS import 引入方式 link引入方式的区别？**

**伪类 / 伪元素?**

#### **CSS 新特性?**

```css
transition：过渡
transform：旋转、缩放、移动或者倾斜
animation：动画
gradient：渐变
shadow：阴影
border-radius：圆角
```

#### **sass 的 mixin?**

mixin 类似于对象,对象里面写好CSS 属性,那里用到了就引用这个对象,避免重复写CSS

# **JS**

##　三星问题

**基本数据类型？ 哪些是在堆里 哪些实现栈里？**

- 基本类型

  四基: String number boolean symbol -> 栈

  两空: undefined null  -> 堆

  一对象: Object (包括 数组 函数 日期 对象之父)

- 引用类型  实现在Stack 里

- Symbol 的作用

  symbol

**判断变量的类型 instanceof() 如何实现的??**

- typeof
- instanceof 及 原理
- Object.toString().call() 以及原理 [[class]]

**typeof 可以判断的类型** 

1. 值类型Num String null  undefined Symbol Booleam
2. 函数类型
3. 引用类型  到那时不能细分引用类型

**怎么判断 一个变量是不是数组?**

instanceof 顺着原型链向上寻找

#### **原型和原型链?**

- 给你一个构造函数 描述 构造函数 实例 以及原型之间的关系

构造函数的portotype 属性指向原型

``` js
1.var a = [1,2,3]
2.只有0、1、2、length 4 个key
3.为什么可以 a.push(4) ，push 是哪来的？
4.a.proto === Array.prototype
5.push 就是沿着 a.proto 找到的，也就是 Array.prototype.push，这个寻找的过程可以看做原型链
6.Array.prototype 还有很多方法，如 join、pop、slice、splice
7.Array.prototype 就是 a 的原型（proto）
a.__proto === Array.prototype
```



#### **对于class 的理解? 新增的特性?**以及优缺点?

class 只是一个ES6 的语言规范, 由ECMA 委员会发布,但 ECMA 只规定语法规则, 并不去规定如何实现

就是构造函数的另一种写法 就是 一种语法糖

- extend
- super
- 扩展或重写方法

class 的原型本质

class 中的继承( extends )只是一个形式   还是通过原型实现的 

构造函数中 写 super()

```js
typeof  Student // "function`"
Student.prototype.__proto__ === People.prototype
```



#### **Jquery 简易实现**

```js
class jQuery {
	constructor (selector){
		const result = document.querySelectorAll(selector);
		const length = result.length;
		for (let i = 0; i < length; i++) {
			this.[i] = result[i];
			this.selector = selector;
		}
		this.length = length;
	}
	get(index) {
		return this[index];
	}

	each(fn) {
		for (let i = 0; i< this.length; i++){
			const elem = this[i];
		}
	}

	on(type,fn){
		return this.each(elem => {
			elem.addEventListener(type,fn,false)
		})
	}

}
```



**实现继承的几种方式?**

162页

1. 原型链继承,将父类的实例作为子类的原型   子类的实例同时也是父类的实例,父类新增的原型方法 / 属性, 子类都能够访问.  缺点是原型对象的所有属性被所有实例共享,无法实现多继承, 无法向父类构造函数传参
2. 构造继承 使用父类的构造函数来增强子类实例, 可以实现多继承,但只能继承父类的属性和方法,不能继承原型属性和方法.无法实现函数复用.每一个子类都有函数实例的副本,影响性能
3. 寄生组合继承  通过寄生的方式, 砍掉父类的实例属性,这样,调用两次父类的构造函数的时候,就不会初始化两次实例方法和属性





#### **闭包 及优缺点**

定义: 

> 函数A 里面包含了 函数B，而 函数B 里面使用了 函数A 的变量，那么 函数B 被称为闭包。 又或者：闭包就是能够读取其他函数内部变量的函数

用途: 设计私有变量 (隐藏)  内部函数访问外部作用域变量

优点: 可以防止变量被全局变量污染

缺点: 函数中的所有变量都保存在内存中,内存消耗大,不能滥用闭包

解决方法: 在退出函数之前,将使用的局部变量全部删除 element = null;

```js
闭包的经典题，输出什么？
for(var i = 0; i < 3; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000);
}
//3个3，首先，for 循环是同步代码，先执行三遍 for，i 变成了 3；然后，再执行异步代码 setTimeout，这时候输出的 i，只能是 3 个 3 了

有什么办法输出 0 1 2：
第一种：
把var改成let，每个 let 和代码块结合起来形成块级作用域，当 setTimeout() 打印时，会寻找最近的块级作用域中的 i，所以依次打印出 0 1 2
第二种：使用立即执行函数，创建一个独立的作用域
for(let i = 0; i < 3; i++) {
  (function(i){
    setTimeout(function() {
      console.log(i);
    }, 1000);
  })(i)
}

闭包的具体使用场景：
1.setTimeout 
原生的setTimeout传递的第一个函数不能带参数，通过闭包可以实现传参效果。
function f1(a) {
    function f2() {
        console.log(a);
    }
    return f2;
}
var fun = f1(1);
setTimeout(fun,1000);//一秒之后打印出1


n
function addCurry () {
    var a = 7
     return function(b) {
         console.log(a + b);
     }
}
var add = addCurry();
add(5);
// 12 
// 典型的闭包题,当addCurry的函数返回值 赋值给 add时, a = 7这个值被捕获了
// 后面无论是b传什么数值都是跟7相加 


// 所有的自由变量的查找, 是在函数定义的地方,向上级作用域查找
// 函数作为参数被传递
function print(fn) {
    const a = 200
    fn()
}

const a = 100
function {
	console.log(a);
}
print(fn) //200 


//函数作为返回值
function create(){
    const a =100;
    return function () {
        console.log(a);
    }
}
const fn = create()
const a = 200 
fn(); //100
```

闭包在实际开发中的场景,举例说明?



#### **this 指向? 在不同的场景下如何取值?**

this  取什么值 不是在函数定义的时候确定,而是在函数执行的时候确定的.

```js
fn()
    this => window/global  // 默认绑定
obj.fn()  // 隐式绑定 在对象直接调用函数的时候
    this => obj
fn.call(xx)  //显示绑定
    this => xx
fn.apply(xx)
    this => xx
const fn2 = fn.bind(xx)   但bind 要返回一个新的函数才能执行
fn2() this => xx
new Fn()  
    this => 新的对象  
fn = ()=> {}
    this => 外面的 this
```



#### **call apply bind?**

1. call()和apply()的第一个参数相同，就是指定的对象。这个对象就是该函数的执行上下文。 
2. call()和apply()的区别就在于，两者之间的参数。 
3. call()在第一个参数之后的 后续所有参数就是传入该函数的值。 
4. apply() 只有两个参数，第一个是对象，第二个是数组，这个数组就是该函数的参数。 
5. bind() 方法和前两者不同在于：bind()方法会返回执行上下文被改变的函数而不会立即执行，而前两者是直接执行该函数。其他的参数和call()相同。 
6. 总结：call和apply方法都是在调用之后立即执行的。而bind调用之后是返回原函数，需要再调用一次才行。

**手写 bind 函数**

```js
Function.prototype.myBind = function () {
	// 将参数拆解为数组
	cosnt args = Array.prototype.slice.call(arguments);

	//获取this
	const myThis = args.shift();
	// 获取调用bind 的函数
	const self = this ；

	// 返回一个函数
	return function (){
		return self.apply(t,args)
	}
}
```




**DOM 事件流 和 事件委托?**

DOM事件流 347页

> 事件流是页面接受事件的顺序

- 事件捕获
- 处于目标阶段
- 事件冒泡阶段

mouseover - mouserout   当鼠标移入元素或者其子元素都会触发事件,存在重复触发的过程

mouseenter - mouseleave 当鼠标移入元素本身(不包含子元素)会触发事件, 不会事件冒泡

事件委托 402

- 事件委托以及好处

```js
假设父元素有4个儿子，我不监听4个儿子，而是监听父元素，看触发事件的元素是哪个儿子，这就是事件委托。
好处：可以监听还没有出生的儿子（动态生成的元素）,省监听器。

初级版：
ul.addEventListener('click', function(e){
     if(e.target.tagName.toLowerCase() === 'li'){
         fn() // 执行某个函数
     }
 })
 
bug：如果用户点击的是 li 里面的 span，就没法触发 fn，这显然不对。
 
高级版：
function delegate(element, eventType, selector, fn) {
     element.addEventListener(eventType, e => {
       let el = e.target
       while (!el.matches(selector)) {
         if (element === el) {
           el = null
           break
         }
         el = el.parentNode
       }
       el && fn.call(el, e, el)
     })
     return element
}
```



#### **Cookie / storage / Session ?**

- Cookie的构成
- localStorage 和 sessionStorage

**Cookie:**

1. HTTP  响应通过 Set-Cookie 来设置Cookie

2. 浏览器访问指定域名必须带上Cookie 作为 Request Header

3. Cookie一般来记录信息  因为HTTP 无状态 而服务端的业务需要状态

```
Set-Cookie: "name=value;domain=.domain.com;path=/;expires=Sat, 11 Jun 2016 11:29:42 GMT;HttpOnly;secure"
```

cookie 的 HTTPOnly 加上之后无法通过js来获取cookie, 从而防止xss攻击

**Session:**

1. Session是服务端的内存数据
2. Session 一般通过在Cookie 里记录 SessionID 来实现
3. SessionID 一般是随机数

**LocalStorage 与 Cookie**

1. Cookie请求会发送到服务器上, 而 LocalStorage 不会
2. Cookie 大小一般在4k以下  LocalStorage 一般为5 mb 左右



**localStorage 和 sessionStorage**

都是存储客户端临时信息的对象

sessionStorage 声明周期是一个会话 而 localStorage 存储的数据生命周期是永久的





#### **let const var 的区别?**

1. var声明变量可以重复声明，而let不可以重复声明 

2. var是不受限于块级的，而let是受限于块级 

3. var会与window相映射（会挂一个属性），而let不与window相映射 

4. var可以在声明的上面访问变量，而let有暂存死区，在声明的上面访问变量会报错 

5. const声明之后必须赋值，否则会报错

6. const定义不可变的量，改变了就会报错

7. const和let一样不会与window相映射、支持块级作用域、在声明的上面访问变量会报错

```js
for(let i= 0; i < 3; i++){
    setTimeout(() => {
    console.log(i);
	});
} // 012
var 是全局作用域  存在变量提升 setTimeout 等到代码块执行完毕再执行,所以每次循环的全局变量的i都是一样的数值
let 是块级作用域 每次循环产生一个代码块,每个代码块中的i都是新的

// 题目: 创建10<a>, 依次点击弹出相应的序号
//不要求立刻执行代码的情况 
let a;
for (let i = 0; i < 10l i++){
    a = document.createElement('a');
    a.innerHTML = i +'<br>'
    a.addEventListener('click', function(e) {
        e.preventDefault();
        alert(i);
    })
}

```





#### **ES6 异步编程 Promise 和 async await?**

**单线程和异步**

JS 和 DOM 渲染共用同一个线程,因为js 可以修改DOM 结构

虽然浏览器和Node.js 已经支持JS 启动进程. Web Work 但是JS 一次只能做一件事的单线程的本质没变

异步的原因来自于 JS  是一门单线程的语言, 所以遇到网络请求的时候 不能卡住不动

**同步和异步的区别是什么?**

异步不会阻塞代码执行

同步会阻塞代码执行

Promise

Promise 通过可信任的语义把回调参数作为参数传递, 将回调的任务交给一个 我们与其他工具之间的可信任机制

- 内部状态

- Promise.race 和 Promise.all

  ```js
  1.背代码 Promise 用法
   function axios(){
       return new Promise((resolve, reject)=>{
           成功时调用 resolve(数据)
           失败时调用 reject(错误)
       })
   }
  
  //axios() 为Promise的实例  由then 方法 then里面的第一个参数就是 resolve 函数
   axios().then(success, fail).then(success2, fail2)
  
  2.背代码 Promise.all 用法
   Promise.all([promise1, promise2]).then(success1, fail1)
   promise1和promise2都成功才会调用success1
  
  3.背代码 Promise.race 用法
   Promise.race([promise1, promise2]).then(success1, fail1)
  promise1和promise2只要有一个成功就会调用success1
  
  补充： catch则是用来指定发生错误时的回调函数
  // 优点  通过串行的方式解决回调地狱 callback hell 形成一个链式的结果
// 缺点  无法取消 Promise 错误需要通过回调函数来捕获
  ```

  **async / await**
  
  本质是 Generator 函数 + yield  的语法糖
  
  Generator 是ES6 提供的一种异步编程的解决方案.
  
  ``` js
   function returnPromise(){
      return new Promise( function(resolve, reject){
          setTimeout(()=>{
              resolve('fuck')
          },3000)
      })
   }
  
   returnPromise().then((result)=>{
      result === 'fuck'
   })
  
  ```

 var result = await returnPromise()
   // result === 'fuck'


   例子二
   document.gerElementById("btn").onclik= async ()=>{
      let res = await axios();
      console.log('结果',res);
   }

  // async await 最简单那的使用就是 省略掉.then 直接拿到返回的结果
  //目的是把异步代码写成同步代码(看起来像)
  // 但如果 多个异步操作没有依赖性  使用await 导致性能降低
  ```
  

**前端使用异步的场景有哪些?**

-  网络请求  如 ajax 图片加载
- 定时任务 如setTimeout
- 事件处理
- nodejs 读取文件





#### **Javascript 运行机制**

- 单线程 解释性语言 // 一次只能做一件事
- 事件循环 什么是 eventloop
- 宏任务 / 微任务

**事件循环** eventloop

1. 在代码执行的过程中会执行同步代码,然后宏任务(script setTimeout),进入宏任务队列,微任务(Promise.then() , Promise) 进入微任务队列
2. 当宏任务执行完事之后出队, 检查微任务列表, 继续执行到微任务知道执行完毕
3. 执行浏览器的UI 渲染过程
4. 检查是否有 Web Worker 任务 有则执行
5. 继续下一轮的宏任务和微任务



#### **解构赋值**

​```js
数组解析：
let [a, b, c] = [1, 2, 3]   //a=1, b=2, c=3
let [d, [e], f] = [1, [2], 3]    //嵌套数组解构 d=1, e=2, f=3
let [g, ...h] = [1, 2, 3]   //数组拆分 g=1, h=[2, 3]
let [i,,j] = [1, 2, 3]   //不连续解构 i=1, j=3
let [k,l] = [1, 2, 3]   //不完全解构 k=1, l=2

对象解析：
let {a, b} = {a: 'aaaa', b: 'bbbb'}      //a='aaaa' b='bbbb'
let obj = {d: 'aaaa', e: {f: 'bbbb'}}
let {d, e:{f}} = obj    //嵌套解构 d='aaaa' f='bbbb'
let g;
(g = {g: 'aaaa'})   //以声明变量解构 g='aaaa'
let [h, i, j, k] = 'nice'    //字符串解构 h='n' i='i' j='c' k='e'
  ```



## **二星问题**

#### **数据类型的转换?**

- 相等 == 与 全等 === 的区别
- 强制转换和隐式转换
- 包装类 

字符串拼接

```js
const a = 100 + 10 //110
100 + parseInt('10')  //110

const b = 100 + '10' //10010
const c = true + '10' //true10
```

== 与 ===

```js
100 = '100' //ture
0 == '' //true
0 == false //true
false == '' //true
null == undefined // true
只有判断一个对象是否为null 的时候才用  ==
    
```





#### **浅拷贝，深拷贝？ 如何实现深拷贝？**

``` js
第一种：JSON 来深拷贝
 var a = {...}
 var b = JSON.parse( JSON.stringify(a) )
缺点：JSON 不支持函数、引用、undefined、RegExp、Date……

第二种：递归拷贝
 function clone(object){
     var object2
     if(! (object instanceof Object) ){
         return object
     }else if(object instanceof Array){
         object2 = []
     }else if(object instanceof Function){
         object2 = eval(object.toString())
     }else if(object instanceof Object){
         object2 = {}
     }
     你也可以把 Array Function Object 都当做 Object 来看待
     参考 https://juejin.im/post/587dab348d6d810058d87a0a
     for(let key in object){
         object2[key] = clone(object[key])
     }
     return object2
 }
 思路：先判断是否是对象，如果不是的话判断是否为Array，是否是Function，是否是Object，最后遍历进行复制
 
 区别：
 1.浅拷贝并不复制对象本身而是复制一个指针，新对象和旧对象都是在同一块内存地址
 2.深拷贝则会复制整个对象，新对象与旧对象是两块内存地址。
```



**数组和对象常用的方法,ES6 新增的数组方法?？**

- Array 这些方法会不会改变原始的数值?
- slice splice concar filter map reduce
- Object
- keys/assign(用于浅拷贝)

```js
map: 遍历数组，返回回调返回值组成的新数组
forEach: 无法break，可以用try/catch中throw new Error来停止
filter: 过滤
some: 有一项返回true，则整体为true
every: 有一项返回false，则整体为false
join: 通过指定连接符生成字符串
push / pop: 末尾推入和弹出，改变原数组， 返回推入/弹出项【有误】
unshift / shift: 头部推入和弹出，改变原数组，返回操作项【有误】
sort(fn) / reverse: 排序与反转，改变原数组
concat: 连接数组，不影响原数组， 浅拷贝
slice(start, end): 返回截断后的新数组，不改变原数组
splice(start, number, value...): 返回删除元素组成的数组，value 为插入项，改变原数组
indexOf / lastIndexOf(value, fromIndex): 查找数组项，返回对应的下标
reduce / reduceRight(fn(prev, cur)， defaultPrev):
两两执行，prev 为上次化简函数的return值，cur 为当前值(从第二项开始)
```



#### **requestAnimationFrame?**

相比使用setInterval 实现的动画效果,requestAnimationFrame 的优势是?





**箭头函数?**

- 没有this  箭头函数的外层函数就是  箭头函数的this绑定
- 没有自己的 arguments 对象 
- 不通过new 关键字调用  没有new target 和 原型



#### **Js 取消事件?**

1. onclick <-> btn.onclik = null; 
2. addEventListener( ) <-> remove~

```js
//removeEventListener()的都三个参数必须与addEventListener()一致 
// 该参数为 这个布尔值表示   描述事件是冒泡还是捕获 
// 通过 addEventListener() 方法添加的匿名函数将无法移除

btn.aaddEventListener('click',function(){alert(1);},false);
btn.removeEventListener('click',function(){alert(1);},false);//没有用！

aaddEventListener和removeEventListener看似传入了相同的参数，
但实际上这二个参数是完全不同的函数,想要移出必须这样：

var fn=function(){
	alert(1);
};
btn.aaddEventListener('click',fn,false);
btn.removeEventListener('click',fn,false);//有效
```



## **一星问题**

**new 内部做了什么?**

用 new 操作符  调用构造函数经历以下四个步骤

1. 创建 一个新的对象
2. 将构造函数的作用域 赋值给 新的对象 this指向这个对象
3. 执行构造函数中的代码  为这个新对象添加属性
4. 返回新的对象
5. 将构造函数的 prototype  属性关联到 实例的 __proto__

#### **防抖/节流?**

了解概念 并 手动实现

节流:  类似于fps 游戏中的射速吗,即使鼠标一直射击,但是只在规定速度内射出子弹一段事件内 如果函数多次被调用, 只选择在时间过后执行一次

防抖:  类似于游戏的cd(读条) 函数在一段时间内不触发

```js
 function throttle(fn, delay){
     let canUse = true
     return function(){
         if(canUse){
             fn.apply(this, arguments)
             canUse = false
             setTimeout(()=>canUse = true, delay)
         }
     }
 }

 const throttled = throttle(()=>console.log('hi'))
 throttled()
 throttled()

 function debounce(fn, delay){
     let timerId = null
     return function(){
         const context = this
         if(timerId){window.clearTimeout(timerId)}
         timerId = setTimeout(()=>{
             fn.apply(context, arguments)
             timerId = null
         },delay)
     }
 }
 const debounced = debounce(()=>console.log('hi'))
 debounced()
 debounced()
```



#### **什么是立即执行函数 立即执行函数的目的?**

```js
;(function (){
    var name
 })()
// 目的是造出一个函数作用域，防止污染全局变量
// ES6 新语法
 {
    let  name
 }
```



#### **数组去重?**

``` js

1.计数排序的逻辑（只能正整数）
 var a = [4,2,5,6,3,4,5]
 var hashTab = {}
 for(let i=0; i<a.length;i++){
     if(a[i] in hashTab){
         // 什么也不做
     }else{
         hashTab[ a[i] ] = true
     }
 }
 //hashTab: {4: true, 2: true, 5: true, 6:true, 3: true}
 console.log(Object.keys(hashTab)) // ['4','2','5','6','3']
 
2.Set 去重
 Array.from(new Set(a))
 
3.WeakMap 任意类型去重
```



#### **如何利用正则实现  string.trim()?**

``` js
function trim(string){
    return string.replace(/^\s+|\s+$/g, '')
}
```



**作用域链?**

#### **垃圾回收?**

红宝书  78页

方法一：标记清除（比较常见）

1. 当变量进入执行环境时，就标记这个变量为“进入环境”。 

   //从逻辑上讲，永远不能释放进入环境的变量所占用的内存，因为只要执行流进入相应的环境，就可能会用到他们。

   2. 当变量离开环境时，则将其标记为“离开环境”。 
   3. 垃圾收集器在运行的时候会给存储在内存中的所有变量都加上标记，它会去掉环境中的变量以及被环境中的变量引用的标记。 
   4. 在此之后再被加上标记的变量将被视为准备删除的变量，原因是环境中的变量已经无法访问到这些变量了。 
   5. 最后垃圾收集器完成内存清除工作，销毁那些带标记的值，并回收他们所占用的内存空间。 

方法二：引用计数（不常见） 

1. 跟踪记录每个值被引用的次数。当声明了一个变量并将一个引用类型赋值给该变量时，则这个值的引用次数就是1。
2. 相反，如果包含对这个值引用的变量又取得了另外一个值，则这个值的引用次数就减1。
3. 当这个引用次数变成0时，则说明没有办法再访问这个值了，因而就可以将其所占的内存空间给收回来。
4. 这样，垃圾收集器下次再运行时，它就会释放那些引用次数为0的值所占的内存。



**图片的预加载  和 懒加载?**

1. 预加载：提前加载图片，当用户需要查看时可直接从本地缓存中渲染 
2. 懒加载：用户滑到某个位置的时候才开始加载图片，主要目的是作为服务器前端的优化，减少请求数或延迟请求数 
3. 本质：两者的行为是相反的，一个是提前加载，一个是迟缓甚至不加载。 预加载则会增加服务器前端压力，懒加载对服务器有一定的缓解压力作用。

#### **JS 获取DOM 节点 转字符串?**

``` js
1.用 jquery 比较容易实现：$(".xxx").html()
2.思路
    2.1 我们可以创建一个 div 元素
    2.2 然后将获取的 dom 节点放到 div 里面
    2.3 利用innerHTML就可以获取到dom 节点的字符串

function domToString (node) {  
     let tmpNode = document.createElement('div')
     tmpNode.appendChild(node) 
     let str = tmpNode.innerHTML
     tmpNode = node = null; // 解除引用，以便于垃圾回收  
     return str;  
}  
```

ES6  装饰器

装饰器

# **框架 Vue**

Vue的生命周期? 请求后端数据在哪个声明周期?

Jquery 与 Vue 开发项目的区别?

watch 与 computer 的区别?

为什么我们需要Vuex 作为状态管理?

组合化开发的优点? 设计组件的考虑因素?

Vue Router? 其中两个重要的标签?

router-link 



# **框架 React**

**受控组件 vs  非受控组件?**



**React 有哪些声明周期函数? 分别有什么用? (Ajax 请求放在那个阶段?)**

**React 如何实现组件之间的通信?**



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

# **HTTP 协议**

**HTTP 状态码?**

```bash
特性：
HTTP 是无连接无状态的
HTTP 一般构建于 TCP/IP 协议之上，默认端口号是 80
HTTP 可以分为两个部分，即请求和响应。

区分状态码
1××开头  - 信息提示
2××开头  - 请求成功
3××开头  - 请求被重定向
4××开头  - 请求错误
5××开头  - 服务器错误

常见状态码
200 OK 客户端请求成功。
301 Moved Permanently 请求永久重定向。
302 Moved Temporarily 请求临时重定向。
304 Not Modified 文件未修改，可以直接使用缓存的文件。
400 Bad Request 由于客户端请求有语法错误，不能被服务器所理解。
401 Unauthorized 请求未经授权，无法访问。
403 Forbidden 服务器收到请求，但是拒绝提供服务。服务器通常会在响应正文中给出不提供服务的原因。
404 Not Found 请求的资源不存在，比如输入了错误的URL。
500 Internal Server Error 服务器发生不可预期的错误，导致无法完成客户端的请求。
503 Service Unavailable 服务器当前不能够处理客户端的请求，在一段时间之后，服务器可能会恢复正常。

补充：301 和 302 的区别是什么？
301 永久重定向，浏览器会记住
302 临时重定向
```



**get post 的区别? get的请求参数可不可以放到Body里面呢?**

|      |   数据的传输方式   |    包    | 参数大小 |        |
| :--: | :----------------: | :------: | :------: | :----: |
| GET  | 通过 url 传输数据  |   一个   |   限制   | 读数据 |
| POST | 通过请求消息体Body | 两个以上 |  无限制  | 写数据 |

GET 类似查找的过程,用户获取数据,不需要每次都与数据库建立连接,所以可以使用缓存

POST 操作过程, 进行修改 和 删除,必须与数据库交互,不能使用缓存.

POST 请求两个以上的包 因为有请求体

GET 最大长度是因为 web 服务器限制 URL 的长度



#### **一次 HTTP 请求的过程?**

#### **怎么跨域, JSONP CORS postMessage 是什么?** 



**CORS**

Cross-Origin Resource Sharing 跨源资源共享 使用自定义的HTTP 头部

HTTP 头部中额外添加 Origin

```bash
因为浏览器出于安全考虑，有同源策略。也就是说，如果协议、域名或者端口有一个不同就是跨域，Ajax 请求会失败。
为来防止CSRF攻击
1.JSONP
    JSONP 的原理很简单，就是利用 <script> 标签没有跨域限制的漏洞。
    通过 <script> 标签指向一个需要访问的地址并提供一个回调函数来接收数据当需要通讯时。
    <script src="http://domain/api?param1=a&param2=b&callback=jsonp"></script>
    <script>
        function jsonp(data) {
        	console.log(data)
    	}
    </script>
    JSONP 使用简单且兼容性不错，但是只限于 get 请求,因为Sctipt 标签只能使用get请求
    JSONP 需要配合后端返回指定格式的数据
2.CORS
    CORS 需要浏览器和后端同时支持，需要设置 Access-Control-Allow-Origin:http://foo.example
    IE 8 和 9 需要通过 XDomainRequest 来实现。
3.postMessage
    这种方式通常用于获取嵌入页面中的第三方页面数据。一个页面发送消息，另一个页面判断来源并接收消息
    
补充：
JSONP和AJAX相比的优缺点？
1.JSONP可以跨域 
2.因为JSONP是通过script标签发送的GET请求，所以读不到AJAX那么精确的状态码

```



#### **Ajax 的四个步骤?**

1. 创建 Ajax 实例
2. 执行 open  确定要访问的链接 以及异步同步
3. 监听请求状态
4. 发送请求

```js
 var request = new XMLHttpRequest()
 request.open('GET', '/a/b/c?name=ff', true) // 第三个参数表示异步请求
 request.onload = ()=> console.log(request.responseText)
 request.send()

// 实现一个 ajax 
var xhr = new XMLHttpRequest()
// 必须在调用 open()之前指定 onreadystatechange 事件处理程序才能确保跨浏览器兼容性
xhr.onreadystatechange = function () {
  if (xhr.readyState === 4) {
    if (xhr.status >= 200 && xhr.status < 300 || xhr.status ==== 304) {
      console.log(xhr.responseText)
    } else {
      console.log('Error:' + xhr.status)
    }
  }
}
// 第三个参数表示异步发送请求
xhr.open('get', '/api/getSth',  true)
// 参数为作为请求主体发送的数据
xhr.send(null)


// 将原生的ajax 封装为 promise
const ajax = (url, method, async, data) => {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest()
    xhr.onreadystatechange = () => {
      // 已经接收到全部响应数据，而且已经可以在客户端使用了
      if (xhr.readyState === 4) {
        if (xhr.status === 200) {
          resolve(JSON.parse(xhr.responseText))
        } else if (xhr.status > 400) {
          reject('发生错误')
        }
      }
    }
    xhr.open(url, method, async)
    xhr.send(data || null)
  })
}

```

ajax 的 readyState 状态都代表什么？

- 0：未初始化，但是已经创建了XHR实例
- 1：调用了open()函数
- 2：已经调用了send()函数，但还未收到服务器回应
- 3：正在接受服务器返回的数据
- 4：完成响应

```js
var func = function func(){
    console.log(func === func)
}
func();
// 我自己等于我自己 两个函数的地址相同
```









