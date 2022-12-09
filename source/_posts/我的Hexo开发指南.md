---
title: 我的Hexo开发指南
date: 2022-12-09 10:10:33
tags: Hexo
cover: https://images.unsplash.com/photo-1670401781625-9eac9c7aaab2
---

### 简介

作为一个Hexo小白，现在我想要拥有一个Hexo的Aurora主题的博客网站，同时我还有一个域名（dongbox.space），我想通过这个域名访问到我的Hexo静态资源，但我没有服务器，所以我打算直接部署在pages服务上，我选择了Github Pages，整个部署过程会分为三部分：

1. 本地运行Hexo+Aurora主题

2. 将Hexo静态文件部署到Github Pages中，配置CloudFlare CDN

3. Hexo优化

## 1. 本地运行Hexo+Aurora主题

#### 一、配置基本环境

```bash
$ npm install hexo-cli -g
$ hexo init blog
$ cd blog
$ npm install
$ npm install hexo-theme-aurora --save
$ npm install hexo-deployer-git -save
```

#### 二、根据文档修改相应配置

[Aurora官方文档地址](https://aurora.tridiamond.tech/guide/getting-started.html#installation)

```bash
$ cd blog
$ cp ./node_modules/hexo-theme-aurora/_config.yml ./_config.aurora.yml

打开`_config.yml`文件开始修改配置
```

##### Step 1：修改`permalink`为`/post/:title.html`

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

##### Step 2：修改`highlight`为`false`，`prismjs`为`true`

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

##### Step 3： 新建一个关于页面

```bash
$ hexo new page about
```

##### Step 4: 生成资源以及检测能否正常部署

```bash
$ hexo clean
$ hexo g
$ hexo server
```

#### 参考文章

- [Hexo](https://hexo.io/zh-cn/)
- [Theme | Hexo Aurora (tridiamond.tech)](https://aurora.tridiamond.tech/guide/theme.html)

### 2. 将Hexo静态文件部署到Github Pages中，配置CloudFlare CDN

#### 一、将Hexo静态文件部署到Github Pages中

1. 创建一个名为`dongbox.github.io`的公共仓库

2. 链接本地Hexo项目到github仓库
   
   ```bash
   # 进入项目目录，此处更换为你的Hexo项目名称
   cd blog
   # 实例化本地仓库
   git init
   # 链接仓库，此处更换为你的仓库地址
   git remote add origin https://github.com/Dongbox/dongbox.github.io.git
   ```

3. 修改配置文件`_config.yml`中的远程仓库地址
   
   ```yml
   deploy:
   type: git
   repo: https://github.com/Dongbox/dongbox.github.io.git
   branch: main
   ```

4. 发布到Hexo
   
   ```bash
   hexo clean && hexo g && hexo d
   ```

5. 上传源码到远程仓库
   
   除了静态文件，我们还要上传Hexo源码文件。
   
   ```bash
   # 创建一个新的分支hexo
   git checkout -b hexo
   # 添加文件到本地仓库
   git add .
   # 提交声明
   git commit -m '内容'
   # 推送源码到hexo分支
   git push origin hexo
   ```

### 二、配置CloudFlare CDN

#### 参考文章

- [基于 Hexo 的 GitHub Pages 配置 CloudFlare CDN_qhh0205的博客-CSDN博客](https://blog.csdn.net/qianghaohao/article/details/83714575)

- [cloudflare加速博客网站出现“此页面不能正确地重定向”的解决办法_喆旭电科的博客-CSDN博客_如何解决cloudflare](https://blog.csdn.net/bcnchina/article/details/106032854)
