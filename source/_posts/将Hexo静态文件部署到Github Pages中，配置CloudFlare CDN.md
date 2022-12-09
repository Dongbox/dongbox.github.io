---
title: 将Hexo静态文件部署到Github Pages中，配置CloudFlare CDN
date: 2022-12-09 10:22:19
tags: Hexo
cover: https://images.unsplash.com/photo-1670506552296-668e793daf7a
---

### 新建github仓库

1. 创建一个名为`dongbox.github.io`

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

5. 远程仓库

首先在 Hexo 的仓库中创建一个新文件：`.github/workflows/deploy.yml`，文件名可以自己取，但是一定要放在 `.github/workflows` 目录中，文件的内容如下：

```yml
name: Hexo Deploy

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-18.04
    if: github.event.repository.owner.id == github.event.sender.id

    steps:
      - name: Checkout source
        uses: actions/checkout@v2
        with:
          ref: master

      - name: Setup Node.js
        uses: actions/setup-node@v1
        with:
          node-version: '18'

      - name: Setup Hexo
        env:
          ACTION_DEPLOY_KEY: ${{ secrets.HEXO_DEPLOY_KEY }}
        run: |
          mkdir -p ~/.ssh/
          echo "$ACTION_DEPLOY_KEY" > ~/.ssh/id_rsa
          chmod 700 ~/.ssh
          chmod 600 ~/.ssh/id_rsa
          ssh-keyscan github.com >> ~/.ssh/known_hosts
          git config --global user.email "sfreebobo@163.com"
          git config --global user.name "dongbox"
          npm install hexo-cli -g
          npm install

      - name: Deploy
        run: |
          hexo clean
          hexo deploy
```

### Hexo部署

```bash
$ hexo d
```

### 参考

- [使用hexo+github免费搭建个人博客网站超详细教程_wapchief的博客-CSDN博客_github hexo](https://blog.csdn.net/wapchief/article/details/54602515)
- https://zhuanlan.zhihu.com/p/170563000
