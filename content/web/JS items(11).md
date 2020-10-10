---
title: "JavaScript 复习（二）"
date: 2020-10-05T18:02:39+08:00
draft: false
---
### 判断
- if, else if, else
    - A && B
        * 如果第一个操作数是对象，则返回第二个数
        * 如果第二个操作数是对象，则只有在第一个操作数的求值结果为true的情况下才会返回该对象。
        * 如果两个操作数都是对象，则返回第二个数操作数。 
        * 如果有一个操作数是null，则返回null。 
        * 如果有一个操作数是NaN，则返回第NaN。
        * 如果第一个操作数是undefined，则返回undefined。 
        * 对于逻辑与，如果第一个操作数是false，无论第二个操作数是什么，结果都不可能再是true。
    - A || B
        * 如果第一个操作数是对象，则返第一个操作数
        * 如果第一个操作数的求值结果为false，则返回第二个操作数
        * 如果两个操作数都是对象，则返回第一个操作数
        * 如果两个操作数是null，则返回null
        * 如果两个操作数是NaN，则返回NaN
        * 如果两个操作数是undefined，则返回undefined 
- a?b:c
- switch case
```js
let x = '10';
switch(x){
    case '10': 
    //=> do it
        x += 1;
        break;
    default:
        //=>else
        x += 2;

}
```
- Exercise
```html
<body style="background-color:white ;">
    <button id="lamp">close</button>
        <script>
            let lamp = document.getElementById('lamp');
            let body = document.body;

            lamp.onclick = function () {
                let bg = body.style.backgroundColor; //只能控制行内样式
                if(bg === 'white') {
                    body.style.backgroundColor = "black";
                    lamp.innerText = "open";
                }
                else {
                    body.style.backgroundColor = "white";
                    lamp.innerText = "close";
                }
            };
        </script>
</body>
```
---
### 循环
- for(init; condition; stride){ }
    - break
    - continue
- for (var key in obj){ }  
--- 
### DOM相关
```js

```
