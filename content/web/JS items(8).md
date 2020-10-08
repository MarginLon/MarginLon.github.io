---
title: "JavaScript 闭包进阶"
date: 2020-09-26T18:02:39+08:00
draft: false
---
# 闭包进阶
- 闭包
    + 闭包概念    
        - 保护私有context不被干扰
        - 保存
        - 弊端：性能
    + 应用1：循环事件绑定或者循环操作中对于闭包的应用
    ```js
    for (var i = 0; i < 3; i++)
    {
        setTimeout(()=>{
            console.log(i);
        },(i + 1) * 1000);
    }
    ```
  ```js
    for (var i = 0; i < 3; i++)
    {
        (function(i){
          setTimeout(()=>{
            console.log(i);
          },(i + 1) * 1000);
        })(i);
        
    }
    ```
    ```js
    // let xxx = proxy(0) ->
    const proxy = i =>{
        return ()=> {
          console.log(i);  
        };
    };
    for (var i = 0; i < 3; i++)
    {
        setTimeout(proxy(i), (i + 1) * 1000);
    }
    ```
    ```js
    for (let i = 0; i < 3; i++)
    {
        setTimeout(()=>{
            console.log(i);
        },(i + 1) * 1000);
    }
    ```
    + 应用2：基于闭包实现早期的模块化(单例)
        - 解决无对象类型值的“全局变量的污染”
            + 解决变量冲突：闭包机制 => 保护
            + 用对象分组，命名空间 => 单例模式
            + 高级单例
                - 功能拆分
                - 模块独立
    + 应用3：惰性函数（思想）
        - 获取元素样式
            - window.getComputedStyle([元素对象])
            - [元素对象].currentStyle
            ```js
            function get_css(element,attr){
                if ('getComputedStyle' in window) {
                    get_css = function (element, attr) {
                        return window.getComputedStyle(element)[attr];
                    };
                }
                else {
                     get_css = function (element, attr) {
                        return element.currentStyle[attr];
                };
               }
               return get_css(element, attr);
            }
            ```
    + 应用4：柯里化函数
```js
let res = fn(1,2)(3);
console.log(res);//=>6 1+2+3

//ToDo
function fn() {
    let outerArgs = Array.from(arguments); 
    
    return function annoymous(){
        let innerArgs = Array.from(arguments);

        let params = outerArgs.concat(innerArgs);
        return params.reduce(function(result, item){
            return result + item;
        });
    };
}

// ES6 ToDo

//数组 reduce
//     + arr.reduce([function])
let arr = [10, 20, 30, 40];
let result = arr.reduce(function (result, item, index){
        console.log(result,item,index);
        return result + item;
});
// 重构 reduce
function reduce(arr, callback, initValue) {
    let result = initValue,
        i = 0;
    if(typeof result=="undefined"){
        result = arr[0];
        i = 1;
    }

}
let arr = [10, 20, 30, 40];
let result = reduce(arr, function(result, item, index){
    return result + item;
});
console.log(result);

```
---
+ 应用5：compose函数
```js
/* 
    在函数式编程当中有一个很重要的概念就是函数组合， 实际上就是把处理数据的函数像管道一样连接起来， 然后让数据穿过管道得到最终的结果。 例如：
    const add1 = (x) => x + 1;
    const mul3 = (x) => x * 3;
    const div2 = (x) => x / 2;
    div2(mul3(add1(add1(0)))); //=>3
​
    而这样的写法可读性明显太差了，我们可以构建一个compose函数，它接受任意多个函数作为参数（这些函数都只接受一个参数），然后compose返回的也是一个函数，达到以下的效果：
    const operate = compose(div2, mul3, add1, add1)
    operate(0) //=>相当于div2(mul3(add1(add1(0)))) 
    operate(2) //=>相当于div2(mul3(add1(add1(2))))
​
    简而言之：compose可以把类似于f(g(h(x)))这种写法简化成compose(f, g, h)(x)，请你完成 compose函数的编写 
*/
 const compose = (...funcs) => {
     return x => {
        return funcs.reduceRight((result, item) =>{
            //result->x item->add1
            //result->add1(x) item->add1
            return item(result);
        }, x);
     };
 };
```
+ 应用6：JQ
    * 暂空
+ 闭包：
    - 简述你对闭包的理解，以及其优缺点？
1. 闭包概念
    + 堆栈内存(ECStack\EC\VO\AO\SCOPE\SCOPE-CHAIN\HEAP)
    + GC垃圾回收机制
2. 作用
     + 总述作用：保存/保护    优缺点
     + 实战中的应用（循环事件绑定、防抖和截流....）
     + 进阶函数
     + 源码分析
     + 自主封装
     + ....
3. 自己对他的认知和理解（夹杂自己的思想）

4. 不要啰嗦，不要深入展开，回答全面是为了引导面试官的兴趣，让其根据你的回答再具体的细问...
5. 回答的时候多加一些助词，例如：在我之前的项目开发中....
6. 不要太学术化，像讲故事一样，通俗易懂 言简意骇的讲出来即可

# 闭包相关
```js
function fn(){
    //存储函数本身，方便递归调用
    console.log(arguments.callee);
}
fn();
//e.g.
(function(i){
    if (i>= 3) return;
    console.log(i);
    arguments.callee(++i);
})(1);
//严格模式，匿名函数的递归
//匿名函数具名化
// 名字不能在外部使用，可以在当前函数私有context使用，代表函数本身
// 值不允许修改 但当前的名字被context其他变量声明过，名字是私有变量，和具名化函数无关，值可以修改。
(function b(i){
    if (i>= 3) return;
    console.log(i);
    b(++i);
})(1);
```