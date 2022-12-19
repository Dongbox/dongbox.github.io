---
title: 剑指Offer-58：左旋转字符串
date: 2022-12-19 17:42:27
tags:
- 栈
- Algorithm
- Leetcode
cover: https://images.unsplash.com/photo-1671400833073-0a066e059f44
---

### 问题

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

```python
# 示例
输入: s = "abcdefg", k = 2
输出: "cdefgab"

输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

### 方法：列表遍历拼接

- 新建一个 list(Python)、StringBuilder(Java) ，记为 resresres ；
- 先向 resresres 添加 “第 n+1n + 1n+1 位至末位的字符” ；
- 再向 resresres 添加 “首位至第 nnn 位的字符” ；
- 将 resresres 转化为字符串并返回。

```python
class Solution:
    def reverseLeftWords(self, s: str, n: int) -> str:
        res = []
        for i in range(n, n + len(s)):
            res.append(s[i % len(s)])  # 利用取余操作在遍历(n, len(s))后开始遍历(0, n)
        return ''.join(res)
```

### 复杂度分析

- 时间复杂度 *O(N)* ： 线性遍历 `s` 并添加，使用线性时间；
- 空间复杂度 O(N) ： 假设循环过程中内存会被及时回收，内存中至少同时存在长度为 `N` 和 `N−1` 的两个字符串（新建长度为 `N` 的 `res` 需要使用前一个长度 `N−1` 的 `res`），因此至少使用 *O(N)* 的额外空间。

### 参考

- [剑指 Offer 58 - II. 左旋转字符串 - 力扣（Leetcode）](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/solutions/196453/mian-shi-ti-58-ii-zuo-xuan-zhuan-zi-fu-chuan-qie-p/)





