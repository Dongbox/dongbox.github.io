---
title: ModelFirst与DBFirst
date: 2022-12-10 10:43:08
tags: Database
categories: Python面试题
cover: https://images.unsplash.com/photo-1669092160303-1e79fdff702d
---

> EF（Entity Framework（实体框架））是微软出品的用来操作数据库的一个框架。  

EF 的三种设计模型：CodeFirst，ModelFirst，DBFirst。  
**ModelFirst**是首先设计实体模型，之后根据实体模型实现到数据库的映射。**DBFirst**是先进行数据库的设计，之后根据数据库生成实体数据模型。

EF 框架的原理就是把实体类的变化通过映射反应到数据库中去，实现表的增删改查。对象上下文是实体类操作数据库的API。应用程序对实体类进行的增删改查操作会经由对象上下文进行映射，最终转换为 SQL 脚本语言，然后执行，最终实现对表的增删改查。当需要修改表的结构时，我们可以选择根据模型更新数据库和根据数据库更新模型两种。

### 参考文章

- [Python面试笔记-pudn.com](https://www.pudn.com/news/6236e3cd5810f120f037b2c1.html)
