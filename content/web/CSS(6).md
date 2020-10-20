---
title: "CSS3 定位和层叠上下文原理"
date: 2020-10-19T22:02:39+08:00
draft: false
---
# Content
- 定位常见值及原理
- position fixed和sticky
- 层叠上下文和层叠顺序
- 层叠上下文形成条件
- 固定定位特殊性
- 层叠上下文对z-index的影响
---
# 定位常见值及原理
- position属性
   - static(default)
      - 默认定位，不产生重叠，top，right，bottom，left，z-index属性无效
   - relative
      - 相对于默认位置偏移，即定位基点为元素默认位置，必须搭配四方位一起使用
      - 使用情形：
         - 1.使方位和z-index生效
         - 2.作为absolute的参照物
   - fixed
      - 相对于viewport偏移，搭配四方位
      - 脱离文档流
      - 使用情形：
         - 1.滚动条滚动固定不动
   - absolute
      - 相对于上级（父元素）偏移
      - 父元素如果是static，变为相对于html
      - 脱离文档流
   - sticky(2017)
      - 动态固定
   - 小结
      - 文档流： 
         1. 脱离：absolute + fixed
         2. 不脱离：relative
      - 参照物：
         1. absolute - 父
         2. fixed - 窗口
         3. relative - 自身
      - 相同点： 方位 + z-index 提高层级
---
# position fixed和sticky
- fixed
   - 始终固定
   - 方位设置，不显式设置也会生效
   - 脱离文档流
- sticky
   - 不一定始终固定
   - 方位设置临界值才固定，至少显式设置一个方位
   - 不脱离文档流
   - 元素的定位参考对象距离其最近的overflow属性值为visible的具有滚动条的祖先元素，如果是以
body或者body的⽗辈元素为考，那么定位参考对象是窗⼝。
---
# 层叠上下文和层叠顺序
- 层叠上下文
- 层叠等级
   - 同一个层叠上下文，它描述定义的是该层叠上下⽂中的层叠上下⽂元素在Z轴上的上下顺序。
- 层叠顺序
   - 正z <span style = "color:red">></span> z-index:auto | 0 <span style = "color:red">></span> inline/inline-blocke <span style = "color:red">></span> float <span style = "color:red">></span> block <span style = "color:red">></span> 负z <span style = "color:red">></span> 层叠上下文 background/border
   - 装饰 <span style = "color:red">></span> 布局 <span style = "color:red">></span> 内容
---
# 层叠上下文形成条件
- 层叠上下文
   - _<html_>
   - position 值为 absolute（绝对定位）或 relative（相对定位）且 z-index 值不为 auto 的元素；
   - position 值为 fixed（固定定位）或 sticky（粘滞定位）的元素;
   - flex (flexbox) 容器的⼦元素，且 z-index 值不为 auto；
   - grid (grid) 容器的⼦元素，且 z-index 值不为 auto；
   - opacity 属性值⼩于 1 的元素；
   - mix-blend-mode 属性值不为 normal 的元素；
   - 不为none：
      - transform
      - filter
      - perspective
      - clip-path
      - mask / mask-image / mask-border
   - isolation : isolate
   - -webkit-overflow-scrolling:touch
   - will-change
- 条件小结
   - 1.html
   - 2.position(非static)
   - 3.CSS3
- 小结
   - 层叠上下⽂可以包含在其他层叠上下⽂中，并且⼀起创建⼀个层叠上下⽂的层级。
   - 每个层叠上下⽂都完全独⽴于它的兄弟元素：当处理层叠时只考虑⼦元素。
   - 每个层叠上下⽂都是⾃包含的：当⼀个元素的内容发⽣层叠后，该元素将被作为整体在⽗级层叠上下
⽂中按顺序进⾏层叠。
---
# 固定定位特殊性
- 单纯是绝对/相对定位元素是⽆法创建⼀个层叠上下⽂的，需要同时满⾜ z-index 值不为 auto 的条
件。然⽽，固定定位元素就不需要满⾜这个条件.
- 固定定位元素⽆需满⾜ z-index 值不为 auto 的条件就可以创建层叠上下⽂；同样地，设置 z-index:
auto 并不能撤销固定定位元素所创建的层叠上下⽂。
- 正常情况下，固定定位是相对于浏览器视窗（viewport）进⾏定位的，但是当其祖先元素中存在符
合以下任意⼀个条件的元素时，固定定位元素会相对于该元素进⾏定位：
   1. transform不为none;
   2. transform-style:preserve-3d;
   3. perspective不为none;
   4. will-change指定上面任一个;

---
# 层叠上下文对z-index的影响
- 层叠上下⽂（stacking context）并不只是z-index（必须配合position才能⽣效）才能创建，还有
很多其他元素（如：opacity、transform等）也可以创建层叠上下⽂;
- 在存在层叠上下⽂的情况下，z-index的⼤⼩决定了层叠⽔平（stacking level），
- 层叠⽔平的⽐较只有在同⼀级别的DOM节点的层叠上下⽂中才有意义;
- 在同⼀DOM节点，并且层级⽔平⼀样的情况下，在HTML⽂档中写在后⾯的元素会遮住前⾯的元素
---