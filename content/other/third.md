---
title: "Resume CSS"
date: 2020-07-18T22:59:58+08:00
draft: false
---
### CSS Info
1. Font Order:
      font-style, font-variant, font-weight, font-stretch, font-size, line-height, font-family

      Sample:

      font: italic normal bold normal 3em/1.5 Helvetica, Arial, sans-serif;
### Q&A
2. CSS实际工作：

    ![HowCSSWork](https://github.com/MarginLon/MarginPostImage/blob/master/HowCSSWork.png?raw=true)

    1.浏览器加载HTML

    2.HTML->DOM

    3.浏览器获取HTML链接的大多数资源，包括CSS

    4.解析CSS，选择器类型将不同规则分类为不同的“存储桶”（渲染树）

    5.将渲染树放置在规则应用到其后应出现的结构中。

    6.页面的视觉显示（绘画）


3. 选择器
   级联：两个规则，后者胜出

   特异性：内联>id>类>元素

   继承:inherit initial unset




### git
git上传

git init

git add .

git commit -m "注释语句"

git remote add origin 网址

git pull --rebase origin master

git push -u origin master

-------------------------------------
