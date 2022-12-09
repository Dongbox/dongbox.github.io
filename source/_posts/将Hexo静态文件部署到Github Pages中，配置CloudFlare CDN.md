---
title: 将Hexo静态文件部署到Github Pages中，配置CloudFlare CDN
date: 2022-12-09 10:22:19
tags: Hexo
cover: https://images.unsplash.com/photo-1670506552296-668e793daf7a
---

### 新建github仓库并上传基本内容

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

### 参考

- [使用hexo+github免费搭建个人博客网站超详细教程_wapchief的博客-CSDN博客_github hexo](https://blog.csdn.net/wapchief/article/details/54602515)
- 
