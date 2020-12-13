---
title: "JavaScript 闭包作用域"
date: 2020-09-20T09:02:39+08:00
draft: false
---
# 闭包作用域
```js
//2020/9/19
//1.
let x = 5;
function fn(x) {
    return function(y) {
        console.log(y + (++x));
    }
}
fn(6);
let f = fn(6);
f(7);
fn(8)(9);
f(10);
console.log(x);
```
![闭包作用域](https://github.com/MarginLon/MarginPostImage/blob/master/%E5%87%BD%E6%95%B0%E9%97%AD%E5%8C%85.png?raw=true)
```js
//2.
let a=0,
    b=0;
function A(a) {
    A = function(b){
        console.log(a+b++);
    };
    console.log(a++);
}
A(1);
A(2);
```
![闭包作用域](https://github.com/MarginLon/MarginPostImage/blob/master/%E5%87%BD%E6%95%B0%E9%97%AD%E5%8C%852.png?raw=true)


```js
  var buttons = document.querySelectorAll('button');
  for (var i = 0; i < buttons.length; i++) {
    // i=0 buttons[0] 第一个按钮
    // i=1 buttons[1] 第二个按钮
    // ....
    // 每一轮循环 i 变量的值 和 需要获取对应某个按钮的索引是一样的  buttons[i]
    buttons[i].onclick = function(){
       console.log('获取当前按钮索引:${i}');
       //不能实现
    };
  }

  //方案1.1：基于“闭包”[每一轮循环都产生一个闭包，存储对应索引；点击事件触发，执行对应函数，让其上级context闭包]
  var buttons = document.querySelectorAll('button');
  for (var i = 0; i < buttons.length; i++) {
      // 每一轮循环形成一个闭包，存储私有变量i的值
      //    + 自执行函数执行，产生EC(A) 私有形参i=0/1/2
      //    + EC（A）中有个小函数,让全局buttons中的某一项占用创建的函数
    (function(i) {
       buttons[i].onclick = function(){
        console.log('获取当前按钮索引:${i}');
       };
    })(i);
  }

  //方案1.2：
   var buttons = document.querySelectorAll('button');
  for (var i = 0; i < buttons.length; i++) i{
       buttons[i].onclick = function(i){
        return function () {
            console.log('获取当前按钮索引:${i}');
            };
    })(i);
  }
  //方案1.2注解
  var obj = { //返回值赋值给fn
      fn: (function(){
          console.log('大函数');
          return function(){
              console.log('小函数');
          }
      })()
  };
  obj.fn();//执行返回的小函数

  //方案1.3 基于let也是闭包
  let buttons = document.querySelectorAll('button');
  for (let i = 0; i < buttons.length; i++) i{
       buttons[i].onclick = function(){
            console.log('获取当前按钮索引:${i}');
            };
  }

  //方案2 自定义属性
  var buttons = document.querySelectorAll('button');
  for (var i = 0; i < buttons.length; i++) i{
      // 每一轮循环给当前button设置自定义属性存索引
       buttons[i].myIndex = i;
       buttons[i].onclick = function(){
           // this -> 当前点击的按钮
            console.log('获取当前按钮索引:${this.myIndex}');
       };
  }

  //方案3 事件委托 html <button index='i'></button>;
  // 无论点击body中的谁，都会触发body的点击事件
  // ev.target事件源：具体点击的是谁
  document.body.onclick = function(ev) {
      var target = ev.target
          targetTag = target.tagName;
      if(targetTag==="BUTTON"){
          var index = target.getAttribute('index');
          console.log('获取当前按钮索引:${this.myIndex}');
      }
  };
```
