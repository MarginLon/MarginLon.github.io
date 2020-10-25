---
title: "JavaScript Iterator"
date: 2020-10-25T20:02:39+08:00
draft: false
---
# Content
- Iterator
---
# Iterator
- Iterator是一种机制，遍历各种不同的数据，依次处理成员
    - next方法遍历
    - 每次遍历返回一个对象 { done:false, value: xxx}
        + done：记录是否完成
        + value：当前遍历的结果

- 拥有Symbol.iterator，基于for of可遍历
    - 对象默认不具备
    - 数组
    - 部分类数组 arguments/ Nodelist/ HTMLCollection...
    - String
    - Set
    - Map
    - generator object
    - ...(展开运算符)
- [实例](https://github.com/MarginLon/CSS_JS_Repos/blob/main/JS/iterator.js)
- [生成器对象](https://github.com/MarginLon/CSS_JS_Repos/blob/main/JS/generator.js) generator function返回
```js
function* func(){

}
let iterator = func();
// iterator.__proto__ === func.prototype (Generator)
console.log(iterator instanceof func) //=> true;
new func(); //Error func is not a constructor

// GeneratorFunction
    // + next
    // + return
    // + throw 
```
