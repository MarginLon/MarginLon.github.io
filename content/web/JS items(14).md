---
title: "JavaScript 对象"
date: 2020-10-11T10:02:39+08:00
draft: false
---
### 原型重定向
1. 内置类原型无法重定向
2. 大量方法扩充
```js
function Fn(){}
Fn.prototype = Object.assign(Fn.prototype,{
    say(){},
    jump(){},
    eat(){}
});

//简化编写，统一管理
// 弊端 : constructor丢失 原有的原型方法丢失 
//          + 手动设置constructor 和方法
//          + 新旧原型对象合并 
```
---
### 对象数据类型
+ 普通/日期/正则/数组/DOM元素/类数组集合...
+ prototype原型(排除Function.prototype)
+ \_\_proto\_\_(排除Object.prototype.\_\_proto\_\_)
+ ...
+ 函数
    + 所有的函数也是"普通对象"，具备\_\_proto\_\_，都是Function的实例
    + Function.prototype 本质是一个匿名空函数
    + Function.\_\_proto\_\_ === Function.prototype
    + Function.prototype上存在 call/apply/bind... 所有函数都可以找到这三个方法调用执行
    + Function是对象，他是Object的实例，Object是函数，它是Function的实例
    + 函数都有'name' 'length'
    + 箭头函数无prototype，不能 new 箭头函数
+ new Foo; new Foo();
    + 能否传递实参
    + 优先级 19 20 (obj.xxx 成员访问 20)
---
### 创建值
- 字面量
- 构造函数
    - 引用类型 上述两种无本质区别
    - 基本类型 
        + 字面量创造的是基本数据类型值，是所属类的实例
        + 构造函数方式创造引用数据类型，是所属类的实例
```js
let num1 = 10;
let num2 = new Number(10);
console.log(num1.toFixed(2)); //=>'10.00' 底层：默认先把10转换为对象格式，再调用Number.prototype的方法处理
console.log(num2.toFixed(2)); // =>'10.00' 基于__proto__查找调用
console.log(num1 + 20); // => 30 直接运算
console.log(num2 + 20); // => 30  底层：
                            // + 对象->数字/字符串
                            //          + 首先调用num2[Symbol.toPrimitive]
                            //          + 没有则调用num2.valueof()
                            //          + 没有则toString/Number
```
### this
- 事件绑定
- 函数执行
    - 自执行函数
    - 回调函数
    - ...
- 构造函数执行(new)
- 箭头函数中没有自己的this,所用this使用context中的this
```js
let obj = {
    name = 'Margin',
    age: 24,
    fn: function(){
        // this ->  obj
        return function (){
            // this -> window
            console.log(this);
        };
    }
};

let f = obj.fn();
f();
let obj = {
    name = 'Margin',
    age: 24,
    fn: function(){
        // this ->  obj
        return () => {
            // this -> obj
            console.log(this);
        };
    }
};
let f = obj.fn();
f();
f.call(100);//操作无效 没有this call/apply操作也是无效的

```
- 基于call/apply/bind改变函数this
    - Function.prototype => call/apply/bind
    ```js
    window.name = 'WINDOW';
    let obj ={
        name:'Margin',
        age:24
    };
    function fn()
    {
        console.log(this.name);
    }

    fn(); //this->window
    obj.fn();//error 

    fn.call(obj); //this->obj fn先基于__proto__找到Function.prototype.call，call执行时候，fn执行且fn的this变为第一个实参值
    fn.call();//this->window 严格模式 undefined
    fn.call(null);//this->window 严格模式 null [undefined与null相同]
    //--------
    fn.call(obj,10,20);
    fn.apply(obj,[10,20]);//传递数组参数的一项项
    ```
    ---
    - e.g. 获取数组最大值
    ```js
        let arr = [10, 30, 15, 36, 23];
        //排序
        arr.sort(function(a,b){
            return b - a;
        });
        let max = arr[0];

        //假设
        let max = arr[0];
        for (let i = 1; i < arr.legth;i++)
        {
            let item = arr[i];
            if (item > max)
            {
                max = item;
            }
        }
        //reduce
        let max = arr.reduce((result,item) => {
                return item > result ? item : result;
        });

        //Math.max
        Math.max(10,30,15,36,23); 
        //ES6
        let max = Math.max(...arr); 
        //apply的传递特点
        let max = Math.max.apply(null,arr);
        //字符串拼接
        let str = 'Math.max(${arr})';
        let max = eval(str);

    ```
    ---
    - e.g. 类数组集合转换为数组集合
    ```js
    function sum(...arr){
        // arguments :实参集合，类数组，不是Array
        let arr = [...arguments];

        let arr = Array.from(arguments);

        let arr = [];
        for (let i = 0; i<arguments.length; i++){
            let item = arguments[i];
            arr.push(item);
        }
        //let arr = [].slice.call(arguments);

        return arr.reduce((result, item) => item + result);
    }
    let total = sum(10,20,30,40);

    //浅克隆
    let ary = [10,20,30];
    let newAry = ary.slice();//不传递或传递0
    //重写slice
    Array.prototype.slice = function slice() {
        let arr = [];
        for(let i = 0; i<this.length; i++){
            let item = this[i];
            arr.push(item);
        }
        return arr;
    };

    // 如果让内置slice执行，this改为arguments，实现类数组克隆转换为数组
    // 1.slice执行
    // Array.prototype.slice()
    // [].slice()
    // 2.改变this
    // [].slice.call(arguments) 

    ```
    ---
    - e.g. 事件触发，定时器时间，执行对应方法改变this，给方法传递实参
    ```js
    //立即处理
    document.body.onclick = fn.call(obj, 10 ,20);
    setTimeout(fn.call(obj,10,20),1000);//不能实现，call/apply处理，函数立即执行，而不是等事件触发或定时器计时执行

    //预处理 [柯里化函数]
    //先绑定一个匿名函数, 事件触发或达到计时，先匿名函数执行，执行时把需要的fn执行，基于call/apply改变this和参数信息
    document.body.onclick = function(ev) {
        fn.call(obj, 10 , 20, ev);
    };
    setTimeout(function(){
        fn.call(obj,10,2j0);
    },1000);

    //bind，不立即执行，先处理this和参数
    document.body.onclick = fn.bind(obj, 10, 20);
    setTimeout(fn.bind(obj,10,20),1000);
    ```
    ---
    - e.g. call/apply/bind重写
    ```js
    //call思路： 需要执行的函数fn，和需要改变的this指向obj关联
    // obj.xxx = fn
    let obj = {
        name:'Margin',
        age: 24
        fn: fn
    };

    function fn(x,y) {
        console.log(this);
        return x + y;
    }
    // let result = fn.call(obj, 10, 20);
    let result = obj.fn(10,20);
    

    Function.prototype.call = function call(context, ...params) {
        // this -> fn 
        //context -> obj 要改变的this
        // params->[10,20] 要传递的实参
        context.xxx = this;
        let result = context.xxx(...params);
        delete context.xxx;
        return result;
    };
    // 优化： 临时设置context的属性不能和原始对象的属性冲突
    // 优化： context不传递或null，要改的this是window，
    // 优化： 要保证context是引用类型值
            // + number string boolean 可以 new n.constructor(n)
            // + symbol bigint 只能 Object(n)
    Function.prototype.call = function call(context, ...params) {
        // this -> fn 
        //context -> obj 要改变的this
        // params->[10,20] 要传递的实参
        context == null ? context = window :null;
        !/^(object|function)$/.test(typeof context) ? context = Object(context): null;
        let key = Symbol('KEY'),
            result;
        context[key] = this;
        result = context[key](...params);
        delete context[key];
        return result;
    };

    let obj = {
        name:'Margin',
        age: 24
    };

    function fn(x,y) {
        console.log(this);
        return x + y;
    }
    let result = fn.call(obj, 10, 20);
    ```
    ```js
    //原理：闭包 “柯里化”
    Function.prototype.bind = function bind(context, ...params) {
            // this -> fn 要执行的函数
            // context -> obj 要改的this
            // params -> [10,20] 要传的参数
            let that = this;
            return function proxy(...innerArgs) {
                params = params.concat(args);
                return that.call(context, ...params);
            };
    };

     let obj = {
        name:'Margin',
        age: 24
    };

    function fn(x,y,ev) {
        console.log(this,ev);
        return x + y;
    }

    document.body.onclick = fn.bind(obj, 10, 20);
    //document.body.onclick = function (ev) {
    //    fn.call(obj, 10, 20, ev);
    //};
    ```
