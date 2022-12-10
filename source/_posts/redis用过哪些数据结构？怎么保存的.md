---
title: redis用过哪些数据结构？怎么保存的?
date: 2022-12-09 20:15:37
tags: 
cover: https://images.unsplash.com/photo-1666126444655-23492b1532e2
---

### Redis 的五种基本数据类型

#### String（字符串）

简介:String是Redis最基础的数据结构类型，它是二进制安全的，可以存储图片或者序列化的对象，值最大存储为512M

简单使用举例: set key value、get key等

应用场景：共享session、分布式锁，计数器、限流。

内部编码有3种，int（8字节长整型）/embstr（小于等于39字节字符串）/raw（大于39个字节字符串）

#### Hash（哈希）

简介：在Redis中，哈希类型是指v（值）本身又是一个键值对（k-v）结构

简单使用举例：hset key field value 、hget key field

内部编码：ziplist（压缩列表） 、hashtable（哈希表）

应用场景：缓存用户信息等。

#### List（列表）

简介：列表（list）类型是用来存储多个有序的字符串，一个列表最多可以存储2^32-1个元素。

简单实用举例：lpush key value [value ...] 、lrange key start end

内部编码：ziplist（压缩列表）、linkedlist（链表）

应用场景：消息队列，文章列表

#### Set（集合）

简介：集合（set）类型也是用来保存多个的字符串元素，但是不允许重复元素

简单使用举例：sadd key element [element ...]、smembers key

内部编码：intset（整数集合）、hashtable（哈希表）

应用场景：用户标签,生成随机数抽奖、社交需求。

#### 有序集合（zset）

简介：已排序的字符串集合，同时元素不能重复

简单格式举例：zadd key score member [score member ...]，zrank key member

底层内部编码：ziplist（压缩列表）、skiplist（跳跃表）

应用场景：排行榜，社交需求（如用户点赞）。

#### Redis 的三种特殊数据类型

- Geo：Redis3.2推出的，地理位置定位，用于存储地理位置信息，并对存储的信息进行操作。

- HyperLogLog：用来做基数统计算法的数据结构，如统计网站的UV。

- Bitmaps ：用一个比特位来映射某个元素的状态，在Redis中，它的底层是基于字符串类型实现的，可以把bitmaps成作一个以比特位为单位的数组

![5c1c1527bbc9954851162895ec3f47f2.png](https://img-blog.csdnimg.cn/img_convert/5c1c1527bbc9954851162895ec3f47f2.png)

在redisObject中 **[type表示属于哪种数据类型，encoding表示该数据的存储方式]**，也就是底层的实现的该数据类型的数据结构，ptr则是指向数据的存储。

encoding中的存储类型所表示的含义如下图所示：

![](https://img-blog.csdnimg.cn/img_convert/9ae120adbd08bc2393d0bd846714e4dd.png)

### 数据的存储

String类型的数据结构存储方式有三种int、raw、embstr。

Redis中规定假如存储的是 **[整数型值]**，比如set num 123这样的类型，就会使用 int的存储方式进行存储，在redisObject的**[ptr属性]**中就会保存该值。

![84880f95ccff808c1e172aa4f1718013.png](https://img-blog.csdnimg.cn/img_convert/84880f95ccff808c1e172aa4f1718013.png)

#### SDS

假如存储的**[字符串是一个字符串值并且长度大于32个字节]**就会使用SDS(simple dynamic string)方式进行存储，并且encoding设置为raw；若是**[字符串长度小于等于32个字节]**就会将encoding改为embstr来保存字符串。

![1650938b53726c698463efc2a2d21414.png](https://img-blog.csdnimg.cn/img_convert/1650938b53726c698463efc2a2d21414.png)

### 参考文章

- [redis 超详细的Redis五种数据结构详解（理论+实战） - DoubleLi - 博客园 (cnblogs.com)](https://www.cnblogs.com/lidabo/p/16673547.html)

- [每日一问：Redis有几种数据结构,底层分别是怎么存储的？_星仔学习的博客-CSDN博客](https://blog.csdn.net/u012868901/article/details/122926726)

- [Redis源码解析之SDS（缓存面试加分项） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/467043930)
