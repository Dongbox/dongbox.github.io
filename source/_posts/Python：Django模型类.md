---
title: Python：Django模型类
date: 2022-12-10 16:17:36
tags:
- Python面试题
- Django
categories: Python
cover: https://images.unsplash.com/photo-1658953229664-e8d5ebd039ba
---

### ORM简介

ORM，全称Object Relational MAPPing，中文叫做对象关系映射，通过ORM我们可以通过类的方式去操作数据库，而不用再写原生的SQL语句。通过把表映射成类，把行作实例，把字段作为属性，ORM在执行对象操作的时候最终还是会把对应的操作转换为数据库原生语句。使用ORM有许多优点：

**易用性**：使用ORM做数据库的开发可以有效的减少重复SQL语句的概率，写出来的模型也更加直观、清晰。

**性能损耗小**：ORM转换成底层数据库操作指令确实会有一些开销。但从实际的情况来看，这种性能损耗很少（不足5%），只要不是对性能有严苛的要求，综合考虑开发效率、代码的阅读性，带来的好处要远远大于性能损耗，而且项目越大作用越明显。

**设计灵活**：可以轻松的写出复杂的查询。

**可移植性**：Django封装了底层的数据库实现，支持多个关系数据库引擎，包括流行的MySQL、PostgreSQL和SQLite。可以非常轻松的切换数据库

#### 参考文章

- [Pycharm开发Django的ORM模型介绍 - 哔哩哔哩 (bilibili.com)](https://www.bilibili.com/read/cv13480671/)

### 模型类继承

一共有三种继承模式：

- 抽象基类

- 多表继承

- 代理模型

#### 1. 抽象基类

该模型将不会创建任何数据表。当其用作其它模型类的基类时，它的字段会自动添加至子类。

```python
from django.db import models

class CommonInfo(models.Model):
    name = models.CharField(max_length=100)
    age = models.PositiveIntegerField()

    class Meta:
        abstract = True  # Meta中声明为基类
```

 `CommonInfo` 模型不能用作普通的 Django 模型，因为它是一个抽象基类。它不会生成数据表，也没有管理器，也不能被实例化和保存。

从抽象基类继承来的字段可被其它字段或值重写，或用 `None` 删除。

**Meta继承**

当一个抽象基类被建立，Django 将所有你在基类中申明的 [Meta](https://docs.djangoproject.com/zh-hans/4.1/topics/db/models/#meta-options) 内部类以属性的形式提供。若子类未定义自己的 [Meta](https://docs.djangoproject.com/zh-hans/4.1/topics/db/models/#meta-options) 类，它会继承父类的 [Meta](https://docs.djangoproject.com/zh-hans/4.1/topics/db/models/#meta-options)。当然，子类也可继承父类的 [Meta](https://docs.djangoproject.com/zh-hans/4.1/topics/db/models/#meta-options)，比如:

```python
from django.db import models

class CommonInfo(models.Model):
    # ...
    class Meta:
        abstract = True
        ordering = ['name']

class Student(CommonInfo):
    # ...
    class Meta(CommonInfo.Meta):
        db_table = 'student_info'
```

> Django 在实例化 [Meta](https://docs.djangoproject.com/zh-hans/4.1/topics/db/models/#meta-options) 属性前，对抽象基类的 [Meta](https://docs.djangoproject.com/zh-hans/4.1/topics/db/models/#meta-options) 做了一个调整——设置 `abstract=False`。因此抽象基类的子类不会自动地变成抽象类。

如果子类从多个抽象基类继承，则默认情况下仅继承第一个列出的类的 [Meta](https://docs.djangoproject.com/zh-hans/4.1/topics/db/models/#meta-options) 选项。为了从多个抽象类中继承 [Meta](https://docs.djangoproject.com/zh-hans/4.1/topics/db/models/#meta-options) 选项，必须显式地声明 [Meta](https://docs.djangoproject.com/zh-hans/4.1/topics/db/models/#meta-options) 继承。

```python
...
class Unmanaged(models.Model):
    class Meta:
        abstract = True
        managed = False

class Student(CommonInfo, Unmanaged):
    home_group = models.CharField(max_length=5)

    class Meta(CommonInfo.Meta, Unmanaged.Meta):
        pass
```

#### 2. 多表继承

Django 支持的第二种模型继承方式是层次结构中的每个模型都是一个单独的模型。每个模型都指向分离的数据表，且可被独立查询和创建。

> 可以理解为自动创建了一个OneToOneField。

```python
from django.db import models

class Place(models.Model):
    name = models.CharField(max_length=50)
    address = models.CharField(max_length=80)

class Restaurant(Place):
    serves_hot_dogs = models.BooleanField(default=False)
    serves_pizza = models.BooleanField(default=False)
```

`Place` 的所有字段均在 `Restaurant` 中可用，虽然数据分别存在不同的表中。所有，以下操作均可:

```python
>>> Place.objects.filter(name="Bob's Cafe")
>>> Restaurant.objects.filter(name="Bob's Cafe")
```

若有一个 `Place` 同时也是 `Restaurant`，你可以通过小写的模型名将 `Place` 对象转为 `Restaurant` 对象。

```python
>>> p = Place.objects.get(id=12)
# If p is a Restaurant object, this will give the child class:
>>> p.restaurant
<Restaurant: ...>
```

然而，若上述例子中的 `p` *不是* 一个 `Restaurant` （它仅是个 `Place` 对象或是其它类的父类），指向 `p.restaurant` 会抛出一个 `Restaurant.DoesNotExist` 异常。

`Restaurant` 中自动创建的连接至 `Place` 的 [`OneToOneField`](https://docs.djangoproject.com/zh-hans/4.1/ref/models/fields/#django.db.models.OneToOneField "django.db.models.OneToOneField") 看起来像这样:

```python
place_ptr = models.OneToOneField(
    Place, on_delete=models.CASCADE,
    parent_link=True,
    primary_key=True,
)
```

> 你可以在 `Restaurant` 中重写该字段，通过申明你自己的 [`OneToOneField`](https://docs.djangoproject.com/zh-hans/4.1/ref/models/fields/#django.db.models.OneToOneField "django.db.models.OneToOneField")，并设置 [`parent_link=True`](https://docs.djangoproject.com/zh-hans/4.1/ref/models/fields/#django.db.models.OneToOneField.parent_link "django.db.models.OneToOneField.parent_link")。

##### 关于多表继承中的Meta

多表继承情况下，子类不会继承父类的 [Meta](https://docs.djangoproject.com/zh-hans/4.1/topics/db/models/#meta-options)

因此子类模型无法访问父类的 [Meta](https://docs.djangoproject.com/zh-hans/4.1/topics/db/models/#meta-options) 类。不过，有限的几种情况下：若子类未指定 [`ordering`](https://docs.djangoproject.com/zh-hans/4.1/ref/models/options/#django.db.models.Options.ordering "django.db.models.Options.ordering") 属性或 [`get_latest_by`](https://docs.djangoproject.com/zh-hans/4.1/ref/models/options/#django.db.models.Options.get_latest_by "django.db.models.Options.get_latest_by") 属性，子类会从父类继承这些。

#### 3. 代理模型

使用 [多表继承](https://docs.djangoproject.com/zh-hans/4.1/topics/db/models/#multi-table-inheritance) 时，每个子类模型都会创建一张新表。这一般是所期望的行为，因为子类需要一个地方存储基类中不存在的额外数据字段。不过，有时候你只想修改模型的部分属性——比如修改默认管理器，或添加一个方法。

这个时候就是代理模型出手的时候了，为原模型创建一个 *代理*。你可以创建，删除和更新代理模型的实例，所以的数据都会存储的像你使用原模型（未代理的）一样。不同点是你可以修改代理默认的模型排序和默认管理器，而不需要修改原模型。

```python
from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)

class MyPerson(Person):
    class Meta:
        proxy = True

    def do_something(self):  # 添加一个方法，但仍然和父类操作的是同一张表
        # ...
        pass
```

`MyPerson` 类与父类 `Person` 操作同一张数据表。特别提醒， `Person` 的实例能通过 `MyPerson` 访问，反之亦然。

```python
>>> p = Person.objects.create(first_name="foobar")
>>> MyPerson.objects.get(first_name="foobar")
<MyPerson: foobar>
```

也可以只是简单修改下排序模式，比如代理模型按照`last_name`进行排序。

```python
class OrderedPerson(Person):
    class Meta:
        ordering = ["last_name"]
        proxy = True
```

那么普通的 `Person` 查询结果不会被排序，但 `OrderdPerson` 查询接轨会按 `last_name` 排序。

**基类约束**

一个代理模型必须继承自一个非抽象模型类。你不能继承多个非抽象模型类，因为代理模型无法在不同数据表之间提供任何行间连接。一个代理模型可以继承任意数量的抽象模型类，假如他们 *没有* 定义任何的模型字段。一个代理模型也可以继承任意数量的代理模型，只需他们共享同一个非抽象父类。

**代理模型管理器**

若你未在代理模型中指定模型管理器，它会从父类模型中继承。如果你在代理模型中指定了管理器，它会成为默认管理器，但父类中定义的管理器仍是可用的。

```python
from django.db import models

class NewManager(models.Manager):
    # ...
    pass

class MyPerson(Person):
    objects = NewManager()

    class Meta:
        proxy = True
```

#### 时间模型类

pip install django-model-utils

[项目地址](https://github.com/jazzband/django-model-utils)

### 参考文章

- [模型 | Django 文档 | Django](https://docs.djangoproject.com/zh-hans/4.1/topics/db/models/#model-inheritance)

- [Django扩展用户模型_不负韶华ღ的博客-CSDN博客_django扩展用户](https://blog.csdn.net/weixin_49346755/article/details/117931249)
