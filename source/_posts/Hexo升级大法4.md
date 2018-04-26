---
title: Hexo升级大法(4)-添加结尾标题
date: 2018-04-26 22:32:56
tags: Hexo
categories: Hexo
---

# 给文章后面添加结束标语

原文链接：https://asdfv1929.github.io/2018/01/28/add-the-end/

## 新建文件
在`\themes\next\layout\_macro`中新建`passage-end-tag.swig`文件，添加代码至该文件中：

```
<div>
    {% if not is_index %}
        <div style="text-align:center;color: #ccc;font-size:14px;">-------------本文结束<i class="fa fa-paw"></i>感谢您的阅读-------------</div>
    {% endif %}
</div>
```
## 修改`post.swig`
打开`\themes\next\layout\_macro\post.swig`文件，在`post-body`后，`post-footer`前，添加下面内容：

```
<div>
  {% if not is_index %}
    {% include 'passage-end-tag.swig' %}
  {% endif %}
</div>
```

## 修改`_config`
打开主题配置文件`（_config.yml)`,在末尾添加：

```
# 文章末尾添加“本文结束”标记
passage_end_tag:
  enabled: true
```

齐活，自己发挥下，搞个有意思的结尾吧。

