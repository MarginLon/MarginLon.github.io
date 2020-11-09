---
title: "JavaScript AJAX相关"
date: 2020-11-02T22:02:39+08:00
draft: false
---
# Content
- 前后端分离开发中的AJAX和HTTP
    - AJAX基础
    - AXIOS
---
## AJAX基础
- AJAX解决网页异步刷新
    - 同步刷新
    - 异步刷新
        1. 浏览器可以从服务器同时请求多项内容；
        2. 浏览器请求返回的速度会快得多；
        3. 只有页面中真正改变的部分得到更新；
        4. 能够减少服务器数据流量；
        5. 用户可以在页面更新的同时继续工作；
        6. 有些改变无须与服务器往返通信就可以处理。
- XML / JSON
    - [AJAX实例 GET/POST](https://github.com/MarginLon/CSS_JS_Repos/blob/main/JS/ajax%E7%9B%B8%E5%85%B3/ajaxOperation.js)
    - AJAX状态 
        - xhr.readyState  
        0. UNSENT 未发送,默认  
        1. OPENED 已打开 执行了OPEN
        2. HEADERS_RECEIVED: 服务器已经返回响应头的信息
            - 响应头：Date 返回时的服务器时间 先返回后主体慢慢返回
            - 响应主体：客户端需要的信息
        3. LOADING 主体正在加载返回
        4. DONE 主体信息返回
    - HTTP网络状态码 - xhr.status
        - 以2开始 200 服务正常返回数据（数据是否为想要的不一定 业务流程：code标识表示业务逻辑上的成功失败）
        - 以3开始 304 读取的是协商缓存的数据 301永久重定向(一般用于域名的转移) 302/307 临时转移/重定向（一般用于服务器的负载均衡）
        - 以4开始 400 请求参数有误 401 无权访问 404 地址错误 403 服务器拒绝执行 [一般都是客户端问题]
        - 以5开头 500 服务器发生未知错误 503 超负荷 [一般是服务器问题]
    - XHR属性方法
---
## AXIOS
- 基础见纸笔
       
