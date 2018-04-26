---
title: Hexo升级大法（1）
date: 2018-04-25 12:08:32
tags: Hexo
categories: Hexo
---

# Hexo 升级之路

  一些不可抗的地球引力原因，打算把个人电脑的一部分MD文件放到博客上，毕竟，这年头，小白就要多学手艺，多一份找工作的机会不是。由于个人的审美以及目的不同，我选择了next这个大名鼎鼎的主题。我的Hexo博客，自打建立之初到现在荒废已久，所以，今天要折腾下，升级的问题。走起吧~

## 第一步，把冰箱门打开，不对，是升级Hexo

很简单(但是我不goole下，我是不知道滴)，进入blog的目录，检查更新：

```
npm outdated
Package                              Current  Wanted  Latest  Location
hexo-deployer-git                      0.2.0   0.2.0   0.3.1  hexo-site
hexo-generator-search                  1.0.4   1.0.4   2.2.1  hexo-site
hexo-generator-seo-friendly-sitemap   0.0.19  0.0.19  0.0.21  hexo-site
hexo-renderer-ejs                      0.2.0   0.2.0   0.3.1  hexo-site
hexo-renderer-marked                  0.2.11  0.2.11   0.3.2  hexo-site
hexo-server                            0.2.2   0.2.2   0.3.1  hexo-site
```
![](https://i.loli.net/2018/04/24/5adf0b5ed1372.png)

根据需要，简单修改一下`package.json`文件：

```
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "hexo": {
    "version": "3.7.1"
  },
  "dependencies": {
    "hexo": "^3.7.1",
    "hexo-deployer-git": "^0.3.1",
    "hexo-generator-archive": "^0.1.4",
    "hexo-generator-category": "^0.1.3",
    "hexo-generator-index": "^0.2.0",
    "hexo-generator-tag": "^0.2.0",
    "hexo-renderer-ejs": "^0.3.0",
    "hexo-renderer-marked": "^0.3.0",
    "hexo-renderer-stylus": "^0.3.1",
    "hexo-server": "^0.3.1"
  }
}
```

把 Hexo 的版本号修改为`3.7.1 `，其他的也根据情况更新一下。

齐活，npm更新一下

` npm install --save`

检查下Hexo

```
hexo version

hexo: 3.7.1
hexo-cli: 1.1.0
os: Darwin 16.7.0 darwin x64
http_parser: 2.7.0
node: 8.9.1
v8: 6.1.534.47
uv: 1.15.0
zlib: 1.2.11
ares: 1.10.1-DEV
modules: 57
nghttp2: 1.25.0
openssl: 1.0.2m
icu: 59.1
unicode: 9.0
cldr: 31.0.1
tz: 2017b
```

## 第二步，把大象装进冰箱，不对，是设置主题

### 下载主题

1. 在终端切换到hexo 根目录. 在hexo目录下一定有 node_modules, source, themes 和其他文件夹:

2. 从 github 上获取主题 。这里有几种方式来获取主题:

    - 在大多数情况下 稳定。 推荐用户下载这个。     
    
    ```
    $ mkdir themes/next
$ curl -s https://api.github.com/repos/iissnan/hexo-theme-next/releases/latest | grep tarball_url | cut -d '"' -f 4 | wget -i - -O- | tar -zx -C themes/next --strip-components=1
    ```
    - 您必须定义版本。从标签列表里选择版本替换v5.1.2。

    ```
    $ mkdir themes/next
$ curl -L https://api.github.com/repos/iissnan/hexo-theme-next/tarball/v5.1.2 | tar -zxv -C themes/next --strip-components=1
    ```


    - 使用克隆命令，你将得到整个存储库。而且在任何时候你都可以切换到任何标签发布版本。 获取标签列表：

    ```
    $ git clone https://github.com/iissnan/hexo-theme-next themes/next
    
    $ cd themes/next
    $ git tag -l
    …
    v5.0.0
    v5.0.1
    v5.1.0
    v5.1.1
    v5.1.2
    ```
    
    例如, 你想要切换到v5.1.0 标签发布版本. 输入以下命令:
    
    ```
    $ git checkout tags/v5.1.0
    Note: checking out 'tags/v5.1.0'.
    …
    HEAD now on 1f72f68... CSS: Remove global list-style setting of ul
    ```
    
    如果你想切换回 master 分支的话, 输入这个命令:
    
    `$ git checkout master`
    
3. 在 hexo 根目录下 的配置文件_config.yml里设置主题:

`theme: next`

### 修改语言

在站点配置文件_config.yml中可以将语言切换成中文

```
language: en
# language: zh-Hans
# language: zh-hk
# language: zh-tw
# language: ru
# language: fr-FR
# language: de
# language: ja
# language: id
# language: pt
# language: pt-BR
# language: ko
# language: it
# language: nl-NL
```

我勒个去，这么简单点事，搞到半夜1点了，真是智商低，睡吧睡吧，猴年马月在补上
