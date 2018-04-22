---
title: sh任务
date: 2018-03-12 17:43:39
tags:
---
#### 代码如下

```
if [ -d $1 ]; then
 echo ‘$! 已经存在’
 exit
else
 mkdir $1
 cd $1
 mkdir css js
 touch index.html css/style.css js/main.js
 echo \<\!DOCTYPE\> >> index.html
 echo \<title\>hello\</title\> >> index.html
 echo \<h1\>Hi\</h1\> >> index.html
 echo h1\{color\: red\;\} >> css/style.css
 echo var string \= \”Hello World\” >> js/main.js
 echo alert\(string\) >> js/main.js
exit
fi

```

