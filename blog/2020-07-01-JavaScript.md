---
id: JavascriptProblem
title: JavascriptProblem
author: Adrian Yang
author_title: Front End Engineer @ Facebook
author_url: https://github.com/Druidss
author_image_url: https://avatars2.githubusercontent.com/u/40681152?s=460&u=e324c1f3465c768888c1fcf798b5f5eb1be9d60d&v=4
tags: [JavaScript, Interview, JavascriptProblem]
---


# 堆栈内存及闭包作用域

- JS 8 中数据类型 及区别
- JS 堆栈内存的运行机制
- 变量提升机制
- 作用域 和 作用域链
- 闭包的两大作用: 保存 / 保护
- JS 的编译机制: VO AO GO
- JS 高级编程技巧   惰性函数 合理化函数 高阶函数

<!--truncate-->



### **基本数据类型？哪些是在堆里 or 栈里？**

- 基本类型

  四基: String number boolean symbol -> 栈

  两空: undefined null  -> 堆

  一对象: Object (包括 数组 函数 日期 对象之父)

- 引用类型  实现在Stack 里

- Symbol 的作用

  symbol为变量提供唯一的标识, 可以解决全局函数变量冲突的问题

### **判断变量的类型 instanceof() 如何实现的??**

- typeof
- instanceof 及 原理 : instanceof 顺着原型链向上寻找
- Object.toString().call() 以及原理 [[class]]

**如何判断一个对象是否属于某个类**

1. InstanceOf： 于判断构造函数的原型对象是否在对象原型链上的某个位置

2. Object.toString().call()  通过返回的 [[Class]] 属性来进行判断

所有用typeof返回为object的变量都含有一个内部属性`[[Class]]`，可以看成是内部的分类，利用Object.prototype.toString.call()可返回该分类。

例如`Object.prototype.toString.call([])`   返回[[Object Array]]



### typeof

#### **typeof 可以判断的类型**? 

1. 值类型Num String null  undefined Symbol Booleam
2. 函数类型
3. 引用类型  到那时不能细分引用类型 不能判断数组

#### typeof NaN 的结果是什么？

typeof NaN会返回number。NaN是一个特殊值，它与自身不相等，NaN !=NaN 为true



### **怎么判断 一个变量是不是数组?**

1.  instanceof 顺着原型链向上寻找

2. ```js
   arr.toString() === '[object Array]'; // true
   Object.prototype.toString.call(arr) === '[object Array]'; // true
   ```

3. ```js
   Array.isArray(arr); // true
   ```



**什么是值？什么是类型？什么是变量？ 它们之间的区别和联系？**

变量中包括 值

类型 指的是 值类型

JavaScript 中 变量的类型可变



### **为什么基础类型在栈上 引用类型在堆上?** 

字符串是存放在栈上么？ 

用new关键字来新建String对象，对象会存放在堆中

对象中有一个 number 属性，那么 number 属性是存放在堆上还是栈上?  

存放指针的属性存放在栈上

栈中内存大小的空间是固定的, 基本类型占用的空间小,大小固定,按值来访问

引用类型占据的空间大,大小不固定储存在栈中影响程序性能



### **== 的判断逻辑**

在比较前 将被比较的值转换成相同的类型

1. 字符串和数值型进行==比较时，将字符串转换为数值型再进行比较。
2. 其他类型跟布尔值进行比较时，先将布尔值转换为数值型，再进行其他比较。
3. NaN和本身取==时为false
4. null == undefined 为true
5. 如果两个操作值都是对象，则需比较两者是否为同一个引用对象。

#### 其他值到数字值的转换规则？

undefined返回NaN。

null返回0.

true返回1，false返回0.

字符串类型的值转换为数值型如同利用Number()，若字符串中含有非数字型返回NaN，空字符串返回0.

#### 其他值到布尔类型的值的转换规则？

转换为false的有六种：

null、undefined、false、""、NaN、+0、-0

#### Object.is() 与原来的比较操作符 “===”、“==” 的区别？

==表示在比较前可以进行类型转换，===表示严格比较，若类型不同会直接返回false

Object.is()与===类似，但处理了一些特殊情况，比如+0和-0不再相对，NaN和自身是相等的。







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

### **原型和原型链?**

> 在JavaScript中我们使用构造函数创建一个实例对象时，每个构造函数内部都有一个prototype属性，这个属性是一个对象，即原型对象。
>
> 实例对象内部的` __proto__ `属性指向构造函数的原型对象.   `a._proto_` === Array.prototype

**原型链能够实现所谓的继承的本质原因是什么？**

因为在访问对象的属性的时候 不仅在该对象上搜寻,还有依照原型链向上搜索

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

#### js 中获取原型的方法

P.constructor.prototype

Object.getPrototypeOf(P)

`P.__proto__`



### **对于class 的理解? 新增的特性?**以及优缺点?

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



### **实现继承的几种方式?**

162页

1. 原型链继承,将父类的实例作为子类的原型   子类的实例同时也是父类的实例,父类新增的原型方法 / 属性, 子类都能够访问.  缺点是原型对象的所有属性被所有实例共享,无法实现多继承, 无法向父类构造函数传参
2. 构造继承 使用父类的构造函数来增强子类实例, 可以实现多继承,但只能继承父类的属性和方法,不能继承原型属性和方法.无法实现函数复用.每一个子类都有函数实例的副本,影响性能
3. 寄生组合继承  通过寄生的方式, 砍掉父类的实例属性,这样,调用两次父类的构造函数的时候,就不会初始化两次实例方法和属性



1. 原型链继承：将子构造函数的原型对象指向父构造函数的实例对象，那么子构造函数的实例对象可继承父类上的属性及方法。缺点是创建子类时不能向父类传参，并且父类原型上的所有引用类型可应用到所有实例对象上。

   ```javascript
   function Father(name, age){
   	this.name = name;
   	this.age = age;
   }
   Father.prototype.getName = function(){
   	return this.name;
   }
   function Child(skill){
   	this.skill = skill;
   }
   Child.prototype = new Father('zhangsan', 20);
   var child = new Child('dance');
   console.log(child.getName());
   ```

2. 构造函数继承：通过在子类中使用对父构造函数使用call方法来调用，并且修改this指针指向子类，同时可以传递参数。优点：避免了引用类型的属性被所有实例共享，也解决了不能传参的问题。缺点是因为方法都在构造函数中定义了，因此每次创建实例时都要创建一遍方法。

   ```javascript
   function Father(name, age){
   	this.name = name;
   	this.age = age;
   	this.getName = function(){
   		return this.name;
   	}
   	this.getAge = function(){
   		return this.age;
   	}
   }
   function Child(name, age, skill){
   	Father.call(this, name, age);
   	this.skill = skill
   }
   var child = new Child('zhangsan', 20, 'dance');
   console.log(child.getName())
   ```

3. 组合继承：通过结合了原型链继承和构造函数继承。

   ```javascript
   function Father(name, age){
   	this.name = name;
   	this.age = age;
   }
   Father.prototype.money = function(){
   	console.log('100000');
   }
   function Child(name, age, skill){
   	Father.call(this, name, age);
   	this.skill = skill;
   }
   Child.prototype = new Father();
   Child.prototype.constructor = Child;
   Child.prototype.exam = function(){
   	console.log('i want to have an exam');
   }
   var child = new Child('zhangsan', 20, 'dance');
   console.log(child.money())
   ```

4. 原型式继承：将以参数形式传入的对象作为创建对象的原型。

   ```javascript
   function creatObj(o){
   	function F(){};
   	F.prototype = o;
   	return new F();
   }
   var person = {
       name: 'zhangsan',
       age: 20
   }
   var person1 = creatObj(person);
   var person2 = creatObj(person);
   person1.name = 'lisi';
   console.log(person1.name, person2.name);
   ```

5. 寄生式继承

   ```js
   function Father(name, age){
   	this.name = name;
   	this.age = age;
   }
   function Child(name, age){
   	Father.call(this, name, age);
   }
   (function(){
   	var Super = function(){};
   	Super.prototype = Father.prototype;
   	Child.prototype = new Super();
   })()
   Child.prototype.constructor = Child;
   var child = new Child('Tom', 20);
   console.log(child.name)
   ```





### **call apply bind?**

1. call()和apply()的第一个参数相同，就是指定的对象。这个对象就是该函数的执行上下文。 
2. call()和apply()的区别就在于，两者之间的参数。 
3. call()在第一个参数之后的 后续所有参数就是`传入该函数的值`。 
4. apply() 只有两个参数，第一个是对象，第二个是`数组`，这个数组就是该函数的参数。 
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

//手写call
Function.prototype.myCall = function(context){
    if(typeof this !== 'function'){
        console.error('type error')
    };
    //获取参数
    let args = [...arguments].slice(1),
        result = null;
    //判断context是否传入 若没传入则设为window
    context = context || window;
    //将调用函数设为对象的方法
    context.fn = this;
    result = context.fn(...args);
    delete context.fn;
    return result;
}
//手写apply
Function.prototype.myApply = function(context){
    if(typeof this !== 'function') {
        console.error('type error');
    }
    let result = null;
    context = context || window;
    context.fn = this;
    if(arguments[1]){
        result = context.fn(...arguments[1]);
    } else {
        result = context.fn()
    }
    delete context.fn;
    return result;
}
//手写bind
Function.prototype.myBind = function(newObject){
    if( typeof this !== 'function'){
        console.error('type error');
    }
    var args = [...arguments].slice(1);
    var that = this;
    return function(){
       return that.apply(newObject, args.concat([...arguments]))
    }
}
```











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



# 三星问题

#### **ES 6 新特性**

1. 变量声明: let
2. 解构赋值
3. 模板字符串
4. 箭头函数



#### **js 有哪些内置对象**

1. Array
2. Date
3. Math
4. String / RegExp 字符串
5. Number Boolean
6. Object





### DOM BOM

#### DOM怎样添加、移除、移动、复制、创建和查找节点

```js
 1 创建元素节点：createElement()
 var p = document.createElement("p");

 2 向父节点的childNodes的末尾添加子节点：
 appendChild(nodeInsert)

3 复制节点 cloneNode(bool)
nodeA.clone(ture);
 参数为布尔值，参数设为true则进行深复制，会复制nodeA节点及其整个子树；参数为false进行浅复制，只复制nodeA节点；
 
4 替换节点 replaceChild(newNode, oldNode)
oldNode.parentNode.replaceChild(newNode, oldNode);

5 移除节点 removeChild(nodeA)
nodeA.parentNode.removeChild(nodeA);

6 查找
  getElementsByTagName()    //通过标签名称

  getElementsByClassName() //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)

  getElementById()    //通过元素Id，唯一性
   
  querySelectorAll('p')  // CSS 选择器

property 直接对变量属性进行修改  不会体现在HTML 结构中
p1.style.width = '100px'

attribute  修改html 属性,会改变html 结构  
p1.setAttritube('data-name', 'adrian')
两者都可能引起DOM 渲染
```

#attribute  #property 





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









#### **闭包 及优缺点**

定义: 

> 闭包是指有权访问另一个函数内变量的函数
>
> 函数A 里面包含了 函数B，而 函数B 里面使用了 函数A 的变量，那么 函数B 被称为闭包。 

用途: 

1. 设计私有变量 (隐藏)  内部函数访问外部作用域变量
2. 另一个作用是将已经运行结束的函数上下文中的变量对象保存在内存中，通过闭包函数保存了对变量对象的引用，因此这个变量对象不会被回收。

优点: 可以防止变量被全局变量污染

缺点: 函数中的所有变量都保存在内存中,内存消耗大,不能滥用闭包

解决方法: 在退出函数之前,将使用的局部变量全部删除 element = null;



#### **作用域的本质是什么？闭包和作用域的关系是什么？**

作用域限制了 `哪个变量在哪里有效`

`通过作用域 实现了函数的闭包`

保证执行函数时变量对象的有序访问，是指向变量对象的有序列表，变量对象包含执行函数内所有的变量和函数，通过作用域链我们可以查找外部函数的变量和函数，当我们执行函数时会首先查找执行上下文中的变量，若没有则沿着作用域链向上查找，直至全局上下文中查找全局变量。

在执行上下文的创建阶段:  创建了作用域链(当前变量对象 + 所有父级的变量对象)

(闭包)回调函数 因为作用域链仍可以访问值  

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

1. 函数外部可以访问函数内部的变量，通过闭包函数，我们可以在函数外部调用闭包函数在外部获取到函数内部的变量。
2. 另一个作用是将已经运行结束的函数上下文中的变量对象保存在内存中，通过闭包函数保存了对变量对象的引用，因此这个变量对象不会被回收。









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







#### **DOM 事件流 和 事件委托?**

DOM事件流 347页

> 事件流是页面接受事件的顺序

#### **三种事件模型是什么？**

1. DOM 0级事件处理程序 该事件模型没有事件流的概念

2. IE事件模型，该事件模型涉及两个事件流，执行阶段和冒泡阶段，首先会监听并触发目标事件，然后会依次冒泡到最外层document，所经过的节点依次判断是否绑定了事件，若有则触发。可以通过attachEvent来监听事件，可以监听多个函数并按顺序执行。
3. DOM2事件模型，该事件模型涉及三个事件流，捕获阶段、执行阶段和冒泡阶段,可以通过addEventListener来监听事件，第三个参数用来判断捕获和冒泡的顺序。

- 事件捕获  (由上到下)
- 处于目标阶段
- 事件冒泡阶段



mouseover - mouserout   当鼠标移入元素或者其子元素都会触发事件,存在重复触发的过程

mouseenter - mouseleave 当鼠标移入元素本身(不包含子元素)会触发事件, 不会事件冒泡\



**事件委托 402**

- 事件委托以及好处

事件委托的本质:

事件委托的本质是通过事件冒泡使父节点能够监听到子节点的事件，从而产生事件函数。也就是将监听函数绑定在子节点的父节点上，这样不必为每个子节点都绑定监听事件，父节点可以通过事件对象定位到子节点目标上。例如当我们动态创建子节点时，动态创建的子节点也可以有监听事件，

可以利用事件委托的形式将监听函数绑定在父节点上，可以减少内存上的消耗。

```js
假设父元素有4个儿子，我不监听4个儿子，而是监听父元素，看触发事件的元素是哪个儿子，这就是事件委托。
好处：可以监听还没有出生的儿子（动态生成的元素）,省监听器。

// addEventListener(event, function, useCapture) 	
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

#addEventLister #事件委托 #DOM



#### **Cookie / storage / Session ?**

- Cookie的构成
- localStorage 和 sessionStorage

**Cookie:**

1. HTTP  响应通过 Set-Cookie 来设置Cookie
2. 浏览器访问指定域名必须带上Cookie 作为 Request Header
3. Cookie一般来记录信息  因为HTTP 无状态 而服务端的业务需要状态
4. 编码方式为encodeURL()

```
Set-Cookie: "name=value;domain=.domain.com;path=/;expires=Sat, 11 Jun 2016 11:29:42 GMT;HttpOnly;secure"
```

cookie 的 HTTPOnly 加上之后无法通过js来获取cookie, 从而防止xss(跨站脚本攻击)

CSRF: 跨站请求伪造   盗取用户身份 以用户的身份发送恶意请求  通过HTTPS 头部的refer 防御

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

#cookie



#### **let const var 的区别?**

1. var声明变量可以重复声明，而let不可以重复声明 
2. var是不受限于块级的，而let是受限于块级 
3. var会与window相映射（会挂一个属性），而let不与window相映射 
4. var可以在声明的上面访问变量，而let有暂存死区，在声明的上面访问变量会报错 
5. const声明之后必须赋值，否则会报错
6. const定义不可变的量，改变了就会报错
7. const和let一样不会与window相映射、支持块级作用域、在声明的上面访问变量会报错

**为什么不建议使用var**

因为var 里面会变量提升, 会输出 undefined 而用let定义变量, 会产生 ReferenceError

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

#let #const



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



**前端使用异步的场景有哪些?**

-  网络请求  如 ajax 图片加载
- 定时任务 如setTimeout
- 事件处理





#### **Javascript 运行机制**

- 单线程 解释性语言 // 一次只能做一件事
- 事件循环 什么是 eventloop
- 宏任务 / 微任务

**事件循环** eventloop

- 同步任务都在主线程上执行，形成一个执行栈
- 主线程之外，还存在一个任务队列。只要异步任务有了运行结果，就在任务队列之中放置一个事件。
- 一旦执行栈中的所有同步任务执行完毕，系统就会读取任务队列,将队列中的事件放到执行栈中依次执行

1. 在代码执行的过程中会执行同步代码, 然后宏任务(script setTimeout),进入宏任务队列,执行过程中如果遇到微任务
   微任务(Promise.then() , Promise) 进入微任务队列 
2. 当宏任务执行完事之后出队, 检查微任务列表, 继续执行到微任务知道执行完毕
5. 继续下一轮的宏任务和微任务



#### **解构赋值**

```js
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

#### 如何将字符串转化为数字，例如 '12.3b'?

1. 使用Number（）方法，但前提是所包含的字符串不包含不合法字符。

2. parseInt（）方法，取整。(将数值转换成整形)

3. parseFloat（）方法，浮点数

4. 隐式类型转换

   

#### ["1", "2", "3"].map(parseInt) 答案是多少？

parseInt方法是将数值转为整数型，接收两个参数，分别为val和radix，即数值和基数，基数范围为2~36之间，并且数值不能大于基数值，这样才能正确返回整数型。map方法传递了三个参数，分别为value，index，array，默认第三个参数被省略。

这样数组传递给parseInt的参数分别为1-0，2-1，3-2，因为数值不能大于基数，所以后两项返回为NaN，第一项由于基数是0，所以默认为10，返回1。因此答案为[1, NaN, NaN]。





#### **浅拷贝，深拷贝？ 如何实现深拷贝？**

``` js
第一种：JSON 来深拷贝
 var a = {...}
 var b = JSON.parse( JSON.stringify(a) )
缺点：JSON 不支持函数、引用、undefined、RegExp、Date……
原理就是先将对象转换为字符串，再通过JSON.parse重新建立一个对象。


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


var array = [
   { number: 1 },
   { number: 2 },
   { number: 3 }
];
function copy (obj) {
        var newobj = obj.constructor === Array ? [] : {};
        if(typeof obj !== 'object'){
            return;
        }
        for(var i in obj){
           newobj[i] = typeof obj[i] === 'object' ?
           copy(obj[i]) : obj[i];
        }
        return newobj
}
var copyArray = copy(array)
copyArray[0].number = 100;
console.log(array); //  [{number: 1}, { number: 2 }, { number: 3 }]
console.log(copyArray); // [{number: 100}, { number: 2 }, { number: 3 }]
 思路：先判断是否是对象，如果不是的话判断是否为Array，是否是Function，是否是Object，最后遍历进行复制
 
 区别：
 1.浅拷贝并不复制对象本身而是复制一个指针，新对象和旧对象都是在同一块内存地址
 2.深拷贝则会复制整个对象，新对象与旧对象是两块内存地址。
```



```JS
    // 获取当前类型
    function getType(attr) {
        let type = Object.prototype.toString.call(attr);
        let newType = type.substr(8, type.length - 9);
        return newType;
    }


    // 声明一个函数
    function cloneDeep (target) {
        // 判断是否传入类型为Object
        if (typeof target !== 'object') {
            return target;
        }
        // 声明新对象
        let newTarget = getType(target) === 'Array' ? [] : {};
        // 循环对象 递归复制给新对象
        for (let key in target) {
            // 判断属性是否在对象本身上
            if (target.hasOwnProperty(key)) {
                // 递归调用
                newTarget[key] = cloneDeep(target[key]);
            }
        }
        // 返回新对象
        return newTarget;
    }

    // 测试代码
    const target = {
        val1: 1,
        val2: undefined,
        val4: 'target',
        val5: {
            name: 'target',
            age: function () {},
            sym: Symbol('setter')
        }
    };
    const targetArray = [1, 2, 3, {name: '123', age: 789}];
    console.log(cloneDeep(target));
    console.log(cloneDeep(targetArray));

```







#### **数组和对象常用的方法,ES6 新增的数组方法?？**

- Array 这些方法会不会改变原始的数值?
- keys/assign(用于浅拷贝) 

1. 数组和字符串的转换方法：toString()、join()
2. 数组尾部操作方法：push()，pop()，push参数可以为多个
3. 数组头部操作方法：shift()，unshift()
4. 数组重排序的方法: reverser()  sort()
5. 数组连接的方法：concat() 返回的是拼接好的数组，不影响原数组
6. 数组截取方法：slice(start, end) 用于截取数组中的一部分进行返回 不影响原数组
7. 数组删除方法：splice(start, number) 用于删除数组中的指定项 返回被删除的数组，影响原数组
8. every() some() forEach() filter() map()
9. reduce() 

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

fill()数组的fill方法可以用一个固定值填充数组从起始索引到终止索引的全部元素。
fill接收三个参数，固定值，起始索引，终止索引。
其中起始索引和终止索引可省略，默认为0和this对象的length值。
```





#### **requestAnimationFrame?**

使用js 实现一个持续的动画效果,requestAnimationFrame是专门为浏览器解决js执行动画的api，

**相比使用setInterval 实现的动画效果,requestAnimationFrame 的优势是?**

- 浏览器优化并行的动画动作, 合并动作在一个渲染周期内完成. 更流畅
- 解决毫秒的不精确性
- 避免过度渲染( 渲染频率太高,..)

我们知道动画效果是通过一帧一帧连续变化而形成的效果，如果我们用定时器来执行动画的话，会因为定时器属于异步函数而可能在规定时间之后执行，因为js是单线程的，所以异步队列要等同步任务执行完毕后再执行回调函数，这样就不能保证动画的流畅性。

类似于定时器的清除方法  `cancelAnimationFrame`

```js
1.window.requestAnimationFrame() 
    说明：该方法会告诉浏览器在下一次重绘重排之前调用你所指定的函数
    1.参数：该方法使用一个回调函数作为参数，这个回调函数会在浏览器下一次重绘之前调用。
            回调函数会被自动传入一个参数，DOMHighResTimeStamp，标识requestAnimationFrame()开始触发回调函数的当前时间

    2.返回值：
            一个 long 整数，请求 ID ，是回调列表中唯一的标识。是个非零值，没别的意义。你可以传这个值给 				        window.cancelAnimationFrame() 以取消回调函数。
            
备注：若你想在浏览器下次重绘之前继续更新下一帧动画，那么回调函数自身必须再次调用window.requestAnimationFrame()
 
2.window.cancelAnimationFrame(requestID)
    取消一个先前通过调用window.requestAnimationFrame()方法添加到计划中的动画帧请求。
    requestID是先前调用window.requestAnimationFrame()方法时返回的值，它是一个时间标识，用法与定时器的id类似。
```





#### **箭头函数?**

- 没有this  箭头函数的外层函数就是  箭头函数的this绑定
- 没有自己的 arguments 对象  在箭头函数中访问`arguments`实际上获得的是外层局部（函数）执行环境中的值。
- 不通过new 关键字调用  没有new target 和 原型 prototype



#### Js 取消事件?

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



#### 什么是“前端路由”？

>  前端路由指的是不同路由对应的不同功能的页面交给前端来做，之前是服务器通过url的不同来返回不同的页面。

**什么时候适合使用“前端路由？**

一般单页面应用时候适合前端路由，大部分页面结构不改变，只改变部分结构。

**“前端路由”有哪些优点和缺点？**

前端路由优点：不必向服务器端请求，缓解了服务器端压力，用户体验好，页面流畅。

前端路由缺点：单页面应用无法记住之前滚动过得位置，也无法在前进后退过程中记住滚动的位置。

前端路由有两种实现方式，一种是hash，另一种是history.pushState。pushState为浏览器添加一条历史记录，添加完后可以使用history.state获取。并且在history模式下，前端的url必须与向后端传递的url保持一致。



## **一星问题**

#### **new 内部做了什么?**

用 new 操作符  调用构造函数经历以下四个步骤

1. 创建 一个新的对象 (在内存上开辟一个空间)
2. 将构造函数的 prototype  属性关联到 实例的` __proto__`
3. 将构造函数的作用域 赋值给 新的对象 this指向这个对象
4. 执行构造函数中的代码  为这个新对象添加属性
5. 返回新的对象 return this



#### **防抖/节流?**

#### 函数防抖

- 概念:  延迟要执行的动作, 若在延迟的这段时间内, 再次触发了 则取消之前开启的动作,重新计时
- 举例:  电脑无操作一分钟后进入休眠, 当40秒时鼠标被移动, 则重新再计时一分钟
- 实现: 定时器
- 应用: 搜索时`等用户完整输入内容后`再发送查询请求

```js
  let inputNode = document.getElementById('user_input')
  let id
  inputNode.addEventListener('keyup',function () {
    let value = inputNode.value
    if(id){
      clearTimeout(id)
    }
    id = setTimeout(()=>{
      sendAjax(value)
    },300)
  })
  
  function sendAjax(data) {
    console.log(`发送了一次Ajax请求，内容为${data}`)
  }
```



#### 函数节流 (throttle)

*  概念：设定一个特定的时间，让函数在特定的时间内只执行一次，不会频繁执行
*  举例：fps游戏，鼠标按住不松手，子弹也不会连成一条线
*  实现：定时器、标识
*  需求：在鼠标滚轮滚动的时候，每隔2秒钟，打印一次

```js
  let canLog = true
  document.body.onscroll = function () {
    if(canLog){
      console.log(1)
      canLog = false
      setTimeout(()=>{
        canLog = true
      },2000)
    }
  }
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

- 两层循环法

- 利用语法自身键的不可重复性

- [原博客]:https://segmentfault.com/a/1190000016418021

``` js
1. 利用 includes
function unique(arr) {
    if (!Array.isArray(arr)) {
        console.log('type error!')
        return
    }
    var array =[];
    for(var i = 0; i < arr.length; i++) {
            if( !array.includes( arr[i]) ) {//includes 检测数组是否有某个值
                    array.push(arr[i]);
              }
    }
    return array
}
 
2.Set 去重
function unique(arr){
	return Array.from(new Set(arr));
}
// 但无法去除掉空对象{}
//set 类似于数组 只不过成员值是唯一的, 没有重复的值

3. splice 去重 
function unique(arr){            
        for(var i=0; i<arr.length; i++){
            for(var j=i+1; j<arr.length; j++){
                if(arr[i]==arr[j]){   
                    arr.splice(j,1);
                    j--;
                }
            }
        }
return arr;
}


4. Map //类似于对象  提供值对值的对应, 一种更完善的Hash 结构实现
创建一个空Map数据结构，遍历需要去重的数组，把数组的每一个元素作为key存到Map中。
由于Map中不会出现相同的key值，所以最终得到的就是去重后的结果
function arrayNonRepeatfy(arr) {
  let map = new Map();
  let array = new Array();  // 数组用于返回结果
  for (let i = 0; i < arr.length; i++) {
    if(map .has(arr[i])) {  // 如果有该key值
      map .set(arr[i], true); //添加键
    } else { 
      map .set(arr[i], false);   // 如果没有该key值
      array .push(arr[i]);
    }
  } 
  return array ;
}


5. hasOwnProperty
利用hasOwnProperty 判断是否存在对象属性
// filter 为数组的每个元素调用callback 函数,返回值为true 的元素创建一个新数组

function unique(arr) {
    var obj = {};
    return arr.filter(function(item, index, arr){
        return obj.hasOwnProperty(typeof item + item) ? false : (obj[typeof item + item] = true)
    })
}


6.  利用 filter
function unique(arr) {
  return arr.filter(function(item, index, arr) {
//indexOf()方法返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。
    //当前元素，在原始数组中的第一个索引==当前索引值，否则返回当前元素
    return arr.indexOf(item, 0) === index;
  });

```



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



#### **图片的预加载  和 懒加载?**

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

#### ES6  装饰器

装饰器是一个作用于函数的表达式

装饰器语法

```js
@demo
class MyClass
======
demo = demo(Myclass)
```



#### **对于JSON 的理解**

　1. JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。

2. Json简单说就是JavaScript中的对象和数组，所以这两种结构就是对象和数组两种结构，通过这两种结构可以表示各种复杂的结构。

在项目开发中我们常用JSON来进行前后端数据的传递，我们在前端将数据转换为JSON字符串的格式传递给后端，后端接收到数据后通过将其转换为特定的数据结构来进行处理。

**js中提供了两种方法来对JSON格式进行处理**

1. 一是`JSON.stringify`将JSON数据结构转变为JSON字符串的模式。

2. 二是`JSON.parse`方法将JSON字符串格式转变为js数据结构，若接收到的数据不是JSON字符串格式就会报错，例如我们在后端接收到JSON字符串格式的数据，可以通过JSON.parse将其转变为js数据结构再进行数据处理。



#### **怎么判断两个对象是否相等**

转成字符串进行判断

```js
JSON.stringify(obj)==JSON.stringify(obj2);
```



#### 为什么使用 setTimeout 实现 setInterval？怎么模拟？

setInterval计时器是每通过一定时间去执行一个函数，但实际上是每经过一定时间将这个事件`添加到任务队列`中，等待执行栈中的事件执行完毕之后才从任务队列中获取事件压入执行栈，

(这时候若是上一个setInterval 函数还没有执行完), 这样就不能保证是每隔一段时间去执行一个事件了。setInterval 只是定时添加到任务队列中,而不是每个程序真正执行完 再执行下一个程序

那么可以通过setTimeout方法来执行,因为setTimeout是真正的运行完一次之后,进行延迟再出发下一个任务，该方法原理是利用递归的方式不断的调用函数来执行setTimeout。

```js
function myInterval(fn, wait){
    var timer = {
        flag: true
    };
    function inside(){
        if(timer.flag){
            fn();
            setTimeout(inside, wait);
        }
    }
    setTimeout(inside, wait); //产生回调函数 使传入的函数再任务队列中执行
    return timer;
}

myInterval(like,1000)

function like(){
    console.log('@@')
}
```





#### setTimeout(fun,0)的使用场景

**! 调整事件的发生顺序**

开发中，某个事件先发生在子元素，然后冒泡到父元素，即子元素的事件回调函数，会早于父元素的事件回调函数触发。如果，想让父元素的事件回调函数先发生，就要用到`setTimeout(f, 0)`。

**监控input 中的文本变化.**  

用户自定义的回调函数，通常在浏览器的默认动作之前触发。比如，用户在输入框输入文本，`keypress`事件会在浏览器接收文本之前触发。所以获取不到当前文本的数值

控制台输入的文本内容是操作前的旧内容。为了获取操作后的新文本内容，可以将对文本的获取和处理放在setTimeout中延时执行



#### .js 延迟加载的方式有哪些？

js代码在解析和执行时会`阻塞页面的渲染`，阻碍dom向下执行，因此我们希望能够延迟js加载，从而使页面性能更好更加流畅。

1. 可以通过在script标签添加`defer`属性，表面页面自上而下执行时若遇到js脚本时不会阻塞页面向下执行，而是加载js脚本和页面解析同时进行，当页面元素全部解析完毕时再按照js脚本的顺序执行js语句。
2. 可以通过在script标签添加`async`属性，它和defer属性的不同是等到js脚本加载完毕就回过头去执行js代码，而不会等到所有页面元素加载完毕，是异步进行的，js脚步不会按照顺序执行，哪个先加载完毕就先执行哪个js代码。
3. 可以利用定时器延迟js脚本的加载。
4. 将js脚本放在html页面的底部。
5. 可以使用动态创建script标签的方式，我们可以对文档的加载事件进行监听，当页面元素全部加载完毕时再动态创建script标签，进行外部js脚本的外链。

#### 说几条写 JavaScript 的基本规范？

在日常书写JavaScript代码时应该遵循一些基本规范利于读者阅读以及日后维护。

例如：

1. 变量声明尽量放在作用域的前面，并且var声明时最好给予初始值。
2. 用‘===’和‘！==’来代替‘==’和‘！=’。
3. 不要给内置对象的原型对象上添加方法，例如Array，Object，Function等。
4. 代码中出现地址、时间等常量用变量来代替。
5. switch语句必须带有default分支。
6. if和for语句要有大括号。

#### 如何编写高性能的 Javascript ？

避免使用过深的嵌套，避免使用未声明的变量，当需要多次访问数组的长度时，可以将长度储存起来。



#### 为什么 0.1 + 0.2 != 0.3？如何解决这个问题？

在计算机中，运算是转换为二进制再进行计算的，js是以64位双精度格式来进行计算的，只有53位有效数字，之后的数字会被截掉，因此产生了误差。

**某些浮点数无法在有限的二进制科学计数法中精确表示。**

科学计数法中表示二进制数: (IEEE 754)

- 符号位  

-  指数位 11位 阶码位(存储指数对应的移码)  

-  有效数(52位) 尾数位(表示浮点数的有效数字 8.00 中的 .00)

> 移码（又叫增码）是符号位取反的[补码](https://baike.baidu.com/item/补码/6854613)，一般用指数的移码减去1来做[浮点数](https://baike.baidu.com/item/浮点数/6162520)的[阶码](https://baike.baidu.com/item/阶码/7798285)，引入的目的是为了保证浮点数的[机器零](https://baike.baidu.com/item/机器零/2211171)为全0。

得[X]移 = x + 2^n-1(n为x的二进制位数，含符号位置，在阶码的表示中，n = 8)

```js
1 - 0.9 === 0.1 *//false* 
1 - 0.1 === 0.9 *//true*
```



![img](https://imgedu.lagou.com/0efa9d2195744587a9f4b7b77d7af38a.jpg)



解决办法 四舍五入到指定小数位

toFixed() 方法来保留小数位 , 在将这个字符串结果转化为数字

parseFloat( (0.1 + 0.2).toFixed(5) )

字符串转换成数字的方法: parseInt(), parseFloat()

#### toPrecision 和 toFixed 和 Math.round 的区别？

toPrecision用于处理精度，从左至右第一个不为0的数开始数起。

toFixed用于处理小数点后精度的个数，从小数点处开始数起，末尾精度四舍五入计算。结果为字符型。

Math.round进行四舍五入取整。



####  一个列表，假设有 100000 个数据，这个该怎么办？

当我们有大量数据时需要考虑几个问题，首先这些数据是否需要同步显示，其次这些数据是否需要按照顺序显示

解决方法：

1. 我们可以使用分页技术，让这些数据分页显示在浏览器上，每次只显示并加载一页数据，其余数据等浏览器操作不同页数时在向服务器端请求渲染。
2. 可以使用懒加载方式，让一部分数据先显示出来，然后当浏览器需要显示某部分数据的时候再去加载那一部分数据，可以减轻服务器端压力，使性能优化。
3. 可以给数据分组显示，比如显示一个定时器，一定时间内显示一部分数据。



#### 分页

前端分页

- 一次性返回所有的数据, 由前端人员进行数据的切割 整理  划分页数
- 当数据量足够大时, 会产生页面卡顿或者 浏览器"假死"

后端分页

- 返回的是一部分的数据, 需要请求时指明, 每页显示多少条,你要哪一页, 交由服务器去进行数据的切割
- 后台需要明确,
  - 每页显示多少条
  - 客户端需要哪一页, 同时后台会返回数据一共有多少个, 用于交给前端显示,



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



```js
var test = (function (i) {
    return function(){
        alert(i*=2);
    }
})(2);  //立即执行的自适应函数
test(5);
```

'4' alert 弹出的结果为字符串

