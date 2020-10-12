---
title: "HTML 回顾"
date: 2020-10-12T10:02:39+08:00
draft: false
---
### HTTP HyperText Transfer Protocol
- HTTP 状态码
    + 200 ：成功。
    + 400 ：客户端请求有语法错误，服务器端不能理解。
    + 401 ：该请求可能未经过授权。
    + 403 ：服务器端收到该请求，但是拒绝为它提供服务，可能是没有权限等等。
    + 404 ：该资源没找到。
    + 500 ：服务器端发生了一个不可预知的错误。
    + 503 ：服务器端当前还不能处理客户端的这个请求，可能过段时间之后才能恢复正常。
### Web Storage
+ cookie   
    1. 大小：4kb
    2. 带宽：访问消耗
    3. 安全风险
+ Web Storage
    1. 存储大小：5~10MB
    2. 不发送至服务器
    3. 更丰富的接口
    4. localStorage,sessionStorage
+ localStorage
    - 持久化的本地存储，不手动删除不会过期
    - 存储：localStorage.setItem(key,value);
    - 读取：localStorage.getItem(key);
    - 删除：localStorage.removeItem(key); / localStorage.clear();