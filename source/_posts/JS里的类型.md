---
title: JS里的类型
date: 2018-04-25 11:27:37
tags: JavaScript
categories: JavaScript
---

# JS里的类型

## 任意类型转字符串

1. String(x）
![](https://i.loli.net/2018/04/24/5adee7c2811d7.png)
2. x.toString()
![](https://i.loli.net/2018/04/24/5adee7fab109c.png)
3. x + ''
![](https://i.loli.net/2018/04/24/5adee7faaffac.png)

## 任意类型转数字

1. Number(x)
2. parseInt(x, 10)[MDN相关资料](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
3. parseFloat(x)[MDN相关资料](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)
4. x - 0
5. +x

## 任意类型转布尔

1. Boolean(x)
2. !!x

## 内存图

1. 你买一个 8G 的内存条
2. 操作系统开机即占用 512MB
3. Chrome 打开即占用 1G 内存
4. Chrome给每个网页分配一定数量的内存
5. 这些内存要分给页面渲染器、网络模块、浏览器外壳和 JS 引擎（V8引擎）
6. JS 引擎将内存分为代码区和数据区
7. 我们只研究数据区
8. 数据区分为 Stack（栈内存） 和 Heap（堆内存）
9. 简单类型的数据直接存在 Stack 里
10. 复杂类型的数据是把 Heap 地址存在 Stack 里

## some面试题

```
javascript
var a = 1
var b = a
b = 2
请问 a 显示是几？  


javascript
var a = {name: 'a'}
var b = a
b = {name: 'b'}
请问现在 a.name 是多少？


javascript
var a = {name: 'a'}
var b = a
b.name = 'b'
请问现在 a.name 是多少？


javascript
var a = {name: 'a'}
var b = a
b = null
请问现在 a 是什么？

```

## 深复制

````
var a = 1
var b = a
b = 2 //这个时候改变 b
a 完全不受 b 的影响
那么我们就说这是一个深复制
````

对于简单类型的数据来说，赋值就是深拷贝。
对于复杂类型的数据（对象）来说，才要区分浅拷贝和深拷贝。

这是一个浅拷贝的例子

```
var a = {name: 'frank'}
var b = a
b.name = 'b'
a.name === 'b' // true
```

因为我们对 b 操作后，a 也变了

什么是深拷贝了，就是对 Heap 内存进行完全的拷贝。

```
var a = {name: 'frank'}
var b = deepClone(a) // deepClone 还不知道怎么实现
b.name = 'b'
a.name === 'a' // true
```



