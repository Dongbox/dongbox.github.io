---
title: 简述一个前端请求的处理流程，uWSGI/nginx/django之间的处理流程
date: 2022-12-09 14:07:57
tags: 
- Python
- HTTP
- Django
categories: Python面试题
cover: https://images.unsplash.com/photo-1666625628272-a1071f6f7173
---

### Nginx

- 资源缓存

- 负载均衡

- 方向代理

- 缓存请求

- 提高并发

### WSGI

**Web服务器网关接口**（**Python Web Server Gateway Interface**，缩写为WSGI）是为[Python](https://baike.baidu.com/item/Python?fromModule=lemma_inlink)语言定义的[Web服务器](https://baike.baidu.com/item/Web%E6%9C%8D%E5%8A%A1%E5%99%A8?fromModule=lemma_inlink)和Web应用程序或[框架](https://baike.baidu.com/item/%E6%A1%86%E6%9E%B6?fromModule=lemma_inlink)之间的一种简单而通用的[接口](https://baike.baidu.com/item/%E6%8E%A5%E5%8F%A3?fromModule=lemma_inlink)

### Django的内部处理流程

![在这里插入图片描述](https://img-blog.csdnimg.cn/641a6fc4430a475683783ff96238024b.png#pic_center)

- 用户浏览器发起http请求

- 请求首先到达 Request Middleware 中间件，它能在views 收到请求前对Request消息内容进行处理，发送响应。

- urls.py 中的 URLConf 对收到请求的url进行匹配，找到相应的视图处理函数或视图类。

- 在View收到请求之前，View Middlewares 被调用， 可以进行一些预处理。

- 视图函数或视图类被调用，视图函数可能访问模型数据 or 调用 form 生成表单对象。

- 所有 model-to-DB 的交互都通过 manager 对象来完成。

- Views 可通以通过context 对象来添加更多传给模板的内容，Views 将 context 上下文数据传给模板进行渲染。

- 模板层使用 Filter与 Tags 渲染输出。

- 模板层将渲染结果 传回给 视图层。

- 视图层发送HTTPResponse 给Response Middlerwares 中间件。

- Ｒesponse middlewares中间件可以向　Response 消息添加额外内容，或者用1个新消息替代。

- wsgi 网关发送 response 给用户浏览器。

#### 参考文章

- [尝试理解Flask源码 之 搞懂WSGI协议 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/46983059)

- [一张图读懂 Django Web请求处理的完整流程_雕弓的博客-CSDN博客_django 消息](https://blog.csdn.net/captain5339/article/details/127691229)

- [【web前端】详解Tornado web框架！ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/172514847)
