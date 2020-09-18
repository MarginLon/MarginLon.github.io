---
title: "JavaScript 函数底层机制"
date: 2020-09-18T10:02:39+08:00
draft: false
---
# 函数底层机制  
![函数底层机制](https://github.com/MarginLon/MarginPostImage/blob/master/%E5%87%BD%E6%95%B0%E5%BA%95%E5%B1%82%E6%9C%BA%E5%88%B6.png?raw=true)

- 创建函数
    + 声明一个变量存储值
    + 函数函数名
    + 开辟堆内存
        * 对象堆：键值对
        * 函数堆：存储代码，字符串形式
    + 创建函数的时候就声明了作用域scope
- 执行函数:
    + 形成一个全新的私有context =>  EC(FN1)
    + AO(FN1)进栈 &emsp;（AO:ActiveObject）
    + 初始化作用域链[Scope-chain]
        - <当前自己的私有context，函数的作用域> => 链的右侧是当前context的“上级”context
    + 初始化this
    + 初始化arguments
    + 形参赋值：当前上下文声明一个形参变量，并传递实参值
    + 变量提升
    + 代码执行
        - 变量：私有只操作自己，和外界无关；如果不是自己私有，则基于chain向context查找，是否为上级私有，如果不是，继续向上查找，直到EC(G)，即<span style="color:red">作用域链查找机制</span>
    + 出栈
------
# 其他
![其他](https://github.com/MarginLon/MarginPostImage/blob/master/%E9%87%8A%E6%94%BE%E6%9C%BA%E5%88%B6.png?raw=true)
- GC：浏览器的垃圾回收机制（内存释放）
    * 栈内存：
        + 加载内面，形成全局context，只有页面关闭后，全局context释放
        + 函数执行私有context，进栈执行；函数中代码执行完成，大部分情况，出栈释放。
    * 堆内存
        + （谷歌）：查找引用
            - 浏览器在空闲或指定时间，查看所有堆内存，把没有被任何东西占用的堆内存释放。
        + （IE）：引用计数
            - 创建了堆内存，被占用一次，则浏览器计数+1，取消占用计数-1，计数=0释放内存； => 某些情况导致计数混乱，出现“内存泄漏”
    * 释放内存：
        + x=null => 手动取消占用
- EC(FN)：
    * 开辟的某个堆内存，被当前EC(FN)外的变量占用，此时当前context即EC(FN)不能被出栈释放
    * 闭包：
        - 私有变量受到context保护
        - 有可能形成不被释放的context，私有变量和一些值被保存，可供下级context中调取使用。
