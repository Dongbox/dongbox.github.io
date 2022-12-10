---
title: 简述一个前端请求的处理流程，uWSGI/nginx/django之间的处理流程
date: 2022-12-09 14:07:57
tags: 
cover: https://images.unsplash.com/photo-1666625628272-a1071f6f7173
---

WSGI

**Web服务器网关接口**（**Python Web Server Gateway Interface**，缩写为WSGI）是为[Python](https://baike.baidu.com/item/Python?fromModule=lemma_inlink)语言定义的[Web服务器](https://baike.baidu.com/item/Web%E6%9C%8D%E5%8A%A1%E5%99%A8?fromModule=lemma_inlink)和Web应用程序或[框架](https://baike.baidu.com/item/%E6%A1%86%E6%9E%B6?fromModule=lemma_inlink)之间的一种简单而通用的[接口](https://baike.baidu.com/item/%E6%8E%A5%E5%8F%A3?fromModule=lemma_inlink)

#### 参考文章

- [尝试理解Flask源码 之 搞懂WSGI协议 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/46983059)

- 
