---
title: 剑指Offer-53：在排序数组中查找数字Ⅰ
date: 2022-12-19 21:10:48
tags:
- 查找算法
- Algorithm
- Leetcode
cover: https://images.unsplash.com/photo-1670515258571-29149b266666
---

### 问题

[剑指 Offer 53 - I. 在排序数组中查找数字 I - 力扣（Leetcode）](https://leetcode.cn/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/description/)

统计一个数字在排序数组中出现的次数。

```python
# 示例
输入: nums = [5,7,7,8,8,10], target = 8
输出: 2

输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
```

### 方法：二分法

> 有序数组中的搜索问题，首先想到 **二分法** 解决。

由于这是一个有序数组并且数组 `nums` 中元素都为整数，因此可以分别二分查找 `target` 和 `target−1` 的右边界，将两结果相减并返回即可。本质上看， `helper()` 函数旨在查找数字 `tar` 在数组 `nums` 中的 插入点 ，且若数组中存在值相同的元素，则插入到这些元素的右边。

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        def helper(tar):
            l, r = 0, len(nums) - 1
            while l <= r:
                m = (l + r) // 2
                if nums[m] <= tar: l = m + 1  # 缩小边界，直到 l=r。
                else: r = m -1
            return l
        return helper(target) - helper(target - 1)

```

### 复杂度分析

- 时间复杂度 `O(logN)` ： 二分法为对数级别复杂度。
- 空间复杂度 `O(1)`： 几个变量使用常数大小的额外空间。

### 参考

- [剑指 Offer 53 - I. 在排序数组中查找数字 I - 力扣（Leetcode）](https://leetcode.cn/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/solutions/155893/mian-shi-ti-53-i-zai-pai-xu-shu-zu-zhong-cha-zha-5/?languageTags=python3)
