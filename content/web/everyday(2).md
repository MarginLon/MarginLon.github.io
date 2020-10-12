---
title: "JavaScript 每日一题（二）"
date: 2020-09-26T18:02:39+08:00
draft: false
---
# 每日一题（二）
- JS的垃圾回收机制
    + 暂空
- 运行结果？
    + 0
    + undefined
    + <span style="color:red">3</span>
    + error
```js
console.log([...[..."..."]].length);
//[".",".","."] 外面又把它扩展到一个新数组，长度仍为3
```
- 运行结果？
    + 1
    + <span style="color:red">undefined</span>

```js
const obj = {
    a:1,
};
const func = () => {
    console.log(this.a);
};
func.call(obj);
//箭头函数的作用域定义时确定，call无法改变this指向， 箭头函数指向window对象
```