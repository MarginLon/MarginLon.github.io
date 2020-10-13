---
title: "CSS 回顾"
date: 2020-10-12T10:02:39+08:00
draft: false
--- 
### 文字
```css
body {
    font-family:'Arial';
    font-size:40px;
    color:red;
    font-weight:bold;
    font-style:italic;
    text-decoration:line-through|underline|overline;
    text-indent:2em;
    line-height:30px;
    letter-spacing:2em;
    text-align:center|left|right;
    }
```
### 列表
```css
ul{
    list-style-type:circle|disc|square|decimal|lower-alpha|upper-alpha;
    list-style-position:outside|inside;
}
```
### 链接
```css
a:link{}
a:hover{}
a:active{}
a:visited{}
```
---
## 元素分类
- 块级元素
```css
<!--宽度继承父元素-->
<div>
  <p></p>
  <h1>
    ...
    <h6>
      <ol>
        <ul>
          <table>
            <address>
              <blockquote>
                <form></form>
              </blockquote>
            </address>
          </table>
        </ul>
      </ol>
    </h6>
  </h1>
</div>
```
- 行内元素
```css
<!--宽度为包含的内容的宽度，高度，行高，顶底边间距不可以设置-->
<a>
  <span>
    <br />
    <i>
      <em>
        <strong> <label></label></strong></em></i></span
></a>
```
- 行内块元素
```css
<img /> <input />
```
---
### 边框
```css
div {
    border:2px solid|dashed|dotted red;
    border-radius:50%;
}

```
### 溢流
```css
p {

}
.one {
    overflow:auto;
}
.two {
    overflow:hidden;
}
.three {
    overflow:visible;
}
```
### 背景
```css
div {
    background-image: linear-gradient(to bottom, red, blue);
}
```
### 轮廓
```css
p{
    outline:red dotted thick;
}
```
### 阴影
```css
div {
    box-shadow:inset 2px 2px 5px #000000;
}
```
---
## 选择器
- 基础选择器：标签选择器，类选择器，id 选择器，通配符选择器
- 组合选择器：标签指定式选择器(p.one)，后代选择器(p .one)，子代选择器(p>.one)并集选择器
- 属性选择器
    - E[attr]
    - E[attr=val]
    - E[attr~=val]:其中一个等于"val"
    - E[attr|=val]:其中之一以"val"开头
- 伪类选择器
    - :link
    - :hover
    - :active
    - :visited
---
## 布局模型
- Flow
    1. 块状元素在所处的包含元素内，自上而下按顺序垂直延伸，默认宽度100%
    2. 行内元素从左至右
- Float
    1. 伪元素清除浮动
```css
.clearfix:after {
  content: '';
  /*设置内容为空*/
  height: 0;
  /*高度为0*/
  line-height: 0;
  /* 行高为0*/
  display: block;
  /*将文本转为块级元素*/
  visibility: hidden;
  /*将元素隐藏*/
  clear: both; /*清除浮动*/
}

.clearfix {
  zoom: 1;
  /*为了兼容IE*/
}
```
- Layer
```css
/* 1. 绝对定位 */
/* + 以浏览器左上角为基准
   + 一个盒子包含在另一个盒子里，父不定位，子以浏览器左上角定位；父定位，子以父左上角定位
   + 绝对定位不占空间
*/
div {
    position:absolute;
    left: 100px; /*相对于浏览器向左偏移100像素*/
    top: 80px; /*相对于浏览器向上偏移80像素*/
    }


/* 2. 相对定位 */
/* + 以元素自身的位置为基准
   + 占空间位置
   + 子绝对父相对
*/
.box1 {
        width: 200px;
        height: 100px;
        position: relative;
        border: 1px dashed green;
      }
.box2 {
        width: 100px;
        height: 50px;
        position: absolute;
        border: 1px dashed blue;
        top: 20px;
        left: 20px;
      }

/* 3. 固定定位 */
/* + 类似于绝对定位，但固定定位相对于浏览器视口本身，而非<html>或祖先元素*/
p {
        position: fixed;
        top: 200px;
        left: 100px;
      }
```

    