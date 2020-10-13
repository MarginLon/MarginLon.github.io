---
title: "JavaScript JQ源码对象相关"
date: 2020-10-13T10:02:39+08:00
draft: false
---
- 类数组想用数组中的方法
```js
let obj = {
    0:10,
    1:20,
    length:2
};
// 解法1： 改变this
Array.prototype.forEach.call(obj,item=>{console.log(item);});
// 解法2:  改变原型指向
obj.__proto__ = Array.prototype;
obj.forEach(item=>console.log(item));

// 解法3:  需要用的方法作为obj的一个私有属性
obj.each = Array.prototype.forEach;
obj.each = (item => console.log(item));
```
---
# 数据类型检测
```js
/*JQ中数据类型检测源码*/
var class2type = {};

var toString = class2type.toString;

var hasOwn = class2type.hasOwnProperty;

var fnToString = hasOwn.toString;

var ObjectFunctionString = fnToString.call( Object );

var support = {};

var isFunction = function isFunction( obj ) {

      // Support: Chrome <=57, Firefox <=52
      // In some browsers, typeof returns "function" for HTML <object> elements
      // (i.e., `typeof document.createElement( "object" ) === "function"`).
      // We don't want to classify *any* DOM node as a function.
      return typeof obj === "function" && typeof obj.nodeType !== "number";
  };


	var isWindow = function isWindow(obj) {
	// window.window === window
		return obj != null && obj === obj.window;
	};
function toType( obj ) {
	if ( obj == null ) {
		return obj + "";
	}

	// Support: Android <=2.3 only (functionish RegExp)
	return typeof obj === "object" || typeof obj === "function" ?
		class2type[ toString.call( obj ) ] || "object" :
		typeof obj;
}

```
