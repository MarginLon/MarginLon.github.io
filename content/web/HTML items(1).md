---
title: "HTML items(1)"
date: 2020-07-16T22:59:58+08:00
draft: false
---

[简历练习](https://marginlon.github.io/post/resume/)
---------------


### Q&A：
1.HTML是什么，HTML5是什么？

<font color=#0000CD >HTML 指的是超文本标记语言 (Hyper Text Markup Language)
HTML5 是最新的 HTML 标准。
</font>

2.HTML元素标签、属性都是什么概念？
<font color=#0000CD >
HTML 元素指的是从开始标签（start tag）到结束标签（end tag）的所有代码。
HTML 标签可以拥有属性。属性提供了有关 HTML 元素的更多的信息。
属性总是以名称/值对的形式出现，比如：name="value"。
属性总是在 HTML 元素的开始标签中规定。
</font>

3.文档类型是什么概念，起什么作用？
<font color=#0000CD >Web 世界中存在许多不同的文档。只有了解文档的类型，浏览器才能正确地显示文档。
HTML 也有多个不同的版本，只有完全明白页面中使用的确切 HTML 版本，浏览器才能完全正确地显示出 HTML 页面。这就是 <!DOCTYPE> 的用处。
<!DOCTYPE> 不是 HTML 标签。它为浏览器提供一项信息（声明），即 HTML 是用什么版本编写的。
</font>

4.meta标签都用来做什么的？
<font color=#0000CD >&lt;meta&gt; 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。
&lt;meta&gt; 标签位于文档的头部，不包含任何内容。<meta> 标签的属性定义了与文档相关联的名称/值对。
</font>

5.Web语义化是什么，是为了解决什么问题
<font color=#0000CD >Web 语义化 = Web的意义
Web语义化是指使用恰当语义的html标签、class类名等内容，让页面具有良好的结构与含义，从而让人和机器都能快速理解网页内容。语义化的web页面一方面可以让机器在更少的人类干预情况下收集并研究网页的信息，从而可以读懂网页的内容，然后将收集汇总的信息进行分析，结果为人类所用；另一方面它可以让开发人员读懂结构和用户以及屏幕阅读器（如果访客有视障）能够读懂内容。
有利于 SEO ,即搜索引擎优化。
</font>

6.链接是什么概念，对应什么标签？
<font color=#0000CD >&lt;meta&gt; HTML 使用超级链接与网络上的另一个文档相连。
对应&lt;a&gt;&lt;/a&gt;
</font>

7.常用标签都有哪些，都适合用在什么场景
<font color=#0000CD >&lt;a&gt;&lt;/a&gt;:超链接
&lt;article&gt;&lt;/article&gt;:帖子等
&lt;aside&gt;&lt;/aside&gt;:侧边栏
&lt;b&gt;&lt;/b&gt;:加粗
......<br />
</font>

8.表单标签都有哪些，对应着什么功能，都有哪些属性

<font color=#0000CD >&lt;form&gt;&lt;/form&gt;
<b> 元素input：</b>
<form>
First name:<br>
<input type="text" name="firstname">
<br>
Last name:<br>
<input type="text" name="lastname">
</form>
<br />
action属性： 定义在提交表单时执行的动作。向服务器提交表单的通常做法是使用提交按钮。省略跳转当前。
<br />
method属性：GET & POST
<br />
name属性：
<br />
&lt;fieldset&gt;&lt;/fieldset&gt;
&lt;legend&gt;&lt;/legend&gt;
</font>

9.ol, ul, li, dl, dd, dt等这些标签都适合用在什么地方，举个例子
<font color=#0000CD > ol ul li 列表元素
dl dd dt 定义列表元素</font>
