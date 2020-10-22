---
title: "CSS3 伪类伪元素&布局"
date: 2020-10-17T22:02:39+08:00
draft: false
---
# Content
- 伪类和伪元素
- 布局
- 实际布局
---
# 伪类和伪元素
- 伪类：
   - ⽤于当已有元素处于的某个状态时，为其添加对应的样式，这个状态是根据⽤户⾏为⽽动态变化的。
   - 伪类存在的意义是为了通过选择器，格式化DOM树以外的信息以及不能被常规CSS选择器获取到的
信息。

- 伪元素：
   - ⽤于创建⼀些不在⽂档树中的元素，并为其添加样式。
   - 伪元素可以创建⼀些⽂档语⾔⽆法创建的虚拟元素。
- 区别：
   - 有没有创建⼀个DOM树之外的元素
   - 伪类本质上是为了弥补常规CSS选择器的不⾜，以便获取到更多信息；伪元素本质上是创建了⼀个有内容的虚拟容器；
   - 可以同时使⽤多个伪类，⽽只能同时使⽤⼀个伪元素；
---
# 布局
- table

>   display:table  
>   dispaly:table-cell,  即td  
>   display:table-row,  即tr  
>   table-layout:fixed|auto   

- Float

>        在非IE浏览器下，当容器的高度为auto，且容器的内容中有浮动（float为left或right）的元素，在这种情况下，容器的高度不能自动伸长以适应内容的高度，使得内容溢出到容器外面而影响（甚至破坏）布局的现象。这个现象叫浮动溢出，为了防止这个现象的出现而进行的CSS处理，就叫CSS清除浮动。        
>
>        BFC的生成:满足条件：
>        1.根元素
>        2.float不为none
>        3.overflow不为visible
>        4.display为inline-block、table-cell、table-caption
>        5.position为absolute或fixed
>
>        BFC的约束规则：
>        1.内部的Box会垂直方向接连放置
>        2.margin塌陷
>        3.每个元素的margin-left与包含块的border-left相接触(左向右)，浮动元素也是如此
>        4.BFC区域不与float元素区域重叠
>        5.计算BFC高度，浮动子元素也参与
>        6.BFC就是页面上的隔离的独立容器，容器里的子元素不影响外面，反之亦然
>        
>        float+margin:两列布局 三列布局
- inline-block
> 处理间隙(父元素:font-size:0)
- Flex
> display: -webkit-box; /* Chrome 4+, Safari 3.1, iOS Safari 3.2+ */  
> display: -moz-box; /* Firefox 17- */  
> display: -webkit-flex; /* Chrome 21+, Safari 6.1+, iOS Safari 7+, Opera 15/16 */  
> display: -moz-flex; /* Firefox 18+ */  
> display: -ms-flexbox; /* IE 10 */  
> display: flex; /* Chrome 29+, Firefox 22+, IE 11+, Opera 12.1/17/18, Android 4.4+ */   
- Grid
- Columns 
- Shapes
- 盒模型
---
# 实际布局
- 水平居中
   - 文字,块,多个块
   ```html
   <body>
      <div id="parent">
         <div id="child">Margin</div>
      </div>
   </body>
   ```
   ```css
   <style>
   /* 方案1 */
   #parent{text-align:center;}
   #child{display:inline-block;}
   /* 优点：兼容性 */
   /* 缺点：子元素文本继承text-align而居中 */

   /* 方案2 */
   #child{display:table;margin:0 auto;}
   /*缺点：子元素脱离文档流，margin属性无效 */

   /* 方案3 */
   #parent{position:relative;}
   #child{position:absolute;left:50%;margin-left:-[parentWidth]/2;}

   /* 方案4 */
   #parent{position:relative;}
   #child{position:absolute;left:50%;transform:translateX(-50%)}
   /*优点: 父元素是否脱离文档流，不影响子元素水平居中*/
   /*缺点：兼容性 */

   /* 方案5 */
   #parent{display:flex; justify-content:center;}

   </style>

   ```
   - 小结
      - ⽂本/⾏内元素/⾏内块级元素 .parent{text-align:center}
      - 单个块级元素 .son{width:1000px(定宽)，margin:0 auto}
      - 多个块级元素 .parent{text-align:center} .son{display:inline-block}
      - 使⽤绝对定位: ⼦绝⽗相，top、right、bottom、left的值是相对于⽗元素尺⼨的，然后margin或者transform是相对于⾃身尺⼨的，组合使⽤达到⽔平居中的⽬的;
      - 任意个元素(flex): #parent{display: flex; justify-content: center; }
- 垂直居中
   ```html
   <body>
      <div id="parent">
         <div id="child">Margin</div>
      </div>
   </body>
   ```
   ```css
   <style>
   /* 方案1 */
   #parent{;}
   #child{line-height = [parentHeight];}

   /* 方案2 */
   #parent{display:table-cell;vertical-align:middle;}
   /*缺点：子元素脱离文档流，margin属性无效 */

   /* 方案3 */
   #parent{position:relative;}
   #child{position:absolute;top:50%;margin-top:-[parentWidth]/2;}

   /* 方案4 */
   #parent{display:flex; align-items:center;}
   /*缺点：子元素脱离文档流，margin属性无效 */

   </style>

   ```
   - 小结：
      - ⽂本/⾏内元素/⾏内块级元素 .parent{height:150px;line-height:150px;} ⾼度等于⾏⾼的值；
      - 图⽚元素: .parent{height:150px;line-height:150px;font-size:0;} .son{vertical-align:middle}
      - 单个块级元素:
          - 使⽤tabel-cell实现: .parent{display:table-cell;vertical-align:middle}
          - 使⽤position实现: ⼦绝⽗相，top、right、bottom、left的值是相对于⽗元素尺⼨的，然后margin或者transform是相对于⾃身尺⼨的，组合使⽤达到垂直居中的⽬的；
          - 利⽤flex实现 .parent{display:flex; align-items: center;}
      - 任意个元素：.parent{display:flex; align-items: center;} 或 .parent{display:flex;} .son{alignself:center;}或者 .parent{display:flex;flex-direction: column;justify-content: center;}
- [居中布局](https://github.com/MarginLon/CSS_JS_Repos/tree/main/CSS/%E5%B1%85%E4%B8%AD%E5%B8%83%E5%B1%80)
- [两列布局](https://github.com/MarginLon/CSS_JS_Repos/tree/main/CSS/%E4%B8%A4%E5%88%97%E5%B8%83%E5%B1%80)
- [三列布局1](https://github.com/MarginLon/CSS_JS_Repos/tree/main/CSS/%E4%B8%89%E5%88%97%E5%B8%83%E5%B1%801)
- [三列布局2，圣杯布局，双飞翼](https://github.com/MarginLon/CSS_JS_Repos/tree/main/CSS/%E4%B8%89%E5%88%97%E5%B8%83%E5%B1%802)
- [等分布局，等高布局，全屏布局](https://github.com/MarginLon/CSS_JS_Repos/tree/main/CSS/%E7%AD%89%E5%88%86%E5%B8%83%E5%B1%80)
- 多列布局
   - columns
   - column-width
   - column-count
   - column-rule-color
   - column-rule-style
   - column-rule-width
   - column-span
   - column-fill
   - column-gap