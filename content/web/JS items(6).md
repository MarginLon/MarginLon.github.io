---
title: "JavaScript 练习（一）"
date: 2020-09-21T10:02:39+08:00
draft: false
---
## 变量提升
------
### 红笔标注思考时间长或存疑错点
#### 1.
```js
console.log(a, b, c);
var a = 12,
    b = 13,
    c = 14;
function fn(a) {
    console.log(a, b, c);
    a = 100;
    c = 200;
    console.log(a, b, c);
}
b = fn(10);
console.log(a, b, c);
```
  + 结果:
    - undefined,undefined,undefined
    - <span style="color:red;">10,13,14</span>
    - 100, <span style="color:red;">13</span>, 200
    - <span style="color:red;">12, undefined, 200</span>
    
  + 分析：
    - 第一行console.log输出时， 变量提升 ```var a, b, c;```，只声明不定义
    - 第二行console.log是在```function fn(a){...}```内的，当```b=fn(10)```执行，此时```b,c```在全局context已经定义，函数fn中没有私有变量```b,c```，基于作用域链向上查找，而```a```是实参传递给形参得到10.
    - 第三行console.log是在```function fn(a){...}```内的，此时```a,c```被赋值100，200.
    - 第四行console.log是在```b=fn(10)```执行后，此时```a```作为全局context的```a```，值为12，```c```在函数fn中赋值```c=200;```得到200，最后fn没有形成闭包，堆内存被释放, b没有指向，故```undefined```

#### 2.
```js
var i = 0;
function A() {
    var i = 10;
    function x() {
        console.log(i);
    }
    return x;
}
var y = A();
y();
function B() { 
    var i = 20;
    y();
}
B();
```
 + 结果:
    - 10
    - <span style="color:red;">10</span>
    
  + 分析：
    - 第一个10，按照函数底层机制步骤推算。
    - 第二个10，B()的私有变量i为20， y() => A的x()，x的作用域链使得B的私有变量i没有影响到console.log(i)的输出。<span style="color:red;">(存疑)</span>

#### 3.
```js
var a=1;
var obj ={
   name:"tom"
}
function fn(){
   var a2 = a;
   obj2 = obj;
   a2 =a;
   obj2.name ="jack";
}
fn();
console.log(a);
console.log(obj);
```
 + 结果:
    - 1
    - { name:"jack" }
    
  + 分析：
    - 见 JS.let/var/this中带var不带var的区别

#### 4.
```js
var a = 1;
function fn(a){
    console.log(a)
    var a = 2;
    function a(){}
}
fn(a);
```
 + 结果:
    - <span style="color:red;">[Function: a]</span>
    
  + 分析：
    - 按var function的顺序变量提升

#### 5.
```js
console.log(a); 
var a=12; 
function fn(){
    console.log(a); 
    var a=13;  
}
fn();   
console.log(a);

----

console.log(a); 
var a=12;
function fn(){
    console.log(a);
    a=13;
}
fn();
console.log(a);

----
```
 + 结果:
    - undefined
    - undefined
    - 12
    - //分割线//
    - undefined
    - 12
    - 13
    
  + 分析：
    - 见 JS.let/var/this中带var不带var的区别

#### 6.
```js
var foo='hello'; 
(function(foo){
   console.log(foo);
   var foo=foo||'world';
   console.log(foo);
})(foo);
console.log(foo);
```
 + 结果:
    - hello
    - hello
    - hello
    
  + 分析：
    - ```'hello'||'world'```结果为```'hello'```
#### 7.重中之重，精力有限，暂时似懂非懂，本周五考完试分析过程
```js
{
    function foo() {}
    foo = 1;
}
console.log(foo);

----

{
    function foo() {}
    foo = 1;
    function foo() {}
}
console.log(foo);

----

{
    function foo() {}
    foo = 1;
    function foo() {}
    foo = 2;
}
console.log(foo);
```
 + 结果:
    - <span style="color:red;">[Function:foo]</span>
    - <span style="color:red;">1</span>
    - <span style="color:red;">1</span>
    
  + 分析：
    - [代码块提升解析](https://juejin.im/post/6844903955814694919)  

#### 8.
```js
var x = 1;
function func(x,y=function anonymous1(){x=2}) {
  x = 3;
  y();
  console.log(x);
}
func(5);
console.log(x);
---
var x = 1;
function func(x,y=function anonymous1(){x=2}) {
  var x = 3;
  y();
  console.log(x);
}
func(5);
console.log(x);
---
var x = 1;
function func(x,y=function anonymous1(){x=2}) {
  var x = 3;
  var y = function anonymous1(){x=4};
  y();
  console.log(x);
}
func(5);
console.log(x);
```
 + 结果:
    - hello
    - hello
    - hello
    
  + 分析：
    - ```'hello'||'world'```结果为```'hello'```

## 数据类型和基础知识
------
### 红笔标注思考时间长或存疑错点
#### 1.
```js
let result = 100 + true + 21.2 + null + undefined + "Tencent" + [] + null + 9 + false;
console.log(result);
```
+ 结果：
  - NaNTencentnull9false

#### 2.
```js
{}+0?alert('ok'):alert('no');
0+{}?alert('ok'):alert('no');
```
+ 结果：
  - no
  - ok

#### 3.
```js
let res = Number('12px');
if(res===12){
    alert(200);
}else if(res===NaN){
    alert(NaN);
}else if(typeof res==='number'){
    alert('number');
}else{
    alert('Invalid Number');
}
```
+ 结果：
  - number

#### 4.
```js
let arr = [27.2,0,'0013','14px',123];
arr = arr.map(parseInt);
console.log(arr);
```
+ 结果：
  - 27
  - <span style="color:red;">NaN</span>
  - 1
  - 1
  - 27
+ 分析：
  - parseInt([value],[radix])

## 闭包作用域
------
### 红笔标注思考时间长或存疑错点
#### 1.
```js
var a = 10,
    b = 11,
    c = 12;
function test(a) {
    a = 1;
    var b = 2;
    c = 3;
}
test(10);
console.log(a, b, c);
```
+ 结果：
  - 10 ,11 ,3
#### 1.
```js
var a = 4;
function b(x, y, a) {
    console.log(a);
    arguments[2] = 10;
    console.log(a);
}
a = b(1, 2, 3);
console.log(a);
```
+ 结果：
  - 3
  - 10
  - undefined
#### 3.
```js
var a = 9;
function fn() {
    a = 0;
    return function (b) {
        return b + a++;
    }
}
var f = fn();
console.log(f(5));
console.log(fn()(5));
console.log(f(5));
console.log(a);
```
+ 结果：
  - <span style="color:red;">5</span>
  - 5
  - <span style="color:red;">6</span>
  - <span style="color:red;">2</span>
+ 分析：
  - 错因：先return值再a++
#### 4.
```js
var test = (function (i) {
    return function () {
        alert(i *= 2);
    }
})(2);
test(5);
```
+ 结果：
  - 4
#### 5.
```js
var x = 4;
function func() {
    return function(y) {
        console.log(y + (--x));
    }
}
var f = func(5);
f(6);
func(7)(8);
f(9);
console.log(x);
```
+ 结果：
  - 9 
  - 10
  - 10
  - 1
#### 6.
```js
var x = 5,
    y = 6;
function func() {
    x += y;
    func = function (y) {
        console.log(y + (--x));
    };
    console.log(x, y);
}
func(4);
func(3);
console.log(x, y);
```
+ 结果：
  - <span style="color:red;">11 6</span>
  - <span style="color:red;">13</span>
  - <span style="color:red;">10 6</span>
+ 分析：
  - <span style="color:red;">存疑</span>
#### 7.
```js
function fun(n, o) {
    console.log(o);
    return {
        fun: function (m) {
            return fun(m, n);
        }
    };
}
var c = fun(0).fun(1);
c.fun(2);
c.fun(3);
```
+ 结果：
  - undefined
  - 0
  - 1
  - 1
+ 分析：
  - <span style="color:red;">存疑</span>
#### 8.
+ 闭包：
  + 函数执行形成私有context，context中的某些内容（一般堆内存地址）被context以外的事物（变量等）占用，则当前context不能被释放。
    - 优点：
      * 保护：保护私有context的私有变量和外界互不影响
      * 保存：context的私有变量和值保存起来
    - 弊端：栈内存太大，影响性能，需合理利用
#### 9.
 - var 存在变量提升 let 不存在变量提升
 - 全局context var相当于给GO增一个属性，一改随改；let和GO没有关系。
 - let不允许同context重复声明（不管先前何种方式声明，都不能let再声明），var无所谓。
 - let产生块级私有context
#### 10.
```js
var b = 10;
(function b() {
    b = 20;
    console.log(b);
})();
console.log(b);
```
+ 结果：
  - [Function: b]
  - 10
+ 分析：
  - <span style="color:red;">```b=20```存疑</span>
+ 修改代码：
```js
var b = 10;
(function b() {
    let b = 20;
    console.log(b);
})();
console.log(b);
```
#### 11.
```js
function fn(a,b){
   return function(c){
       return a+b+c;
   }
}
```
#### 12.
```js
//暂超出能力范围，因本周五有必修课考试，实难在本周花费精力完成此题目。
```

## this
------
### 红笔标注思考时间长或存疑错点（this掌握不行，需再练习）
#### 1.
```js
var num = 10;
var obj = {
    num: 20
};
obj.fn = (function (num) {
    this.num = num * 3;
    num++;
    return function (n) {
        this.num += n;
        num++;
        console.log(num);
    }
})(obj.num);
var fn = obj.fn;
fn(5);
obj.fn(10);
console.log(num, obj.num);
```
+ 结果：
  - 22
  - 23
  - 65 30
#### 2.
```js
let obj = {
    fn: (function () {
        return function () {
            console.log(this);
        }
    })()
};
obj.fn();
let fn = obj.fn;
fn();
```
+ 结果：
  - {fn:[Function]}
  - Object [global]{
     ...
    }
#### 3.
```js
var fullName = 'language';
var obj = {
    fullName: 'javascript',
    prop: {
        getFullName: function () {
            return this.fullName;
        }
    }
};
console.log(obj.prop.getFullName());
var test = obj.prop.getFullName;
console.log(test());
```
+ 结果：
  - undefined
  - language
#### 4.
```js
var name = 'window';
var Tom = {
    name: "Tom",
    show: function () {
        console.log(this.name);
    },
    wait: function () {
        var fun = this.show;
        fun();
    }
};
Tom.wait();
```
+ 结果：
  - window
#### 5.
```js
window.val = 1;
var json = {
    val: 10,
    dbl: function () {
        this.val *= 2;
    }
}
json.dbl();
var dbl = json.dbl;
dbl();
json.dbl.call(window);
alert(window.val + json.val);
```
+ 结果：
  - 24
#### 6.
```js
(function () {
  var val = 1; 
  var json = {
    val: 10,
    dbl: function () {
              val *= 2;
          }
  };
  json.dbl();
  alert(json.val + val);
})();
```
+ 结果：
  - 12
