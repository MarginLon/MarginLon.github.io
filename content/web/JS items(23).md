---
title: "JavaScript 设计模式"
date: 2020-10-25T20:02:39+08:00
draft: false
---
# Content
- 单例设计模式
- Promise
- 工厂设计模式
- 发布订阅设计模式
---
# 单例设计模式
---
# Promise
---
# 工厂设计模式
---
# 发布订阅设计模式
- 观察者模式:level up！
- 发布一个计划，并向计划中订阅一个个方法
- 当触发某个事件或到达某个阶段，通知计划中订阅的方法，按顺序依次执行

- [第一版](https://github.com/MarginLon/CSS_JS_Repos/blob/main/JS/subscribe1.js): 不支持自定义事件，且一个页面只有一个事件池 [单例设计模式]
- [第二版](https://github.com/MarginLon/CSS_JS_Repos/blob/main/JS/subscribe2.js): 支持自定义事件，一个页面只有一个事件池
- [第三版](https://github.com/MarginLon/CSS_JS_Repos/blob/main/JS/subscribe3.js): 多个事件池，事件池独立，也有共同方法 on/off/fire