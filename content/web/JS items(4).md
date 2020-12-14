---
title: "JavaScript let/var/this"
date: 2020-09-20T15:02:39+08:00
draft: false
---

# this

```js
//函数执行主体：谁执行函数
//函数执行context：在哪执行

console(this);//window
{
    let n = 12;
    console(this);//window
}      

// 1.事件绑定：给当前元素的某个事件行为绑定方法，当事件触发、方法执行，方法中的this是当前元素本身
//IE6~8 DOM2事件绑定 attachEvent //window
document.body.onclick = function () {
    console.log(this);//body
};

// 2.普通函数执行
// 函数执行前是否有点，没有点，this即window（严格模式下undefined）
// 有点，点谁this谁
// 匿名函数（自执行函数/回调函数）如果没有特殊处理，则this一般都是window/undefined
function fn(){
     console.log(this);//创建时不能确定this
}
let obj = {
    name:'ABC';
    fn:fn();
};
fn();//window

//
function fn(callback) {
    callback();//this->window
}
let obj = {
    sum(){
        console.log(this);
    }
};
obj.sum();//this->obj;
fn(obj.sum);

//
setTimeout(function(){
    console.log(this); //window
},1000);

//
let obj = {
    name:'xxx'
};
let arr = [10,20];
arr.forEach(function(item,index){
    console.log(this); // obj 触发回调函数执行的时候,forEach内部把回调函数的this改为传递的第二个参数值obj
},obj);

//
let obj = {
    sum(){
        console.log(this);
    }
};
(obj.sum)();//this->obj
(10,obj.sum)();//this->window


```

            