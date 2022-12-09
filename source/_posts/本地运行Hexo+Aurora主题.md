---
title: 如何部署Hexo到github
date: 2022-12-07 08:15:36
tags: Hexo
cover: https://images.unsplash.com/photo-1666126444655-23492b1532e2

---

## 过程

### 一、配置基本环境

```bash
$ npm install hexo-cli -g
$ hexo init blog
$ cd blog
$ npm install
$ npm install hexo-theme-aurora --save
$ npm install hexo-deployer-git -save
```

### 二、根据文档修改相应配置

[Aurora官方文档地址](https://aurora.tridiamond.tech/guide/getting-started.html#installation)

```bash
$ cd blog
$ cp ./node_modules/hexo-theme-aurora/_config.yml ./_config.aurora.yml

打开`_config.yml`文件开始修改配置
```

#### Step 1：修改`permalink`为`/post/:title.html`

```yml
# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
url: https://tridiamond.tech
permalink: /post/:title.html
permalink_defaults:
pretty_urls:
  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
  trailing_html: true # Set to false to remove trailing '.html' from permalinks
```

#### Step 2：修改`highlight`为`false`，`prismjs`为`true`

```yml
highlight:
  enable: false
  line_number: true
  auto_detect: false
  tab_replace: ''
  wrap: true
  hljs: false
prismjs:
  enable: true
  preprocess: true
  line_number: true
  tab_replace: ''
```

#### Step 3： 新建一个关于页面

```bash
$ hexo new page about
```

#### Step 4: 生成资源以及检测能否正常部署

```bash
$ hexo clean
$ hexo g
$ hexo server
```

## 参考链接

- 
- https://hexo.io/zh-cn/
- [Theme | Hexo Aurora (tridiamond.tech)](https://aurora.tridiamond.tech/guide/theme.html)