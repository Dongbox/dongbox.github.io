---
title: Python：Python2与Python3
date: 2022-12-10 21:20:33
tags: Python
categories: Python面试题
cover: https://images.unsplash.com/photo-1670258897358-1e0347859dab
---

- `print()` vs `print`

- Unicode vs ASCII

- 除法：浮点 vs 整数

- `StandardError`废弃，统一使用`Exception`；raise去除`raise IOError, ""`格式，统一为`raise IOError("file str")`

- `range` vs `xrange`

- 去除`<>`不等运算符，统一为`!=`

- 去除long类型

- 新增了bytes

- 去除`.next()`方法

- dict的has_key()方法被去掉

- dictiionary的keys()、values()、items()、zip()、map()、filter()不再直接返回list对象，但可以强制转换。

### 参考文章

- [深入浅析Python2.x和3.x版本的主要区别 _ 搞代码 (gaodaima.com)](http://www.gaodaima.com/162209.html)
