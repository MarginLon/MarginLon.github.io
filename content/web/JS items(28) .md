---
title: "JavaScript 复习（三）"
date: 2020-11-10T22:02:39+08:00
draft: false
---
# Content
- DOM相关
- 数组
---
## DOM相关
- DOM document object model 文档对象模型
    * 获取DOM元素
        ```js
        document.getElementById([ID])
        document.body 
        document.getElementsByTagName([标签名])
        ```
---
## 数组
- arr.length-1 最后一项的索引
    * delete arr[0]; // delete length不变 
- 增删改
    * push  arr[arr.length] = x; 数组末尾追加新项
    * pop   arr.length--; //删除最后一项
    * shift
    * unshift
    * splice
- 查找拼接
    * slice
    * concat
- toString
    * toString
    * join
- 验证包含
    - indexOf / lastIndexOf
    - includes
- 排序
    - reverse
    - sort
- 迭代
    - forEach
    - map
