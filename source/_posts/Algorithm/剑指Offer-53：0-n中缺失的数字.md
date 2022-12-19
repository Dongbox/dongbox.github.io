---
title: 剑指Offer-53：0~n中缺失的数字
date: 2022-12-19 21:26:25
tags:
- 查找算法
- Algorithm
- Leetcode
cover: https://images.unsplash.com/photo-1657444984080-5c08464bde8c
---

### 问题

[剑指 Offer 53 - II. 0～n-1中缺失的数字 - 力扣（Leetcode）](https://leetcode.cn/problems/que-shi-de-shu-zi-lcof/description/?envType=study-plan&id=lcof&plan=lcof&plan_progress=y8llrks)

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

```python
# 示例
输入: [0,1,3]
输出: 2

输入: [0,1,2,3,4,5,6,7,9]
输出: 8
```

### 方法：二分法

根据题意，数组可以按照以下规则划分为两部分。

- 左子数组： `nums[i]=i`；
- 右子数组： `nums[i]≠i`

缺失的数字等于 **“右子数组的首位元素”** 对应的索引；因此考虑使用二分法查找 “右子数组的首位元素” 。

```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        l, r = 0, len(nums) - 1
        while l <= r:
            m = (l + r) // 2
            if nums[m] == m: l = m + 1  # “右子数组的首位元素” 一定在闭区间 [m+1,j] 中。
            else: r = m - 1  # ”左子数组的末位元素” 一定在闭区间 [i,m−1]中。
        return l
```

### 复杂度分析
- 时间复杂度 *O(logN)*： 二分法为对数级别复杂度。
- 空间复杂度 *O(1)*： 几个变量使用常数大小的额外空间。

### 参考

- [剑指 Offer 53 - II. 0～n-1中缺失的数字 - 力扣（Leetcode）](https://leetcode.cn/problems/que-shi-de-shu-zi-lcof/solutions/155915/mian-shi-ti-53-ii-0n-1zhong-que-shi-de-shu-zi-er-f/?languageTags=python3)
