---
title: Hexo升级大法(2)-评论
date: 2018-04-26 22:12:10
tags: Hexo
categories: Hexo
---

# Gitalk

非原创，自己记录下

本文转自：https://asdfv1929.github.io/2018/01/20/gitalk/

`Gitalk` 是一个基于 `Github Issue` 和 `Preact` 开发的评论插件。

## 注册Register Application
在GitHub上注册新应用，链接：https://github.com/settings/applications/new
![](https://i.loli.net/2018/04/26/5ae1c9377aec6.png
)

参数说明：
`Application name：` # 应用名称，随意
`Homepage URL：` # 网站URL，如`https://hermeswu.github.io`
`Application description:` # 描述，随意
`Authorization callback URL：`# 网站URL，`https://hermeswu.github.io`

点击注册后，页面跳转如下，其中`Client ID`和`Client Secret`在后面的配置中需要用到，到时复制粘贴即可：
[![2018-04-26_20-49-05.png](https://i.loli.net/2018/04/26/5ae1caf0331d6.png)](https://i.loli.net/2018/04/26/5ae1caf0331d6.png)

## 配置文件

### gitalk.swig
新建`/layout/_third-party/comments/gitalk.swig`文件，并添加内容：

```
{% if page.comments && theme.gitalk.enable %}
  <link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
  <script src="https://unpkg.com/gitalk/dist/gitalk.min.js"></script>
   <script type="text/javascript">
        var gitalk = new Gitalk({
          clientID: '{{ theme.gitalk.ClientID }}',
          clientSecret: '{{ theme.gitalk.ClientSecret }}',
          repo: '{{ theme.gitalk.repo }}',
          owner: '{{ theme.gitalk.githubID }}',
          admin: ['{{ theme.gitalk.adminUser }}'],
          id: <%= page.date %>,
          distractionFreeMode: '{{ theme.gitalk.distractionFreeMode }}'
        })
        gitalk.render('gitalk-container')           
       </script>
{% endif %}
```
### comments.swig
修改`/layout/_partials/comments.swig`，添加内容如下，与前面的elseif同一级别上：

```
{% elseif theme.gitalk.enable %}
 <div id="gitalk-container"></div>

```
### index.swig
修改`layout/_third-party/comments/index.swig`，在最后一行添加内容

```
{% include 'gitalk.swig' %}
```
### gitalk.styl
新建`/source/css/_common/components/third-party/gitalk.styl`文件，添加内容：

```
.gt-header a, .gt-comments a, .gt-popup a
  border-bottom: none;
.gt-container .gt-popup .gt-action.is--active:before
  top: 0.7em;
```
### third-party.styl
修改`/source/css/_common/components/third-party/third-party.styl`，在最后一行上添加内容，引入样式：

```
@import "gitalk";
```
### _config.yml
在主题配置文件`next/_config.yml`中添加如下内容：

```
gitalk:
  enable: true
  githubID: github帐号  # 例：HermesWu  
  repo: 仓库名称   # 例：HermesWu.github.io
  ClientID: Client ID
  ClientSecret: Client Secret
  adminUser: github帐号 #指定可初始化评论账户
  distractionFreeMode: true
```

以上就是NexT中添加gitalk评论的配置，博客上传到GitHub上后，打开页面进入某一博客内容下，就可看到评论处。

# 更新：
## 解决：gitalk 报错 Error: Validation Failed.--MD5 加密 id 避免 github issue lables 50 字符限制
1. 创建一个`github gist` 文件保存 https://github.com/blueimp/JavaScript-MD5/blob/master/js/md5.min.js `js` 源码：
https://gist.githubusercontent.com/qhh0205/78e9e0b1f3114db6737f3ed8cdd51d3a/raw/3894c5be5aa2378336b1f5ee0f296fa0b22d06e9/md5.min.js
2. 将 `gist` 链接嵌入到 `layout/_third-party/comments/gitalk.swig` 文件，嵌入时的 `js` 链接地址需要注意下：
不能直接写第一步的创建的 `gitst` 链接地址，需要将 `gist.githubusercontent.com` 替换为 `rawgit.com`。即嵌入地址为: https://rawgit.com/qhh0205/78e9e0b1f3114db6737f3ed8cdd51d3a/raw/3894c5be5aa2378336b1f5ee0f296fa0b22d06e9/md5.min.js
最终 `layout/_third-party/comments/gitalk.swig` 配置如下：

```
{% if page.comments && theme.gitalk.enable %}
  <link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
  <script src="https://unpkg.com/gitalk/dist/gitalk.min.js"></script>
  <script src="https://rawgit.com/qhh0205/78e9e0b1f3114db6737f3ed8cdd51d3a/raw/3894c5be5aa2378336b1f5ee0f296fa0b22d06e9/md5.min.js"></script>
   <script type="text/javascript">
        var gitalk = new Gitalk({
          clientID: '3840ba8c8d80c18be7e3',
          clientSecret: '1b00f2efe5285973c24da9ed9ac895775eacc8ea',
          repo: '{{ theme.gitalk.repo }}',
          owner: '{{ theme.gitalk.githubID }}',
          admin: ['{{ theme.gitalk.adminUser }}'],
          id: md5(location.pathname),
          distractionFreeMode: '{{ theme.gitalk.distractionFreeMode }}'
        })
        gitalk.render('gitalk-container')
    </script>
{% endif %}
```




