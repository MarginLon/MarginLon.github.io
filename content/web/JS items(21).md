---
title: "JavaScript 同步异步编程和事件循环"
date: 2020-10-24T20:02:39+08:00
draft: false
---
# Content
- 同步异步编程和事件循环
---
# 同步异步编程和事件循环
- 进程和线程
    - 1个进程包含多个线程
    - 进程：程序（一个页面）
    - 线程：一个线程处理一个任务
    - 浏览器多线程：
        - HTTP网络线程：资源文件加载
        - GUI渲染线程：页面自上而下渲染，绘制页面
        - JS渲染线程：用于渲染JS代码
    - JS单线程：浏览器只开辟一个线程渲染JS，JS本质都是同步的。
    - JS异步：基于多线程结合EventLoop事件循环，构建异步效果。
        - 定时器:设置定时器是同步的过程，而间隔[Interval]后触发绑定方法执行是异步的
- ECstack（栈内存）
    - 代码执行”JS渲染线程“自上而下解析执行，即【主线程】。
- Event Queue 事件队列 【等待任务队列】
    - 浏览器加载页面产生，存储待执行的任务，<span style="color:red">优先级队列</span>
        - 微任务队列：（先找）如果微任务队列没有，则在去宏任务队列中查找
        - 宏任务队列：一般按照谁先到达执行条件
        
    - 代码执行过程中，只要创建一个异步的任务，则会进入EventQueue
        - 任务放置完成，不需要等待，主线程继续向下渲染同步的代码
        - 定时器或者事件绑定等创建的异步任务，放置到事件队列，浏览器开辟新线程 => 监听线程：监听定时器是否到达指定时间
        - <span style="color:red">同步任务执行完</span>，主线程空闲，才会看EQ中的等待任务，<span style="color:red">依次拿出来放置到栈内存，让主线程执行</span>，此任务执行完，主线程再次空闲，再去EQ中查找，即为<span style="color:red">EventLoop事件循环机制.</span>
- js渲染线程
    - 词法分析
    - 自上而下的代码分析为一个个任务，放在宏任务队列，词法分析完成，再执行。
- 异步任务
    * 宏任务
        - 定时器
        - 事件绑定
        - AJAX/FETCH等创建的网络请求
    * 微任务
        - Promise:then/resolve(reject)通知注册的onfulfilled/onrejected方法执行
        - async/await 
            - async：让一个函数返回Promise实例，默认成功，除非本身就是返回一个Promise实例，结果则以返回实例为主
            - await:
                - 函数中如果需要使用await，则所在的函数必须基于async修饰
                - await可以使异步的编程模拟出同步的效果
                + await后面一般会放置一个Promise实例（其他正常值也是可以的）
                + 等待Promise状态为成功后，获取成功的结果，并且执行函数体中await下面的代码
                + ```js
                    async function fn() {
                    // 先执行handel，返回一个Promise实例
                    //   + 接下来等待，等待Promise实例变成成功态「再此期间，函数体中await下面代码都不会执行」
                    //   + 当状态变为成功，把成功的结果给result，继续执行下面代码
                    let result = await handle();
                    console.log(result); //=>1S后输出'OK'

                    // 虽然await后面放置的是一个10,肯定算是成功的，但是await下面代码也不是立即执行的，也需要等，等待同步任务执行完
                    //  => await本身是异步的(await下面的代码，需要等到await后面的Promise实例「不是实例也会当做实例来处理」变为成功，才会执行后面的代码)，模拟出来一个类似于同步的效果
                    let n = await 10;
                    console.log(n); //=>10

                    // 如果await后面的Promise实例是失败的，则不再处理之前存放的微任务（也就是下面的代码）：因为没处理失败，浏览器抛出异常 Uncaught (in promise) NO  =>用try catch 解决
                    try {
                        let m = await Promise.reject('NO');
                        console.log(m);
                    } catch (err) {

                    }
                    }
                    fn(); 
                  ```
-[实例](https://github.com/MarginLon/CSS_JS_Repos/blob/main/JS/eventQueue.js)
