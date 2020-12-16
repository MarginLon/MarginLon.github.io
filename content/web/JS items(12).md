---
title: "JavaScript 原型与原型链"
date: 2020-10-10T18:02:39+08:00
draft: false
---
### 原型prototype 原型链__proto__

---
### new相关
```js
function Dog(name) {
    this.name = name;
}
Dog.prototype.bark = function () {
    console.log('wangwang');
}
Dog.prototype.sayName = function () {
    console.log('my name is ' + this.name);
}
/*
let sanmao = new Dog('三毛');
sanmao.sayName();
sanmao.bark();
*/
function _new(Ctor,...params) {
    // ctor->Dog params->['三毛']
    //1.创建一个实例对象 
    let obj = {};
    obj.__proto__ = Ctor.prototype;
    //__proto__ IE禁止使用
    // Object.create([obj]): 创建一个空对象，把[obj]作为当前空对象的__proto__指向
        // - [obj]可以是null或一个对象
        // - null，则当前空对象不具备__proto__属性，即不属于任何类的实例
    // let obj = Object.create(Ctor.prototype);

    //2.构造函数当作普通函数执行[私有context，作用域链，初始this，形参赋值]
    // this->指向创建的实例对象 基于call方法改变即可
    let result = Ctor.call(obj, ...params);

    //3.观察函数执行的返回值，如果没有返回值或返回基本类型，默认返回实例对象，否则返回自己的返回值
    if(/^(object|function)$/.test(typeof result)) return result;
    return obj;
}
let sanmao = _new(Dog, '三毛');
sanmao.bark();
sanmao.sayName();
console.log(sanmao instanceof Dog);


//兼容版本
Object.create = function (pro) {
    function Proxy(){}
    Proxy.prototype = pro;
    return new Proxy;
};

function _new(Ctor) {
    //获取除第一个以外的实参，数组形式保存
    var params = [].slice.call(arguments, 1);
    
    var obj = Object.create(Ctor.prototype);
    //基于apply改变this，也可以把数组中的每一项传递给函数
    var result = Ctor.apply(obj, params);
    if(/^(object|function)$/.test(typeof result)) return result;
    return obj;
}

var sanmao = _new(Dog, '三毛');
sanmao.bark();
sanmao.sayName();
console.log(sanmao instanceof Dog);
```
---
### 扩展内置类原型方法
```js
//去重后排序
Array.prototype.unique = function unique(){
    //this -> arr
    let result = new Set(this);
    result = Array.from(result);
    return result;
};

let arr = [1, 2 ,3, 2, 3, 4, 2, 3, 4, 2, 1, 2, 3, 4, 5, 3, 4];
let result = arr.unique().sort((a,b) => a-b);





function unique(arr) {
    // ...
    let result = new Set(arr);
    result = Array.from(result);
    return result;
}

let arr = [1, 2 ,3, 2, 3, 4, 2, 3, 4, 2, 1, 2, 3, 4, 5, 3, 4];
let result = unique(arr);

//let result = arr.sort((a,b) => a-b);
console.log(arr,result);
```