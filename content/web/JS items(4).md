---
title: "JavaScript let/var/this"
date: 2020-09-20T15:02:39+08:00
draft: false
---
# let/var
- 传统声明变量：var function
- ES6：let const import()
- let VS const
    - let 变量储值可改 
    - const 赋值不能再与其他赋值关联
- let VS var
    - var 存在变量提升 let 不存在变量提升
        + 变量提升：代码执行前“var/function”提前声明或定义
            - var 只声明
            - function 声明+定义
    - 全局context var相当于给GO增一个属性，一改随改；let和GO没有关系。
    - let不允许同context重复声明（不管先前何种方式声明，都不能let声明），var无所谓。
    - var
        + var：方法内局部，方法外全局
        + 不加var：全局
        + ![var](https://github.com/MarginLon/MarginPostImage/blob/master/var%E5%8F%98%E9%87%8F.png?raw=true)
    - 暂时性死区（暂存的Bug）
        + ```js
          console.log(typeof n);//undefined
          let n = 12;//使上一句报错 
          ```
    - let产生块级私有context
        + context & 作用域
            - 全局context
            - 函数执行的私有context
            - 块级作用域（私有context）
                - 对象 function的大括号 判断，循环和代码块的大括号
                ```js
                    debugger;//开启断点调试,控制台基于F10/F11 逐过程/逐语句 控制执行
                    //代码块不会对n产生限制，n使全局context
                    {
                        var n = 12;
                        console.log(n);

                        let m = 13;
                    }
                    console.log(n);
                    console.log(m);// m is not defined


                    let i = 0;//不产生块级context
                    for (; i< 5;i++)
                    {
                        console.log(i);
                    }
                    console.log(i);//5
                ```
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

            