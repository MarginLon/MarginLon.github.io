---
title: "JavaScript Promise"
date: 2020-10-18T14:02:39+08:00
draft: false
---
# Content
- Promise
---
# Promise
- ES6新增的一个内置类，承诺/约定模式，基于这种模式可以有效地处理异步
- ```js
	//“AJAX串行"
	let data = null;
	//基于JQ->AJAX异步从服务器获取数据
	$.ajax({
		url:'api/1.json',
		method:'GET',
		dataType:'json',
		success:function(result) {
			data = result;
		}
	});
		// 回调地狱
		$.ajax({
		url:'api/1.json',
		method:'GET',
		dataType:'json',
		success:function(result) {
				$.ajax({
		url:'api/2.json',
		method:'GET',
		dataType:'json',
		success:function(result) {
				$.ajax({
		url:'api/3.json',
		method:'GET',
		dataType:'json',
		success:function(result) {
			// ...
		}
	});
		}
	});
		}
	});

	// Promise
	const api1 = () => {
		return new Promise(resolve => {
		 	$.ajax({
		url:'api/1.json',
		method:'GET',
		dataType:'json',
		success:function(result) {
			resolve(result);
		}
	});
		});
	};
	const api2 = () => {
		return new Promise(resolve => {
		 	$.ajax({
		url:'api/2.json',
		method:'GET',
		dataType:'json',
		success:function(result) {
			resolve(result);
		}
	});
		});
	};
	const api3 = () => {
		return new Promise(resolve => {
		 	$.ajax({
		url:'api/3.json',
		method:'GET',
		dataType:'json',
		success:function(result) {
			resolve(result);
		}
	});
		});
	};

	api1().then(result => {
		return api2();
	}).then(result => {
		return api3();
	}).then(result => {
		console.log('OK');
	});

	(async function(){
		let result = await api1();

		result = await api2();

		result = await api3();
	})();
  ```
- 异步：
	- ajax请求
	- 事件绑定
	- 定时器
	- Promise/async/await
	- window.requestAnimationFrame
- ```js
	// new Promise
		// 立即执行传递的executor函数
		 // 在executor函数中一般用来管控一个异步的操作
		 // 传递给executor函数两个函数参数
		// 创造Promise实例 
		 // [[PromiseState]] ：3种状态 "pending" "fulfilled/resolved" "rejected"
		 // [[PromiseResult]] :默认undefined，存储成功的结果或失败的原因
		 // p1.__proto__ -> Promise.prototype : then / catch / finally
		//执行resolve控制实例的状态变为成功，传递的值是成功的结果
		 //  [[PromiseState]] : 'fulfilled'
		 //  [[PromiseResult]] :100
		 // resolve(100);

		//执行reject控制实例的状态变为失败
		 //  [[PromiseState]] : 'rejected'
		 //  [[PromiseResult]] :0
		 // reject(0);

		//一旦状态从pending改变，无法再次改变
		 // 报错 => rejected
		
		//执行顺序
			// 1.new Promise
			// 2.executor:一个异步定时器
			// 3.p1.then注入2个方法
			// ----等待1000ms
			// 4.执行定时器回调函数：执行resolve改变promise状态
			// 5.通知之前基于then注入的两个方法的第一个执行
	let p1 = new Promise(function(resolve, reject){
		setTimeout(()=>{
			resolve('OK');
		},1000);
	});
	p1.then(result =>{
		// p1实例的状态修改为fulfilled，通知第一个函数执行，result ->[[PromiseResult]]
	}, reason => {
		// p1实例的状态修改为rejected，通知第二个函数执行，reason ->[[PromiseResult]]
	});


	let p1 = new Promise(function(resolve, reject){
		console.log(1); // ->(1)
			resolve('OK'); // 修改状态和值，并通知基于Then注入的方法执行[问题:.Then还没执行，方法还没注入，不知道该通知谁来执行]
			// 此时需要把通知方法执行的操作先保存起来 【放入到等待任务队列】 ->异步操作
		console.log(2); // ->(2)
	});
	p1.then(result =>{
		// p1实例的状态修改为fulfilled，通知第一个函数执行，result ->[[PromiseResult]]
		console.log(result); //->(4)
	}, reason => {
		// p1实例的状态修改为rejected，通知第二个函数执行，reason ->[[PromiseResult]]
		console.log(reason);
	});
	console.log(3); // ->(3)


	let p1 = new Promise(resolve => {
		setTimeout(()=>{
			resolve('OK'); // -> 立即修改状态和值 同步
			console.log(1); // ->(1) 说明无论是否基于then注入了方法，执行resolve/reject，通知对应注入方法执行的操作是异步操作，不立即执行，排入等待队列，其他处理完再通知对应方法执行
		},1000);
	});
	p1.then(result => {
		console.log(2); // -> (2)
	});
  // ==============================================
  	// promise实例状态和值
	// 1.new Promise
		// executor resolve/reject执行控制其状态及值 执行失败控制报错
	// 2. .then返回的新实例
		// .then注入的两个方法无论哪个执行，只要不报错，新实例的状态即"fulfilled"；只要执行报错，新实例的状态就是rejected;且新实例的[[Result]]是方法返回的值
		// 但如果方法执行返回的是一个新的promise实例，则此实例最后的成功或者失败，直接决定.then返回实例的成功和失败，得到的结果是一样的。

	let p1 = Promise.resolve('OK');
	let p2 = p1.then(result => {
		console.log('成功->',result); // 成功 'OK'
		return 10; 
	}, reason => {
		console.log('失败->',reason);
	});

	p2.then(result => {
		console.log('成功->',result); // 成功 10
	}, reason => {
		console.log('失败->',reason);
	});

	console.log(p2); //promise 新实例 执行.then返回一个全新的promise实例
	
	let p1 = Promise.reject('NO');
	let p2 = p1.then(result => {
		console.log('成功->',result); 
		return 10; 
	}, reason => {
		console.log('失败->',reason); //失败 NO 
		return 20;
	});

	p2.then(result => {
		console.log('成功->',result); // 成功 20
	}, reason => {
		console.log('失败->',reason);
	});

	let p1 = Promise.resolve('OK');
	let p2 = p1.then(result => {
		console.log('成功->',result);  //-> 成功 'OK'
		return Promise.reject('NO'); 
	}, reason => {
		console.log('失败->',reason); 
		return 20;
	});

	p2.then(result => {
		console.log('成功->',result); 
	}, reason => {
		console.log('失败->',reason); // -> 失败 'NO'
	});


	// 对于失败的promise实例，如果没有进行任何的方法处理，则console抛出异常【但不会阻碍其余代码执行】
	Promise.reject('NO').then(result => {
		console.log('成功->',result); 
		return 10;
	}, ()=>{});

	// .then注入方法的时候， 如果其中某个方法没有传递， 则会顺延到下一个then中具备相同状态需要执行的函数中
	Promise.reject('NO')
	.then(result => {
		console.log('成功->',result); 
		return 10;
	}/*,reason=>{ return Promise.reject(reason);}*/)
	.then(null, reason => {
		console.log('失败->'),reason); // -> 失败 'NO'
	});

	Promise.resolve('OK')
	.then(null, reason => {
		console.log('失败->'),reason); 
	})
	.then(result => {
		console.log('成功->',result); // ->成功 'OK' 
	});

	// 存放多个成功，最后一个THEN存放失败，无论某一次失败导致promise实例状态是失败的，都会顺延到最后一个失败的处理函数上进行处理
	//  + then(null,return => {...}) 用 catch(reason=>{...}) 代替
	Promise.reject('NO')
	.then(result => {
		console.log('成功->',result); 
		return 10;
	})
	.then(result =>{
		console.log('成功->',result); 
		return 20;
	})
	.then(null, reason => {
		console.log('失败->'),reason); 
	});

	// 多处理 
		// Promise.all 等待所有promise实例都成功，整体返回的状态才是成功，只要有一个失败，整体失败
		// Promise.race 看谁先处理完，先处理完成的状态就是最后整体的状态

	const api1 = () => {
		return new Promise(resolve => {
			resolve('OK'); 
		}
	};
	const api2 = () => {
		return new Promise(resolve => {
			resolve('OK'); 
		}
	};
	const api3 = () => {
		return new Promise(resolve => {
			resolve('OK'); 
		}
	};
	const fn = () => {
		return new Promise(resolve => {
			setTimeout(() => {
				resolve(100);
			},1000);
		});
	};
	const AA = Promise.resolve('AA');

	let p = Promise.all([api(), api2(), api3(), AA, fn(), 10]);
	p.then(result =>{
		//都成功，p成功；results存每个promise的结果
		console.log('成功->',result); 
	})
	.catch(reason =>{
		//只要有一个失败，立即结束，p失败，记录谁失败即原因
		console.log('成功->',reason); 
	});

	// ajax并行：同时发送多个异步的ajax请求（三者之间没有依赖关系），但需要所有的异步请求都处理成功，再统一完成任务
  ```
  