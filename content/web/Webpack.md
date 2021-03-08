---
title: "Webpack"
date: 2020-11-17T15:25:39+08:00
draft: false
---
- [- WebPack](#--webpack)
- [前端工程化](#前端工程化)
- [WebPack](#webpack)
---
## 前端工程化
- 模块化
    - ES6 Module
    - server NodeJS CommonJS
    - 浏览器 Require.js AMD
- 组件化
- 规范化
- 自动化(构建，部署，测试)
## WebPack    
- 功能
    1. 代码转换
    2. 文件优化
    3. 代码分割
    4. 模块合并
    5. 自动刷新
    6. 自动发布
- Install
    ```Shell
    npm init -y  // 初始化package.json

    npm install -g webpack webpack-cli // 全局安装

    npm install --save-dev webpack webpack-cli// 项目目录安装
    ```
- entry
    ```webpack
    module.exports = {
        entry: './path/to/my/entry/file.js'};
    ```
 