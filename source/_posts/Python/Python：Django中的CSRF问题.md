---
title: Python：Django中的CSRF问题
date: 2022-12-10 17:16:23
tags:
- Python面试题
- Django
categories: Python
cover: https://images.unsplash.com/photo-1661366050919-a14b46efee21
---

### CORS简介

CORS是一种允许与托管在不同域上的资源进行交互的机制。例如，应用它的最常见场景之一是Ajax请求。

为了说明CORS是如何工作的，让我们假设您有一个位于domain.com中的web应用程序。但是，为了保存用户信息，应用程序调用部署在另一个url中的API，例如api.domain.com。因此，当将保存数据的请求发送到api.domain.com时，服务器将根据请求的头信息和请求的来源来校验请求。

如果允许服务器中的URL domain.com，它将提供正确的响应。如果不允许该域，服务器将抛出一个异常。此信息交换使用HTTP报头进行。

如果有CORS的需要，可以直接安装`corsheaders`

```bash
pip install django-cors-headers 
```

### CSRF简介

CSRF（Cross-site request forgery），中文名称：跨站请求伪造，也被称为：one click attack/session riding，缩写为：CSRF/XSRF。

##### 模板请求

在Django中，如果是直接使用模板来定义的话，那么可以直接声明：

```python
{ % csrf_token % }
```

##### Ajax请求

csrftoken这个值可以从cookie的`csrftoken`获取到。

验证则有两种方式进行：

- 在请求头中定义`X-CSRFToken`参数。

- 在数据中定义`csrf_token`属性一同传过去

### 

### 参考文章

- [Django CORS Guide: What It Is and How to Enable It (stackhawk.com)](https://www.stackhawk.com/blog/django-cors-guide/)
