---
title: "HTML5 CSS3回顾"
date: 2020-10-14T22:02:39+08:00
draft: false
---
# Content
- HTML
   - 语义化
   - 规范
   - 扩展
      - meta
      - Entity
- CSS
   - At-rule
   - CSS变量
# HTML
## 语义化
- 概念：对⽂本内容结构化（内容语义化），选择合乎语义的标签（代码语义化），便于开发者阅读，维护和写出更优雅的代码的同时，让浏览器的爬⾍和辅助技术更好的解析
- 优势：
   + 利于SEO优化
   + 在样式丢失的时候，仍可以⽐较好的呈现结构
   + 更好地⽀持各种终端
   + 利于团队开发和维护，提⾼效率
## 规范
- div和p，尽量⽤p，因为p在默认情况下有上下间距，对兼容特殊终端有利。
- 需要强调的⽂本，可以使⽤ strong 或 em 标签。
- 使⽤表格时，标题⽤ caption，表头⽤ thead，主体部分⽤ tbody 包围，尾部⽤ tfoot 包围。表头
和⼀般单元格要区分开，表头⽤ th，单元格⽤ td。
- 表单域要⽤ fieldset 标签包起来，并⽤ legend 标签说明表单的⽤途（可理解为表单标题）。
```html
<form>
<fieldset>
<legend>Personalia:</legend> <!-- legend 可理解为表单标题 -->
Name: <input type="text"><br>
Email: <input type="text"><br>
Date of birth: <input type="text">
</fieldset>
</form>
```
- 每个input标签对应的说明⽂本都需要使⽤label标签，并且通过为input设置id属性，在lable标签中
设置for=someld来让说明⽂本和相对应的input关联起来。或者直接在label中内嵌控件。
```html
<label for="username">请输⼊⽤户名: </label>
<input type="text" id="username" name="username">
<!-- OR -->
<label>请输⼊⽤户名<input type="text" id="username" name="usern
ame"></label>
```
- 嵌套规范：
   + 内联元素不能包含块元素
   + 块元素不能放在\<p\>内
   + h1~h6,dt不能包含块元素
- title, keywords, description精简全面
- a标签设置title;外部链接设置rel; rel="nofollow"
- 所有标题使用h1
- br只用于文本换行
- img设置alt
## 扩展
- meta
```html
<!-- 编码 -->
<meta charset="UTF-8" />
<!-- 关键词 -->
<meta name="keywords" content="" />
<!-- 描述 -->
<meta name="description" content=" " />
<!-- 视口-移动设备 -->
<meta name="viewport" content="width=device-width, initial-scale=
1">
<!-- 优先使用IE新版本和Chrome -->
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
<!-- 刷新和重定向 -->
<meta http-equiv="refresh" content="0;url=" />
<!-- 禁⽌浏览器从本地计算机的缓存中访问⻚⾯内容 -->
<meta http-equiv="Pragma" content="no-cache">
<!-- 避免转码 -->
<meta http-equiv="Cache-Control" content="no-siteapp" />
<!-- 启用WebApp全屏模式 -->
<meta name="apple-mobile-web-app-capable" content="yes" />
```
- Entity
![Entity](https://github.com/MarginLon/MarginPostImage/blob/master/HTML%20Entity.png?raw=true)
---
# CSS
## At-rule
- 常规 ：@[KEYWORD] (RULE)
   + @charset
   + @import
   + @namespace
- 嵌套 : @[KEYWORD] { /* 嵌套语句 */ }
   + @document
   + @font-face
   + @keyframes
   + @media
   + @page
   + @supports
--- 
## CSS变量
- 全局/局部
```css
/*全局变量*/
:root { --color: blue; }
.box{color: var(--color)}

/*局部变量*/
.box{
--color: red;
color: var(--color);
}
```
- 拼接
   + 如果变量值是⼀个字符串，可以与其他字符串拼接；
   + 如果变量值是数值，不能与数值单位直接连⽤，使用calc()函数；
   + 如果变量值带有单位，就不能写成字符串;
```css
/*字符串拼接*/
.foo {
   --bar: 'hello';
   --concat: var(--bar) ' world';
}
/*变量为数值*/
.foo {
   --gap: 20;
   margintop: calc(var(--gap) * 1px);
}
/*带单位*/
.foo {
   --foo: 20px;
   font-size: var(--foo);
}
```