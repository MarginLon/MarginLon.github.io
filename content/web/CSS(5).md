---
title: "CSS3 伪类伪元素&布局"
date: 2020-10-17T22:02:39+08:00
draft: false
---
# Content
- 伪类和伪元素
- 布局
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

>   

- 盒
- Flex
- Grid
- Columns 
- Shapes
- 居中
- 多列
- 全屏


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
   #parent{display:flex; align-items:center;}

   </style>

   ```
   - 小结
      - 
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
   #child{position:absolute;}
   /*缺点：子元素脱离文档流，margin属性无效 */

   </style>

   ```
