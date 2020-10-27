---
title: "JavaScript 事件绑定相关"
date: 2020-10-27T20:02:39+08:00
draft: false
---
# Content
- 事件
- 事件对象和阻止默认行为
- 事件的传播机制
- mouseover和mouseenter
---
# 事件
1. 事件:浏览器赋予元素的默认行为，无论是否绑定方法，某些行为触发，相关事件也会触发。
    - [事件参考](https://developer.mozilla.org/zh-CN/docs/Web/Events)
    - 鼠标事件
        - click 点击事件(PC：频繁点击N次，触发N次) 单击事件(移动端：300ms内没有第二次点击，算作单击事件，即300ms延迟)
        - dblclick 双击事件
        - contextmenu 鼠标右键点击触发
        - mousedown 鼠标按下 
        - mouseup 鼠标抬起 
        - mousemove 鼠标移动
        - mouseover 鼠标经过
        - mouseout 鼠标滑出
        - mouseenter 鼠标进入
        - mouseleave 鼠标离开
        - wheel 滚轮滚动
    - 键盘事件
        - keydown 键盘按下
        - keyup 键盘抬起
        - keypress 长按（除Fn shift Capslock）
    - 触屏事件
        - [touch event 单手指]
            - touchstart 手指按下
            - touchmove 手指移动
            - touchend 手指松开
            - touchcancel 意外取消
        - [gesture event 多手指] 
    - 网络事件
        - online
        - offline
    - 表单事件
        - focus 获取焦点
        - blur 失去焦点
        - submit 表单提交（表单元素都包含在form中，并且点击的按钮是submit）
        - reset 表单重置（表单元素都包含在form中，并且点击的按钮是reset）
        - select 下拉框内容选中
        - change 内容改变
        - input (移动端常用) 监控文本框内容随着输入改变而触发
    - 资源事件
        - load 加载成功(window.onload/ img.onload)
        - error 加载失败
        - beforeunload 资源卸载之前(window.beforeunload 页面关闭之前触发)
        - ...
    - CSS3动画事件
        - transitionend transition动画结束
        - transitionstart 开始
        - transitioncancel 取消
        - transitionrun 运行中
    - 视图事件
        - resize 元素（浏览器）大小改变
        - scroll滚动条滚动
    - 剪贴板
    - 拖放事件
    - 媒体事件
    - 。。。

2. 事件绑定：元素默认的事件行为绑定方法，行为触发，执行方法
    - DOM0
        - 语法：[元素].on[事件] = [函数] 
            - ```document.body.onclick = function(){};```
        - 移除：赋值为null或其他非函数值 
            - ```document.body.onclick = null;```
        - 原理：
            - 每个DOM元素对象的私有属性上有"onXXX"的私有属性，对其赋值，
            - 若为undefined没有私有属性不能绑定
            - 只能给当前元素的某个事件行为绑定一个方法，后来者覆盖
            - 性能高
    - DOM2
        - 语法: [元素].addEventListener([事件],[方法],[捕获/冒泡阶段])
            - ```document.body.addEventListener('click',fn1,false);```
        - 移除：[元素].removeEventListener([事件],[方法],[捕获/冒泡阶段])
            - ```document.body.removeEventListener('click',fn1,false);```
        - 原理：
            - 每个DOM元素都会基于\_\_proto\_\_，查找到EvnetTarget.prototype上的addEventListener / removeEventListener， 基于这些方法实现绑定和移除，采用事件池机制
            - DOM2绑定一般不用匿名函数
            - 凡是浏览器提供的事件行为，都可以基于这种模式完成绑定移除(例：window.onDomContentLoaded)
            - 可以给当前元素的某个事件类型绑定多个“不同”的方法（进入事件池），事件行为触发，事件池按绑定顺序取出方法执行
---
# 事件对象和阻止默认行为
3. 事件对象
    - 给当前元素的某个事件行为绑定方法，当事件行为触发，方法执行时，不仅会把方法执行，而且会给方法默认传递一个实参，这个实参即事件对象
    - 存储当前事件操作及触发的相关信息(浏览器本身记录，记录当前这次操作的信息，和所在函数无关)
    - MouseEvent
        - clientX/clientY 鼠标触发点距当前窗口左上角的X/Y轴坐标
        - pageX/pageY 鼠标触发点距body的X/Y轴坐标
        - type 事件类型
        - target/srcElement 获取当前事件源（当前触发的元素）
        - path 传播路径
        - ev.preventDefault() / ev.returnValue=false 阻止默认行为
        - ev.stopPorpagation() / ev.cancelBubble=true 阻止冒泡传播
    - KeyboardEvent
        - key 存储按键名字
        - which/keyCode 获取按键的键盘码
            - 方向键 37-40 左上右下
            - Space 32
            - BackSpace 8
            - Del 46
            - Enter 13
            - Shift 16 Ctrl 17 Alt 18
        - altKey (组合按键)
        - ctrlKey
        - shiftKey
    - TouchEvent
        - changedTouches(常用) 手指离开存储最后一次
        - targetTouches
        - touches 手指离开没有信息
        - => TouchList
        - ev.changedTouches[0] 第一个手指的信息
4. 阻止默认行为
    - 默认行为：浏览器赋予元素默认的行为操作
        - 鼠标右键菜单
        - a标签跳转
        - 记录输入记录
    - ev.preventDefault() 禁用
    ```js
    // 禁用右键菜单
    window.oncontextmenu = function(ev){
        ev.preventDefault();
    }
    // a标签跳转
    // 1. href="javascript:;"
    // 2. 
        link.onclick = function (ev){
            ev.preventDefault();

            // return false;
        }
    ```
---
# 事件的传播机制
5. 事件的传播机制
    - 阶段一：捕获阶段 CAPTURING_PHASE
        - window向下逐级查找事件源
        - 为冒泡阶段提供路径 => ev.path
    - 阶段二：目标阶段 AT_TARGET
        - 触发事件源的事件行为
    - 阶段三：冒泡阶段 BUBBLING_PHASE
        - 按路径，不仅触发当前事件源行为，从内到外，祖先元素的相关事件行为也触发（绑定方法也会执行）
    - DOM0在目标阶段/冒泡阶段触发,DOM2可以在捕获阶段触发
    - ev.stopPorpagation() / ev.cancelBubble=true 阻止冒泡传播
        - ```ev.stopPropagation ? ev.stopPorpagation() : ev.cancelBubble=true```
        -  事件委托/事件代理 ：利用冒泡传播机制，把一个容器A中所有后代元素的某个事件行为E触发要做的操作委托给A的事件行为E，只要触发A中任何元素的E行为，都会传播到A上，把给A绑定的方法执行。基于事件源不同做不同处理。
        - ```js
            // 点击事件行为存在冒泡传播机制，都会传播BODY上，触发body的click。
            // 根据target/srcElement 
            //
            // 性能高
            // 操作动态绑定的元素
            // 某些需求必须基于此完成
          document.body.onclick = function(ev) {
              let target = ev.target,
                  targetClass = target.className;
              if(targetClass==="inner"){
                  console.log('INNER');
                  return;
              }
                 if(targetClass==="box"){
                  console.log('BOX');
                  return;
              }
          };  
          ```
---
# mouseover和mouseenter
- over和out
    - 从父到子：出父入子（出父不正常）
    - 从子到父：出子入父（入父不正常）
- enter和leave
    - 默认阻止了事件冒泡传播