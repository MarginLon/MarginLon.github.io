---
title: "CSS3 移动端响应式"
date: 2020-10-24T10:02:39+08:00
draft: false
---
# Content
- 像素相关
- layout viewport与visual viewport
- viewport缩放适配
- 媒体查询@media
- vw弹性适配
- 动态rem适配
- 弹性flex适配
---
# 像素相关
- 设备像素（像素分辨率） 
    - 设备能控制显示的最小单位，常说的1920×1080像素分辨率就是用的设备像素单位.
- 设备独立像素(dips)    
    - 与设备无关的逻辑像素，代表可以通过程序控制使用的虚拟像素，包含越多的物理像素越清晰
    - window.screen.width|height
- CSS像素
    - 指的是我们在样式代码中使用到的逻辑像素，是一个抽象概念
    - window.innerWidth|Height 含滚动条
    - document.documentElement.clientWidth/Height Layout Viewport的尺寸（Layout Viewport是\<html\>元素的父容器） 不包含滚动条
    - document.documentElement.offsetWidth/Height html元素的尺寸
    - window.pageX/YOffset visual viewport对于layout viewport的偏移值
- 关系
    -  PC端 —— 1个设备独立像素 = 1个设备像素 （在100%，未缩放的情况下，如果缩放到200%可以说1个设备独立像素 = 2个设备像素）
    - 移动端 —— 根据设备不同有很大的差异，根据 ppi 不同我们可以得到不同的换算关系，标准屏幕（160ppi）下 1个设备独立像素 = 1个设备像素
- devicePixelRaio(DPR)  
    - window.devicePixelRaio
    - DPR = 设备像素/设备独立像素
- 设计
    - iphone5 320*568 DPR 2.0 尺寸640\*1136
    - iphone6 375*667 DPR 2.0 尺寸750\*1334
    - iphone6 414*736 DPR 3.0 尺寸1242\*2208
---
# layout viewport与visual viewport
- layout viewport用css像素来衡量尺寸，在缩放、调整浏览器窗口的时候不会改变。缩放、调整浏览器窗口改变的只是visual viewport。
- 在桌面浏览器中，缩放为100%的时候，Layout Viewport宽度等于内容窗口的宽度。但是在移动端，缩放为100%的时候，Layout Viewport不一定等于内容窗口的大小（无响应式设计的需要滑动看）。
# viewport缩放适配
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scaleable=0">
```
---
# 媒体查询@media
- 手机 + pc 结构写在一套html里
- 1.@media
- 2.媒介 screen|TV|print
- 3.连接符 and not only
- 4.判断条件(max/min-width/height)
- 5.{CSS代码块}
- @media(orientation:portrait|landscape)
```css
@media screen and (max-width:480px) {
    .header {display:none;}
    .touchHeader {display:none;}
}
```
---
# vw弹性适配 动态rem适配
- 单位
    - pc: px % em
        - 1em = 16px (父容器html)
            - 首行缩进  p {text-indent:2em;}
            - logo  .logo {text-indent:-9999em;}
    - 手机: rem vw vh vmin vmax
        - 1rem = 16px (根root)
            - 1rem = 100px
        - viewport
            - vw 1/100 * 视口宽度
            - vh 1/100 * 视口高度
            - vmin vmax
    - 换算
        1. 我们假设pad的设计稿是以1920px为标准的。那么：
100vw = 1920px
1vw = 19.2px
我们想要： 1rem = 100px
那么:
100px = 100vw / 19.2 = 1rem
所以：
1rem = 5.208vw。
这时候，我们只要给html的根元素设置：
font-size: 5.208vw即可。

        2. 同理的，手机端我们假设设计稿是以750px为标准的，那么:
100vw = 750px
1vw = 7.5px
我们想要： 1rem = 100px
那么：
100px = 100vw / 7.5 = 1rem
那么：
1rem = 13.33vw
---
# 弹性flex适配
- flex容器
    - [阮一峰flex](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
    - flex-direction:row|vertical(旧:box-orient:horizontal|vertical(多行文本省略号))
        - [多行文本省略号]()
    - flex-wrap:wrap|wrap-reverse 自动折行
    - flex-flow 上两项复合
    - justify-content
    - align-items
    - align-content
- item项目
    - order: 0 排列顺序
    - flex-grow:
    - flex-shrink:
    - flex-basis