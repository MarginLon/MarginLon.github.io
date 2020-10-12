---
title: "JavaScript 练习（二）"
date: 2020-10-10T10:02:39+08:00
draft: false
---
### 面向对象
1. 
```js
function fun(){
    this.a=0;
    this.b=function(){
        alert(this.a);
    }
}
fun.prototype={
    b:function(){
        this.a=20;
        alert(this.a);
    },
    c:function(){
        this.a=30;
        alert(this.a)
    }
}
var my_fun=new fun();
my_fun.b();
my_fun.c();
```
- Answer: 0  30
---
2. 
```js
function C1(name) {
    if (name) {
        this.name = name;
    }
}
function C2(name) {
    this.name = name;
}
function C3(name) {
    this.name = name || 'join';
}
C1.prototype.name = 'Tom';
C2.prototype.name = 'Tom';
C3.prototype.name = 'Tom';
alert((new C1().name) + (new C2().name) + (new C3().name));
```
- Answer: 'Tomundefinedjoin'
---
3. 
```js
function Fn() {
    let a = 1;
    this.a = a;
}
Fn.prototype.say = function () {
    this.a = 2;
}
Fn.prototype = new Fn;// 原型重定向
let f1 = new Fn;
​
Fn.prototype.b = function () {
    this.a = 3;
};
console.log(f1.a);
console.log(f1.prototype);
console.log(f1.b);
console.log(f1.hasOwnProperty('b'));
console.log('b' in f1);
console.log(f1.constructor == Fn);
```
- Answer: 
    * 1
    * undefined
    * [Function]
    * false
    * true
    * true
---
4.
```js
function Foo() {
    getName = function () {
        console.log(1);
    };
    return this;
}
Foo.getName = function () {
    console.log(2);
};
Foo.prototype.getName = function () {
    console.log(3);
};
var getName = function () {
    console.log(4);
};
function getName() {
    console.log(5);
}
Foo.getName();
getName();
Foo().getName();
getName();
new Foo.getName();
new Foo().getName();
new new Foo().getName();
```
- Answer: 2 4 1 1 2 3 3
---
5.
```js
let n = 10;
let m = n.plus(10).minus(5);
console.log(m);//=>15（10+10-5）
```
- Answer:
```js
function compute(num){ 
    num = Number(num); 
    return isNaN(num)?0:num;
    }

Number.prototype.plus = function(n){
    return this+compute(n);
    }

Number.prototype.minus = function(n){
    return this-compute(n);
    }
```
- 补充:
```js
const check = value => {
    value = +value;
    return isNaN(value) ? 0 : value;
};
Number.prototype.plus = function(value){
    // this->n [对象数据类型]
    value = check(value);
    return this + value;
}
Number.prototype.minus = function(value){
    // this->n [对象数据类型]
    value = check(value);
    return this - value;
}
```
---
6.
```js
/*
 * 编写queryURLParams方法实现如下的效果（至少两种方案）
 */
let url="http://www.baidu.com";
console.log(url.queryURLParams("from")); //=>"wx"
console.log(url.queryURLParams("_HASH")); //=>"video"
```
- Answer: 
```js
```
---
7.
```js
function Modal(x,y){
    this.x=x;
    this.y=y;
}
Modal.prototype.z=10;
Modal.prototype.getX=function(){
    console.log(this.x);
}
Modal.prototype.getY=function(){
    console.log(this.y);
}
Modal.n=200;
Modal.setNumber=function(n){
    this.n=n;
};
let m = new Modal(10,20);
```
- Answer: 
```js
class Parent {
    constructor(){
        this.z = 10;
        this.getX = function(){
             console.log(this.x);
            }
        this.getY = function(){
            console.log(this.y);
            }
    }
}
class Modal {
    constructor(x,y) {
        this.x = x;
        this.y = y;
    }
    z;
    getX(){}
    getY(){}
    n = 200;
    setNumber = function (n){
        this.n = n;
    };
}
let m = new Modal(10,20);
//console.log(m);
```
---
8.
```js
let obj = {
    2: 3,
    3: 4,
    length: 2,
    push: Array.prototype.push
}
obj.push(1);
obj.push(2);
console.log(obj);
```
- Answer: { '2': 1, '3': 2, length: 4, push: Array.prototype.push }
---
9.
```js
var a = ?;
if (a == 1 && a == 2 && a == 3) {
    console.log('OK');
}
```
- Answer: 
```js
```
---
10.
```js
let utils = (function(){
    /*
     * toArray：转换为数组的方法
     *   @params
     *      不固定数量，不固定类型
     *   @return
     *      [Array] 返回的处理后的新数组
     */
    function toArray(){
        //=>实现你的代码（多种办法实现）   
    }

    return {
        toArray
    };
})();
let ary = utils.toArray(10,20,30); //=>[10,20,30]
ary = utils.toArray('A',10,20,30); //=>['A',10,20,30]
```

- Answer:
```js
let utils = (function(){

    function toArray(...args){
      // 1.return [].slice.call(arguments)
      // 2.return Array.from(args)
      // 3.return [...args]
    }

    return {
        toArray
    };
})();
let ary = utils.toArray(10,20,30); //=>[10,20,30]
ary = utils.toArray('A',10,20,30); //=>['A',10,20,30]
```
---
11.
```js
//=>浅克隆：只复制对象或者数组的第一级内容
//=>深克隆：克隆后数组的每一级都和原始数组没有关联
//那么请说出，浅克隆都怎么去实现，如何实现深度克隆
let obj = {
    a: 100,
    b: [10, 20, 30],
    c: {
        x: 10
    },
    d: /^\d+$/
};

let arr = [10, [100, 200], {
    x: 10,
    y: 20
}];
```
- Answer:
```js

```
---
12. 
```js
//=>example：要检测的实例
//=>classFunc:要检测的类
function instance_of(example, classFunc) {
    //...
}
let res = instance_of([12,23],Array);
console.log(res); //=>true
```
- Answer
```js
function instance_of(example, classFunc) {
return Object.prototype.toString.call(example)===`[object ${classFunc.name}]`
}
```
---
1. 
```js
//=>编写toType方法，实现数据类型检测
function toType( obj ) {
   //完成你的代码
}
console.log(toType(1)); //=>"number"
console.log(toType(NaN)); //=>"number"
console.log(toType([])); //=>"array"
console.log(toType(/^\d+$/)); //=>"regexp"
console.log(toType({})); //=>"object"
```
- Answer:
```js

```
2. 
```js
~function(){
    function change(){
        //=>实现你的代码
    };
    Function.prototype.change=change;
}();
let obj = {name:'zhufeng'};
function func(x,y){
    this.total=x+y;
    return this;
}
let res = func.change(obj,100,200);
//res => {name:'Alibaba',total:300}
```
- Answer:
```js

```
3. 
```js
~function(){
    //=>bind方法在IE6~8中不兼容，接下来我们自己基于原生JS实现这个方法
    function bind(){

    };
    Function.prototype.bind=bind;
}();
var obj = {name:'zhufeng'};
function func(){
    console.log(this,arguments);
    //=>当点击BODY的时候，执行func方法，输出：obj [100,200,MouseEvent事件对象]
}
document.body.onclick = func.bind(obj,100,200);
```
- Answer:
```js

```
4. 
```js
var name = '珠峰培训';
function A(x,y){
    var res=x+y;
    console.log(res,this.name);
}
function B(x,y){
    var res=x-y;
    console.log(res,this.name);
}
B.call(A,40,30);
B.call.call.call(A,20,10);
Function.prototype.call(A,60,50);
Function.prototype.call.call.call(A,80,70);
```
- Answer:
```js
10,"A"
NaN undefined

NaN undefined
```