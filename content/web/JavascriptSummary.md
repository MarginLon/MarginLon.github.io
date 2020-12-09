---
title: "JavaScript Summary"
date: 2020-12-09T10:02:39+08:00
draft: false
---
- [Abstract](#abstract)
- [Basic Item](#basic-item)
    - [$\color{#FFDAB9}{数据类型及转换}$](#colorffdab9数据类型及转换)
    - [$\color{#8470FF}{数据类型}$](#color8470ff数据类型)
      - [原始值](#原始值)
        - [Undefined](#undefined)
        - [Null](#null)
        - [Boolean](#boolean)
        - [Number](#number)
        - [String](#string)
        - [Symbol](#symbol)
        - [Bigint](#bigint)
      - [引用类型](#引用类型)
        - [对象/函数（基于构造函数创造的实例）](#对象函数基于构造函数创造的实例)
    - [$\color{#8470FF}{类型转换}$](#color8470ff类型转换)
      - [typeof](#typeof)
      - [其他=>Number](#其他number)
      - [其他=>String](#其他string)
      - [其他=>布尔](#其他布尔)
      - [==的规则](#的规则)
      - [对象=>字符串/数字](#对象字符串数字)
      - [其他](#其他)
  - [<br/>](#)
- [Example](#example)
---
# Abstract

---

# Basic Item

### $\color{#FFDAB9}{数据类型及转换}$
<br/>

### $\color{#8470FF}{数据类型}$
<br/>

#### 原始值
<br/>

##### Undefined
##### Null
##### Boolean
##### Number
##### String
##### Symbol
##### Bigint
<br/>

#### 引用类型
<br/>

##### 对象/函数（基于构造函数创造的实例）
| Object | Array | RegExp | Date | Error | Set/Map | ...  |
| :----- | :---- | :----- | :--- | :---- | :------ | :--- |
<br/>

### $\color{#8470FF}{类型转换}$
<br/>

#### typeof
<br/>

- 返回字符串
- null -> 'object'
- 实现CALL的对象[函数、箭头函数、生成器函数、构造函数] -> 'function'
- 未实现CALL的对象 -> 'object'
<br/>

#### 其他=>Number
<br/>

- Number([val])
  - 隐式转换的调用方法（如```isNaN()```）
  - 出现非有效数字字符即为```NaN```
- parseInt/parseFloat([val],[radix])
  - [val] 必须是一个字符串，否则隐式转换
  - [radix] 不设置或为0，按照10处理，若字符串'0x'开头，按照16处理
  - 处理过程：在[val]中找到所有符合[radix]进制的内容，直到遇到不符合的字符，把找到的内容按照[radix]进制转换为10进制
  - [radix]范围：2~36,包括0,否则```NaN```
- 隐式转换
  - inNaN()
  - 数学运算(特殊："+"的字符串拼接)
  - "=="
<br/>

#### 其他=>String
<br/>

- toString()
    - 普通对象{} => 'object Object'
- String([val])
- 隐式转换
  - "+" : 一边出现字符串，则拼接
  - 基于alert/confirm/prompt/document.write等方式输出
<br/>

#### 其他=>布尔
<br/>

- !
- !!
- Boolean([val])
- 隐式转换
  - 循环或条件判断的结果
- 规则:
  - 只有"0, NaN, Null, Undefined, 空字符串"为False
<br/>

#### ==的规则
<br/>

- 类型相同
  - ```{}=={}``` :false 比较堆内存地址
  - ```[]==[]``` :false 
  - ```NaN==NaN``` :false ```Object.is(NaN, NaN)``` :true
- 类型不同
  - ```null==undefined``` :true ```===``` :false null/undefined与其他类型不相等
  - 字符串==对象 对象=>字符串
  - 两边类型不一致，先转换为数字再比较
<br/>

#### 对象=>字符串/数字
<br/>

1. 检测```Symbol.toPrimitive```，获得原始值
2. 第一步没有，```valueOf```获取原始值
3. 第二步没有，调用```toString```，字符串
4. 第三步后，若有需要，基于```Number()```，数字
<br/>

#### 其他
<br/>

- "+"
  - {} + 0 左边{}视为代码块 // +0 => 0
  - ({} + 0) "[object Object]0"
  - 0 + {} "0[object Object]"
- 模板字符串实现的是字符串拼接，对象转换为字符串，其余数学运算，对象=>数字
<br/>
---

# Example

---