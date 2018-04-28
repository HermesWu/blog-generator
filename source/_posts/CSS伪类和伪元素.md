---
title: CSS伪类和伪元素
date: 2018-04-28 18:11:10
tags: 伪类
categories: CSS3
---

# CSS伪类和伪元素

本文非原创，自己整理下
原文链接： https://www.cnblogs.com/ihardcoder/p/5294927.html

## 伪类(pseudo classes)

伪类存在的意义是为了通过选择器找到那些不存在与DOM树中的信息以及不能被常规CSS选择器获取到的信息。

### 指出CSS3伪类的功能有两种：

1. 获取不存在与DOM树中的信息。比如`<a>`标签的:`link、visited`等，这些信息不存在与DOM树结构中，只能通过CSS选择器来获取；
2. 获取不能被常规CSS选择器获取的信息。比如伪类`:target`，它的作用是匹配文档(页面)的URI中某个标志符的目标元素，例如我们可以通过如下代码来实现页面内的区域跳转

```
<ul class="tabs">
    <li><a href="#tab1">标签一</a></li>
    <li><a href="#tab2">标签二</a></li>
    <li><a href="#tab3">标签三</a></li>
</ul>
<div id="tab1" class="tab_content">
<!--tabed content--></div>
<div id="tab2" class="tab_content">
<!--tabed content--></div>
<div id="tab3" class="tab_content">
<!--tabed content--></div>


CSS代码：
.tab_content {
  height: 800px;
  background: red;
  margin-bottom: 100px;
}
#tab1:target, #tab2:target, #tab3:target {
    background:blue;
}
```

当然，通过JavaScript来获取window.location.hash同样可以实现上例中的效果，但这是另外一回事了。总之，:target通过CSS实现了常规CSS无法实现的逻辑。

通过`:nth-child()`伪类可以实现一些很有意思的效果，比如：

```
table tr:nth-child(2n) td{
   background-color: #ccc;
}
table tr:nth-child(2n+1) td{
   background-color: #fff;
}
table tr:nth-child(2n+1):nth-child(5n) td{
   background-color: #f0f;
}
```

上面的代码将所有偶数行背景色设置为#ccc，不能被5整除的奇数行设置背景色#fff，能够被5整除的奇数行设置背景色#f0f。

如果不使用伪类而是使用JavaScript代码来实现上述的效果，恐怕要复杂很多。

可以总结出:nth-child()伪类的效果是将被常规css选择器筛选出的元素按照既定规定进行再次筛选。

CSS3中还引入了许多新的伪类，感兴趣的可以参考[这里](https://www.w3.org/TR/2011/REC-css3-selectors-20110929/#pseudo-classes)。

## 伪元素(Pseudo-elements)

伪元素在DOM树中创建了一些抽象元素，这些抽象元素是不存在于文档语言里的（可以理解为`html`源码）。比如`：documen`接口不提供访问元素内容的第一个字或者第一行的机制，而伪元素可以使开发者可以提取到这些信息。并且，一些伪元素可以使开发者获取到不存在于源文档中的内容（比如常见的`::before,::after`）。

简单来说，伪元素创建了一个虚拟容器，这个容器不包含任何DOM元素，但是可以包含内容。另外，开发者还可以为伪元素定制样式。

以`::first-line`为例，它获取了指定元素的第一行内容并且将第一行的内容加入到虚拟容器中。如果通过JavaScript来实现这个逻辑，那么要考虑的因素就太多了，比如制定元素的宽度、字体大小，甚至浮动元素的图文混排等等。当然，这些问题确实是可以用JavaScript来解决的，但是相对于::first-line简简单单的几个字，用JavaScript恐怕不止这些吧！

举个例子： 

```
q:lang(de)::after{
    content: " (German) ";
}
q:lang(en)::after{
    content: " (English) ";
}
q:lang(fr)::after{
    content: " (French) ";
}
q:not(:lang(fr)):not(:lang(de)):not(:lang(en))::after{
    content: " (Unrecognized language) ";
}
```
以上代码通过伪类"lang获取不同lang属性的节点，并为之设置伪元素::after，伪元素的内容是此节点的语言类型。

## 最后，总结一下

### 伪类与伪元素的特性及其区别：

1. 伪类本质上是为了弥补常规CSS选择器的不足，以便获取到更多信息；
2. 伪元素本质上是创建了一个有内容的虚拟容器；
3. CSS3中伪类和伪元素的语法不同；
4. 可以同时使用多个伪类，而只能同时使用一个伪元素；


