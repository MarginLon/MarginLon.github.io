---
title: "CSS3 工作原理性能优化"
date: 2020-10-23T22:02:39+08:00
draft: false
---
# Content
- CSS布局模型
- BFC
- IFC
- font-size、line-height、vertical-align
---
# CSS布局模型
- flow
    - inline(默认间距去除：父容器:font-size:0;)
    - img的默认间距
- float
  >        在非IE浏览器下，当容器的高度为auto，且容器的内容中有浮动（float为left或right）的元素，在这种情况下，容器的高度不能自动伸长以适应内容的高度，使得内容溢出到容器外面而影响（甚至破坏）布局的现象。这个现象叫浮动溢出，为了防止这个现象的出现而进行的CSS处理，就叫CSS清除浮动。        
    - 子元素浮动 父元素高度塌陷(height:0)
        1. 手动添加height 缺点：高度定死
        2. overflow:hidden 缺点:溢出隐藏  - 下拉框
            -  原理：BFC 规则： 计算BFC高度，浮动子元素也参与
        3. clear:left/right/both - 块的特点 + clear:both + 空内容 - 缺点：无意义标签
        4. 优化第三方案 
            ```css
            .clearfix::after { 
                content :''; 
                display:block; 
                clear:both; 

                width:0; 
                height:0; 
                font-size:0; 
                overflow:hidden; 
                visibility:hidden; 
                } 
            ```
            - 可公用
- layer
    
    - 相同点：position + 方位 + z-index
    - 不同点：
        - 参照物
            1. relative :自身
            2. absolute ：父元素 脱离文档流
            3. fixed ： 脱离文档流
---
# BFC

>
        >        BFC的生成:满足条件：
        >        1.根元素
        >        2.float不为none
        >        3.overflow不为visible(auto scroll hidden)
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
---
# IFC
>      形成条件： 块级元素中仅含内联元素
>      布局规则：
>       1. 子元素水平方向横向排列，并且垂直方向起点为元素顶部
>       2. 子元素只计算横向样式空间[padding,border,margin]
>       3. 垂直方向，子元素以不同方式对齐
>       4. 行框(line box)宽度由包含块和其中浮动决定 
>       5. line box两边紧贴包含块 float优先排列
>       6. line box高度由CSS行高计算规则缺点，同个IFC的多个line box可能高度不同
>       7. inline-level boxes总宽度低于line box，水平渲染规则由text-align决定
>       8. inline box 超过父元素宽度 被分割成多个boxex，分布在多个line box。子元素未设置强制换行时，inline box将不可被分割，溢出父元素。
---
# font-size、line-height、vertical-align
- font-size
    - body 62.5% = 10px
- line-height
    - 不定尺寸或多行文字垂直居中
        1. 主体元素inline-block
        2. 0宽度100%高度辅助元素
        3. vertical-align:middle; (font-size:0) 
    - img下间隙
        - vertical-align: top
        - img{display: block;}
        - font-size: 0 
        - 外套一个div line-height足够小
    - line-height决定一个内联元素的真实占位(真实占行高度)
- vertical-align        