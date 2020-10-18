---
title: "JavaScript 对象数组深克隆浅克隆&深比较浅比较合并"
date: 2020-10-18T10:02:39+08:00
draft: false
---
# Content
- 深克隆浅克隆
	- 对象
	- 数组
- 深比较浅比较合并
# 深克隆浅克隆
- 对象	 
	- ```js
		// =============================================浅克隆
		let obj1 = {
			name:"Margin",
			course: {
				c1:'CSS',
				c2:'JS'
			}
		};

		// 克隆1：循环遍历 【浅】
		let obj2 ={};
		 keys = [
			 ...Object.keys(obj1),
			 ...Object.getOwnPropertySymbols(obj1)
		 ];
		 keys.forEach(key =>{
			 obj2[key] = obj1[key];
		 });

		 // 克隆2：展开运算符 【浅】
		 let obj2 = {
			 ...obj1
		 };

		 // 克隆3：assign 【浅】
		 // 原理 Object.assign([obj1],[obj2]); => 返回结果仍是obj1堆内存，只不过是把obj2中的键值对和obj1的键值对合在一起
		 let obj = Object.assign({},obj1);
		
		 // 克隆4：自定义浅克隆

		 // function toType ...待补充
		 function getOwnPropertys(obj){
			 /*获得所有私有属性，包括Symbol;*/
			 if (obj == null) return [];
			 return [
				 ...Object.key(obj),
				 ...Object.getOwnPropertySymbols(obj)
			 ];
		 }
		 function shallowClone(obj) {
			 // 处理其他
			 let type = toType(obj);
			 if (/^(number|string|boolean|null|undefined|symbol|bigint)$/.test(type)) return obj;
			 if (/^function$/.test(type)) {
				 // 返回一个不同的函数，但是最后执行的效果和原始函数一直
				 return function proxy () {
					 return obj();
				 };
			 }
			 if (/^(regexp|date|error)$/.test(type)) return new obj.constructor(obj);

			 // ..只处理数组或对象
			 let keys = getOwnPropertys(obj),
			 	 clone = {};
			 // clone = new obj.constructor;
			 Array.isArray(obj)?clone = [] : null;

			 for(let i = 0; i < keys.length; i++) {
					 let key = keys[i];
					 clone[key] = obj[key];
			 }
			 // keys.forEach(key => {
			 //	 clone[key] = obj[key];
		 	 //  });
			 return clone;
			 	
		 }
		 // =============================================深克隆
		 // 克隆1：JSON.stringfy / JSON.parse

		 // 原理：基于JSON.stringfy把原对象（数组）变为字符串，再基于JSON.parse把字符串转化为对象或者数组。
		 // 问题：1.正则，Math，ArrayBuffer对象 => 空对象； 2.函数/Symbol/undefined属性值的属性 => 消失；  3. BigInt => 不能处理； 4. Date => String 
		 let obj2 = JSON.parse(JSON.stringfy(obj1));

		 // 克隆2：自定义深克隆
		 function deepClone(obj, cache=new Set()){
			 // 只有数组和对象再处理深克隆，其余情况同浅克隆； 
			 let type = toType(obj);
			 if (!/^(array|object)$/.test(type)) return shallowClone(obj);
			 // 避免无限递归
			 if(cache.has(obj)) return obj;
			 cache.add(obj);

			 let keys = getOwnPropertys(obj),
				  clone = {};
			 type === "array" ? clone = [] : null;

			 keys.forEach(key => {
				 clone[key] = deepClone(obj[key], cache);
			 });
			 return clone;
		 }
	  ```
- 数组	 
	- ```js
		// =============================================浅克隆
		let arr = [10, 20, [30,40]];

		// 克隆1：循环 for each [浅]
		let arr2 = []; 
		arr1.forEach((item, index) => {
			arr2[index] = item;
		});

		arr2 = arr1.map(item => item);

		// 克隆2：展开运算符 Object.assign 【浅】

		// 克隆3：基于slice/concat 【浅】
		let arr2 = arr1.slice();

		// =============================================深克隆
		// 克隆1:JSON.stringfy / JSON.parse
	  ```

# 深比较浅比较合并
- ```js
	//默认参数
	let defaults = {
		url:'',
		method:'Get',
		headers:{
			'Content-Type':'application\json'
		},
		params:null,
		cache:[true]
	};

	// 用户传递参数
	let options = {
		url:'/api/list',
		headers:{
			'x-token':'xxx'
		},
		params:{
			lx: 0,
			from:'wechat'
		},
		cache:[10]
	};

	// 浅比较合并
	Object.assign(defaults, options);

	// 对象合并
	//  obj1对象 obj2对象：依次遍历obj2替换obj1
	//  obj1对象 obj2不是对象：不进行任何处理
	//  obj1不是对象 ：obj2直接替换obj1
	// 检测数据类型..待补充
	function merge(obj1,obj2){	
		let isPlain1 = isPlainObject(obj1),
			isPlain2 = isPlainObject(obj2);
		if(!isPlain1) return obj2;
		if(!isPlain2) return obj1;
		[
			...Object.keys(obj2),
			...Object.getOwnPropertySymbols(obj2)
		].forEach(key =>{
			obj1[key] = merge(obj1[key],obj2[key]);
		});
	}
  ```