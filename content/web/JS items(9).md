---
title: "JavaScript OOP"
date: 2020-09-29T20:02:39+08:00
draft: false
---
# 面向对象
- OOP 面向对象
    + HTML&CSS 标记语言
    + less/sass/stylus：CSS预编译，CSS=>面向对象，需要编译成CSS在浏览器渲染。
    + 对象，类，实例：
        - 对象：泛指
        - 类：细分“对象”，大类和小类
            - 封装，继承，多态
                - 封装：功能的代码封装，低耦合高内聚
                - 继承：子承父
                - 多态：函数重载（名字相同，传参的个数或类型不同，JS中不存在），重写（子写父的新方法）
        - 实例：某个类中具体事物
            + 独有特征
            + 共有特征
    + JS
        - 内置类
        - 自定义类（类都是“函数数据类型”）
            + 函数执行的时候基于new执行即可“构造函数执行”
                - 构造函数 VS 普通函数
                    1. 构造函数执行，也形成私有context
                    2. 创建context后，浏览器默认创建一个对象实例，把当前Fn函数当作类（”构造函数“）
                    3. 初始this，把this指向当前的实例对象。
                    4. 执行完，return时
                        - 没有return/return 基本数据类型值，浏览器默认把创建的实例对象返回
                        - return 引用类型，返回自己的。
            + Fn VS Fn()：
                * Fn代表函数本身（堆内存），Fn()函数执行，获取返回值。
            + new Fn VS new Fn()：
                * 执行，第一个不传递实参，第二个传递实参。
            + 检测一个属性是否为当前对象的成员
                - 属性名 in 对象：无论公私有，有就是true
                - 对象.hasOwnProperty(属性名)：只有私有true
            + 基于"for..in"循环遍历
                + 优先遍历数字属性
                + 不会遍历到Symbol
                + 会把自己扩展到“类原型”上的公共属性方法也遍历 [可枚举的] ```if(!obj.hasOwnProperty(key)) break;//遍历到公共属性，停止遍历```
                + Object.keys(obj):非Symbol私有属性 [数组]
                + Object.getOwnPropertyNames(obj): 同上
                + Object.getOwnPropertySymbols(obj):Symbol私有属性 [数组]
                ```js
                let keys = [...Object.keys(obj),...Object.getOwnPropertySymbols(obj)];
                keys.forEach(key=> {
                            console.log(`属性名:$(),属性值:$()`);.
                });
                ```
                
- POP 面向过程
