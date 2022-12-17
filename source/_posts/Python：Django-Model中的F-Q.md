---
title: 'Python: Django Model中的F&Q'
date: 2022-12-13 22:47:48
tags:
- Python面试题
- Django
categories: Python
cover: https://images.unsplash.com/photo-1669045236900-9988510e0e69
---

## 关于F

F作用：操作数据表中的某列值，也就是数据库中的某个字段，F()允许Django在未实际链接数据的情况下具有对数据库字段的值的引用，不用获取对象放在内存中再对字段进行操作，直接执行原生产[sql语句](https://so.csdn.net/so/search?q=sql%E8%AF%AD%E5%8F%A5&spm=1001.2101.3001.7020)操作

使用场景：对数据库中的所有的商品，在原价格的基础上涨价10元

```python
from django.db.models import F
from app01.models import Book
Book.objects.update(price=F("price")+20)  # 对于book表中每本书的价格都在原价格的基础上增加20元
```

## 关于Q

Q作用：对对象进行复杂查询，并支持&（and）,|（or），~（not）操作符

使用场景：filter查询条件只有一个，而使用Q可以设置多个查询条件

```python
from django.db.models import Q
search_obj=Asset.objects.filter(Q(hostname__icontains=keyword)|Q(ip=keyword))
```

## 参考文章

- [Django中F和Q的区别_Tubby__的博客-CSDN博客_django f q](https://blog.csdn.net/Tubby__/article/details/105069594)
