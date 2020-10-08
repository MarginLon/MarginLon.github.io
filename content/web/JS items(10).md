---
title: "JavaScript 复习（一）"
date: 2020-10-01T18:02:39+08:00
draft: false
---
### 技术论坛
- [掘金](https://juejin.im/)
- [简书](https://www.jianshu.com/)
- [MDN](https://developer.mozilla.org/zh-CN/)
- [StackOverflow](https://stackoverflow.com/)
- [思否](https://segmentfault.com/)
- [百度](http://fex.baidu.com/)
- [腾讯](http://alloyteam.com/)
- [75](https://75.team/)
- [凹凸](https://aotu.io/)
---
### 浏览器内核
1. 谷歌webkit(V8引擎)
    - chrome
    - safari
    - 国产
2. Gecko
    - firefox
3. Trident
    - IE
---
### 开发者工具
- Elements 结构，样式 
- Console(直接F12打开) 调试，报错，测试
- Network HTTP请求，前后端交互等
- Sources 源代码
- Application 本地存储的信息(Cookie.../图片)
---
### JS
* ECMAScript
* DOM
* BOM
---
###  关键字与保留字
- 关键字
    * break do in typeof 
    * case else instaceof var
    * catch export new void
    * class extends return while
    * const finally super with
    * continue for switch yield
    * debugger function this
    * default if throw
    * delete import try
- 保留字
    * enum
    * 严格模式:
        - implements package public
        - interfave protected static
        - let private
    * 代码模块:
        - await
---
### 输出方式
- console
    - console.log() 可多值
    - console.dir() 单值，详细
    - console.table()
    - console.time()/timeEnd()
    - console.warn()
- window框
    - alert() toString
    - confirm()
    - prompt()
- 容器插入
    - document.write 页面 toString 
    - innerHTML / innerText 容器 toString (document.getElementById)
        - 覆盖原文，+=不覆盖
    - value 文本框
---
### number
* NaN isNaN()
    - ```isNaN("12")  // 非number => number 检测```
* 转换
    - Number([value]) 
        + (isNaN的方式) 
        + 字符串：出现非有效数字即为NaN
        + null => 0 undefined => NaN Symbol => error function => NaN
        + 对象  =>字符串 =>数字
            - 普通
            - 数组
            - 其余 NaN
    - parseInt([value])/parseFloat([value])
        - (其他类型) => 字符串 => 数字
        - 查找有效数字字符【符合radix进制】(遇到非有效字符停止)，把值先转换成字符串，一个都没有就是NaN（parseFloat多识别一个小数点）
    - ==的规则：
        + 【类型一样的点】
            * {}=={}:false 对象比较的是堆内存的地址
            * []==[]:false
            * NaN==NaN:false
        + 【类型不一样的转换规则】
            * null==undefined：true，但是 === 的结果是false，剩下null/undefined和其他任何类型都不相等
            * 字符串==对象 对象=>字符串
            * 两边类型不一致，都转化成数字再比较
---
### string
*  其他类型=>字符串  
      + 方法  
        * [val].toString() 
        * String([val])
            - : 普通对象{} =>[object Object] 检测数据类型
            - : 数组对象{} =>第一项, 第二项, 第三项...
      + 隐式转换
        * 加号运算，某一边字符串，表示拼接
            - 加号即使一边有字符串或对象，也不一定是拼接，（++i/i++/+i）
                + {} + 0  左边{}视为代码块 //+0 => 0
                + ({} + 0) "[object Object]0"
                + 0 +{} "0[object Object]"  (Ps:{}转换为数字时，先转为字符串而变成了拼接)
        * 对象转换为数字，需要toString()转换为字符串再转换为数字
        * 基于alert/confirm/prompt/document.write等方式输出内容，先转换成字符串再输出
      + ES6模板字符串：  
        ```let result = `${year}年${month}月${day}日 ${hours}:${minutes}:${seconds}`; ```   
---
### boolean
* 其他类型=>布尔
    + 方法
        * ! 转换成布尔值后取反
        * !! 转换成布尔类型
        * Boolean([val])
      + 隐式转换
        * 循环或条件判断，条件结果即布尔
        * ...
      + 规则：只有'0, NaN, null, undefined, 空字符串'五个会FALSE， 其余为TRUE
---
### object
* 特点:
    1. 键值对(key:value 属性名:属性值) key不可以是引用类型，value可以
    2. obj.attr = value / obj['attr'] = value
    3. Object.keys(obj) 
    4. delete
        - Fake: 属性名存在 属性值为空 ```obj.attr = null```
        - True: 属性不存在```delete obj.attr```
* 对象数据类型=>数字/字符串
    - 首先查找对象的Symbol.toPrimitive属性
    - 不存在，调用valueOf获取原始值
    - 没有，则再调用toString&Number转换
---
### 数据类型检测
- typeof [val]
    * result： string
    * 特殊：
        - typeof null //object
- [example] instanceof [class]
- [example].constructor===[class]
- Object.prototype.toString.call([val]) 







