---
title: "CSS3 回顾"
date: 2020-10-13T10:02:39+08:00
draft: false
--- 
# CSS3
### 浏览器引擎前缀
- -moz- ：Firefox 等使用 Mozilla 引擎的浏览器。
- -webkit- ：Safari 、 Chrome 等使用 Webkit 引擎的浏览器。
- -o- ：Opera 浏览器早期。
- -ms- ：IE 和 Edge 等 。

### 背景
- background-size:length|percentage|cover|contain;
- background-origin:padding-box|border-box|content-box;
- background-clip:border-box|padding-box|content-box;.

### 边框
- border-radius
- border-image:source(url) slice width outset repeat;
    - slice:图片边框向内偏移。
    - width:图片边框宽度。
    - outset:边框图像区域超出边框的量。
    - repeat:图像边框是否应该平铺（repeat）、铺满（round）或拉伸（stretch）。
- box-shadow:水平阴影 垂直阴影 模糊阴影 阴影尺寸 阴影颜色 inset;

### 文字
- RGBA
- text-shadow:水平阴影 垂直阴影 模糊阴影 阴影颜色;
- text-overflow:clip|ellipsis|string;
- overflow-wrap:normal|break-word;
- word-break:normal|break-all|keep-all|;

### 动画&过渡
- 渐变
    - 线性 
        + background: linear-gradient(to direction | angle, color-stop1, color-stop2...);
    - 径向
        + background-image: radial-gradient(shape size at position,start-color,...,last-color);
- 过渡
    - transition: transition | transition-duration | transition-timing-function |
  transition-delay;
        + cubic-bezier(n,n,n,n):在 cubic-bezier 函数中定义自己的值，取值范围是 0 ~ 1。
- 2D&3D
    - transform: 将 2D 或 3D 转换应用到元素上去
    - transform-origin：可以改变被转换元素的位置
    - transform-style：规定被嵌套元素如何在 3D 空间中显示
    - perspective：规定 3D 元素的透视效果，与 perspective-origin 结合使用，可以改变 3D 元素的底部位置
- 动画
    - @keyframes
---
## 布局
- Flex
    - 容器属性
        + flex-direction
            + row|row-reverse|column|column-reverse
        + flex-warp
            + nowrap|wrap|warp-reverse
        + flex-flow
            + flex-direction和flex-warp的简写
        + justify-context
            + flex-start|flex-end|center|space-between|space-around 
        + align-items
            + flex-start|flex-end|center|baseline|stretch
        + align-content
            + flex-start|flex-end|center|space-between|space-around 
    - 子元素属性
        + flex
            + flex-grow || flex-shrink || flex-basis;
        + align-self
---
### 选择器
- E~F E+F
- E[attr^="val"]:以val开头
- E[attr$="val"]:以val结尾
- E[attr*="val"]：包含val
- E:root 设置html
- E:nth-child(n) 第n个子元素
- E:nth-last-child(n)
- E:nth-of-type() 
- E:nth-last-of-type(n)
- E:last-child
- E:first-of-type
- E:last-of-type
- E:first-of-type
- E:only-child
- E:only-of-type
- E:empty
- E:target
- E:not(s)
- E:enabled & E:disabled
- E:checked



