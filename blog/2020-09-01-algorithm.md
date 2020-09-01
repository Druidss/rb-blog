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

```



#### 快速排序 quick

```
找到中间项, 将它从运来的数组中移除, 同时获得这一项的结果
让每一项 与 中间项比较, 比它小的放在左边 大的放在右边

```



选择排序



归并排序



希尔排序



堆排序



计数排序



桶排序



基数排序

## 数组去重