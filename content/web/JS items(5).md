---
title: "JavaScript 数据类型转换&变量提升"
date: 2020-09-21T10:02:39+08:00
draft: false
---
------
- 数据类型转换：  
  1. 其他类型=>Number  
      +  特定需要转换为Number的
         *  Number([val])
             - console.log(Number('')); // 0
             - console.log(Number('10'));// 10
             - console.log(Number('10px'));// NaN 出现非有效数字字符
             - console.log(Number(true));// 1
             - console.log(Number(false'));// 0
             - console.log(Number(null));// 0
             - console.log(Number(undefined));// NaN
             - console.log(Number(Symbol(10)));// error
             - console.log(Number(BigInt(10)));// 10
             - 对象=>数字，valueOf，没有原始值再toString，最后变为数字
         *  parseInt/parseFloat([val])
             - parseInt查找有效数字字符【符合radix进制】(遇到非有效字符停止)，把值先转换成字符串，一个都没有就是NaN（parseFloat多识别一个小数点）
             - (阿里面试题扩展) 
         *    e.g. 数字转换练习.png 
                 + NaN
                 + 0 
                 + false
                 + NaN
                 + 0
                 + false
                 + 12
                 + NaN
                 + true
                 + <font color="red">2.6number</font> //如果出现对象也会变成字符串拼接（对象=>字符串=>数字）
                 + false
                 + <font color="red">booleantrue</font>
      +  隐式转换
         *  isNaN([val])
         *  数学运算（特殊情况： +在字符串情况下表示拼接）
         *  在 == 中，有些值转换为数字再进行比较
         *  ...  
  2. 其他类型=>字符串  
      + 方法  
        * toString() : 普通对象{} =>[object Object] 检测数据类型
        * String()
      + 隐式转换
        * 加号运算，某一边字符串，表示拼接
        * 对象转换为数字，需要toString()转换为字符串再转换为数字
        * 基于alert/confirm/prompt/document.write等方式输出内容，先转换成字符串再输出
  3. 其他类型=>布尔
      + 方法
        * ! 转换成布尔值后取反
        * !! 转换成布尔类型
        * Boolean([val])
      + 隐式转换
        * 循环或条件判断，条件结果即布尔
        * ...
      + 规则：只有'0, NaN, null, undefined, 空字符串'五个会FALSE， 其余为TRUE
  4. ==的规则：
      + 【类型一样的点】
        * {}=={}:false 对象比较的时堆内存的地址
        * []==[]:false
        * NaN==NaN:false
      + 【类型不一样的转换规则】
        * null==undefined：true，但是 === 的结果是false，剩下null/undefined和其他任何类型都不相等
        * 字符串==对象 对象=>字符串
        * 两边类型不一致，都转化成数字再比较
  5. + 加号即使一边有字符串或对象，也不一定是拼接，（++i/i++/+i）
     + {} + 0  左边{}视为代码块 //+0 => 0
     + （{} + 0）"[object Object]0"
     + 0 +{} "0[object Object]"
  6. 对象数据类型=>数字/字符串
      - 首先查找对象的Symbol.toPrimitive属性
      - 不存在，调用valueOf获取原始值
      - 没有，则再调用toString&Number转换
  7. 特殊：
      - alert([value]) => 字符串
      - 模板字符串实现的是字符串拼接，对象会转换为字符串
      - 其余数学运算，对象=>数字
      - "=="比较，把对象转换成字符串或者数字
---
- 变量提升:当前context(可理解为代码解析的一个环节)
  + 全局context，基于var/function声明的变量，window设置对应的属性。
  + 当前dontext所有var/function关键字进行提前声明或定义
    - declare: ```var a;```
    - defined: ```a = 10;``` 
    - var只声明，function有定义
  + EC(G):
    - if 无论条件是否成立，都变量提升，新浏览器function只声明不定义。  
  + 代码块
            