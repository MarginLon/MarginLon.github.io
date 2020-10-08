---
title: "JavaScript 数据类型&底层机制"
date: 2020-09-16T22:43:39+08:00
draft: false
---
# JavaScript

##  数据类型
+ 类型小结
  - 基本数据类型
     + number
        - NaN
          * `isNaN()`
          * `Object.is(NaN, NaN)`
        - Infinity
    + string
    + boolean
    + null
    + undefined
    + symbol
        - static Symbol
        - Symbol.prototype
        - 给对象设置唯一的属性
        - 在vuex/redux中做行为派发的时候，统一管理派发的行为标识，标识的值可以是唯一值。
        - Symbol.hasInstance
        - Symbol.toPrimitive ：
        - Symbol.toStringTag
        - Symbol.iterator
        - Symbol.isConcatSpreadable
        - Symbol.match
        - ...
    + bigint
  - 引用数据类型
    + object
        - 普通对象
        - 数组对象
        - 正则对象
        - 日期对象
        - JSON
        - Set
        - Map
        - ...
    + function
        - 普通函数
        - 构造函数
        - 箭头函数
        - 生成器函数
        - ...
+ typeof原理：
  - [typeof null] => object，所有数据类型是二进制存储，null -> 000000，只要是对象就以000开始 typeof检测按照存储的二进制的值。
+ 浏览器：
  - 开辟一个栈内存=>ECStack=>EC(G)=>VO(G)
  - var [变量] = [值]
     * 1.先创建值
         + 基本：储存在栈
         + 引用：开辟一个堆Heap
     * 2.声明变量
         + 存放到当前context的变量对象中（VO/AO)
     * 3.defined
         + var n; 默认值undefined
  - 引用
     * 1.开辟一个单独Heap
     * 2.16进制地址
     * 3.对象中的键值对分别储存在堆中
     * 4.地址进栈，供变量调用
  - GO
     * window
