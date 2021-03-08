---
title: "JavaScript 面试题"
date: 2020-09-21T10:02:39+08:00
draft: false
---
- [面试题](#面试题)
  - [7. hasPubProperty](#7-haspubproperty)
- [技巧](#技巧)
# 面试题

1. 堆栈内存
![例1堆栈内存](https://github.com/MarginLon/MarginPostImage/blob/master/%E4%BE%8B1%E5%A0%86%E6%A0%88%E5%86%85%E5%AD%98.png?raw=true)
<br/>

2. [闭包三题](https://github.com/MarginLon/CSS_JS_Repos/blob/main/JS/%E5%B0%8F%E7%BB%83%E4%B9%A0/e2.js)

<br/>

![例3闭包相关](https://github.com/MarginLon/MarginPostImage/blob/master/%E4%BE%8B3%E9%97%AD%E5%8C%85%E7%9B%B8%E5%85%B3.png?raw=true)
<br/>

![例4闭包相关](https://github.com/MarginLon/MarginPostImage/blob/master/%E4%BE%8B4%E9%97%AD%E5%8C%85%E7%9B%B8%E5%85%B3.png?raw=true)
<br/>

3. [5个怪异行为](https://github.com/MarginLon/CSS_JS_Repos/blob/main/JS/%E5%B0%8F%E7%BB%83%E4%B9%A0/5%E4%B8%AA%E6%80%AA%E5%BC%82%E8%A1%8C%E4%B8%BA.js)
<br/>

4. 所有的类都是函数数据类型,所有的实例都是对象类型[但是有特殊性] 
   ```js
   console.log(typeof Object); //=>"function"
   console.log(typeof Array);  //=>"function"

   function sum(){} // => typeof sum ==="function"
   let arr = [] // => Array实例 -> 数组，对象
   let n = 10;
   let m = new Number(10);
   m.toFixed(2);  // '10.00'
   n.toFixed(2);  // '10.00' 转为new Number(10)
   n-10; // 0
   m-10; // 0  浏览器把对象转成数字
   ```


5. this  
    ```js
    var x = 3,
        obj = {x:5};
    obj.fn = (function(){
      this.x *= ++x;
      return function(y){
          this.x *= (++x)+y;
          console.log(x); 
      }
    })();
    var fn = obj.fn;
    obj.fn(6);
    fn(4);
    console.log(obj.x, x); 
    // 13
    // 234
    // 95 234
    // this.x *= (++x)+y; 后面是整体
    ```
6. Hoisting
    ```js
    // 1. 
    fn(); // 5
    function fn(){console.log(1);}
    fn(); // 5 
    function fn(){console.log(2);}
    fn(); // 5
    var fn = function(){console.log(3);}
    fn(); // 3
    function fn(){console.log(4);}
    fn(); // 3
    function fn(){console.log(5);}
    fn(); // 3

    // 2. 
    var foo = 1;
    function bar() {
      if (!foo){
        var foo = 10;
      }
      console.log(foo); // 10
    }
    bar();
    ```
  7. hasPubProperty
---
# 技巧
1. 不“背书”   [场景， low一点]
2. 不要只看问题表面，在有限时间内，精简语言更多表达自己  [引导面试官问一些自己擅长或者精心准备的]
  - 基础/理论
  - 实战
  - Bigger：看源码，造轮子
  - 非技术类


3. “闭包” 5分钟
  - 过渡语
  - 抛理论：浏览器渲染执行 堆栈内存 GC垃圾回收机制 保护保存
  - 实战：举1~2个例子
  - 源码
  - 造轮子
  - 总结
  - 谦虚反问