---
title: "JavaScript 数据类型检测底层机制"
date: 2020-10-16T10:02:39+08:00
draft: false
---
# Content
- 数据类型检测底层机制
	+ typeof
	+ instanceof
	+ constructor
	+ Object.prototype.toString.call
- 重写instanceof
# 数据类型检测底层机制
+ typeof 
	+ 返回结果为字符串
	+ ```typeof typeof xxx =>"string"```
	+ ```typeof null => "object"```
	+ 无法细分普通或数组等对象，一律为object
+ instanceof
	+ 检测当前实例是否属于这个类 ```Array[Symbol.hasInstance](arr)```
	+ 一般只用于对象的具体细分，认不清正则
	+ 不能证明 ```xxx instaceof Object```是true就是普通对象
	+ 无法应用到原始值类型检测
	+ 改变了prototype的也不能判断
	+ 
	```js
	let obj = {};
	arr instance of obj; // error  Function.prototype
	```
	+ Symbol.hasInstance原理
		+ (\_\_proto\_\_)是否存在类原型
			- ```js
				arr.__proto__===Array.prototype 
				 // =>  arr instanceof Array : true
			  ```
			- ```js
				arr.__proto__.__proto__===Object.prototype 
				 // =>  arr instanceof Object : true
			  ```
+ constructor
	+ constructor可以被随意更改
	+ 支持基本类型值
+ Object.prototype.toString.call([value])
	+ 除Object.prototype.toString不是转换字符串用来检测数据类型，其余都是
	+ 返回结果"[object 对象[Symbol.toStringTag||对象.构造函数(不受自己更改的影响，对内置类有效)||Object]]"
---
# 重写instanceof
- [重写instanceof](https://github.com/MarginLon/CSS_JS_Repos/blob/main/JS/instanceof.js)
	

