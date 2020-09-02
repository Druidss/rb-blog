---
id: algorithm
title: algorithm
author: Adrian Yang
author_title: Front End Engineer
author_url: https://github.com/Druidss
author_image_url: https://avatars2.githubusercontent.com/u/40681152?s=460&u=e324c1f3465c768888c1fcf798b5f5eb1be9d60d&v=4
tags: [JavaScript, algorithm FrontEnd]
---



# 算法 

### **两数之和**

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

<!--truncate-->



## **递归**

#### 1-10的和

```js
function sum(n){
	if(n > 10)  return 0
	return n+sum(n+1);
}

let  total = sum(1);
console.log(total);
```



#### 细胞分裂

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



## 排序算法

#### 数组常用的api

```js
spliece  实现数组增删改
@params  spliece.(n,m)  
从索引n 开始删除m个元素, 若m 不写 是直接删除到末尾
@return 返回删除的部分

push 向末尾追加
pop
unshift 向开头追加
concat  数组拼接
sort 数组排序  return a-b  进行升序排序
```



#### 冒泡排序 Bubble

```js
数组的当前项 与 后一项进行比较, 若后一项大 则交换位置
一共比较 length-1 轮, 每一次都可以有一个最大数放到末尾  最多比较次数一共为 
两者交换 解构赋值  [a,b] = [b,a]

function bubble(arr) {
	let temp = null;
	//外层循环控制比较轮数
	for (var i = 0; i < arr.length-1; i++) {
		for (var j = 0; j < arr.length-i-1; i++) {
			// 里层循环控制每一轮比较次数
			if (arr[j] > arr[j+1]) {
				temp = arr[j];
				arr[j] = arr[j+1];
				arr[j+1] =temp;
                //[arr[j],arr[j+1]] = [arr[j+1],arr[j]]
			}
		}
	}
	return arr;
}
// O(n^2)
```



#### 插入排序

```js
	// 准备一个新数组, 用来存储抓到手里的牌, 开始先抓一张牌
	let handel = [];
	handle.push(arr[0]);

	// 从第二项开始一次抓牌, 直到把台面上的牌都抓光
	for(let i =1; i < arr.length; i++){
		//A 是新抓的牌
		let A = arr[i];
		// 和 HANDLE 中的牌依次比较
		for(let j = handle.length-1; j>=0; j--){
		 // 每一次比较手中的牌
		  let B = handle[j];
		 // 如果当前 新牌A 比 被比较的牌B大了 将A 放到B 的后面
		 if(A > B){
		 	handle,splice(j+1,0,A)
		 	break;
		 }
		 if(j === 0){
		 	handel.unshift(A);
		 	// 已经比到第一项, 我们把新牌放到手中最前面即可.
		 }
		}
	}
	return handle;
}
// O(n^2)
```



#### 快速排序 quick

```js
找到中间项, 将它从运来的数组中移除, 同时获得这一项的结果
让每一项 与 中间项比较, 比它小的放在左边 大的放在右边
function quick(arr){
	//结束递归  当 arr 小于等于 一项，则不用处理
	if(ary.length <= 1){
		return arr;
	}
	// 1. 找到数组的中间项，在原有的数组中把它移除
	let middleIndex = Math.floor(arr.length/2);
	let middleValue = arr.splice(middleIndex,1)[0];

	// 2. 准备左右两个数组，循环剩下数组中的每一项，比当前小的放在左边数组中，反之放到右边的数组中
	let arrLeft = [];
			arrRight = [];
	for(let i=0; i < arr.length; i++){
		let item = arr[i];
		item < middleValue ? arrLeft.push(item) : arrRight.push(item);
	}
	// 3. 递归的方式让左右两边的数组持续这样处理， 一直到左右两边都排好序为止。 最后进行 左边 + 中间 +右边  拼接成最后结果
	return quick(arrLeft).concat(middleValue,quick(arrRight))
}
//O(nlogn)
```



选择排序

O(n²)

归并排序

O(nlogn)

希尔排序

O(nlogn)

堆排序

 O(nlogn)

计数排序

 O(n+k)



桶排序



基数排序

 O(N*M) 

## 数组去重

unserscore 库 中的  _.uniq()

直接使用set

```js
var result = [...  new Set(arr)]
```


之前没有的元素 push 进新数组
```JS
var arr = [1,1,2,3]
function unique(arr) function unique(arr) {
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
    or
    
    arr.foreach(item=>{
        if(result.indexOf(item) === -1) return array.push(item)
    })

}
```

使用filter

```js
function unique(arr) {
  return arr.filter(function(item, index, arr) {
//indexOf()方法返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。
    //当前元素，在原始数组中的第一个索引==当前索引值，否则返回当前元素
    return arr.indexOf(item, 0) === index;
  });

```

使用 reduce 

```js
function unique(arr) {
	var result = arr.reduce((pre,item)=>{
        return pre.includes(item) ? pre : [...pre,item]
    })
  });

```

利用属性的唯一值

```js
function getUniqueArray(){
	var result = {}

	arr.foreach((item,index)=>{
		result[arr[index]] = 'sss';
	})

	result = Objects.keys(result).map(item => ~~item) //字符串转换成数字
	console.log(result);
}
```

使用双重循环

```js
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
```

sort 进行排序  比较相邻两个数的数值

```js
function getUniqueArray(){
	var result = []
	var temp = arr.sort();
	for (var i = 0 ; i < temp.length; i--) {
		if(temp[i] !=== temp[i+1]){
			result.push(arr[i])
		}
	}
}
```

随机交换数组内的元素（洗牌法）

```js
function randomsort(arr){
    var temp,
        leng = arr.length,
        tempindex;
    for(var i = 0; i < leng; i++){
        tempindex = Math.floor(Math.random()*(leng - i) + i);
        temp = arr[i];
        arr[i] = arr[tempindex];
        arr[tempindex] = temp;
    }
    return arr;
}
```

