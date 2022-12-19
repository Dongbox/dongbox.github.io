---
title: 剑指Offer-03：数组中重复的数字
date: 2022-12-19 20:43:17
tags:
- 查找算法
- Algorithm
- Leetcode
cover: https://images.unsplash.com/photo-1670968982569-81f78c8e841d
---



### 问题

[剑指 Offer 03. 数组中重复的数字 - 力扣（Leetcode）](https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/description/)

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

```python
# 示例
输入：[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```



### 方法：原地交换

> `在一个长度为 n 的数组nums里的所有数字都在 0 ~ n-1 的范围内。这个说明数组元素的 索引 和 值 是 一对多 的关系。`因此，可遍历数组并通过交换操作，使元素的 索引 与 值 一一对应（即 `nums[i]=i`）。因而，就能通过索引映射对应的值，起到与字典等价的作用。

![Picture0.png](https://images-1257166372.cos.ap-shanghai.myqcloud.com/hexo/1618146573-bOieFQ-Picture0.png)

遍历中，第一次遇到数字 `x` 时，将其交换至索引 `x` 处；而当第二次遇到数字 `x` 时，一定有 `nums[x]=x`，此时即可得到一组重复数字。

```python
class Solution:
    def findRepeatNumber(self, nums: [int]) -> int:
        i = 0
        while i < len(nums):
            if nums[i] == i:  # 说明此数字已在对应索引位置，无需交换，因此跳过。
                i += 1
                continue
            if nums[nums[i]] == nums[i]: return nums[i]  # 找到一组重复值，返回此值。
        	# 交换索引为 iii 和 nums[i]nums[i]nums[i] 的元素值，将此数字交换至对应索引位置。
            nums[nums[i]], nums[i] = nums[i], nums[nums[i]]  
        return -1  # 遍历完毕尚未返回，则返回 −1。

```

### 复杂度分析：
时间复杂度 *O(N)* ： 遍历数组使用 O(N) ，每轮遍历的判断和交换操作使用 *O(1)*。
空间复杂度 *O(1)* ： 使用常数复杂度的额外空间。

### 参考

- [剑指 Offer 03. 数组中重复的数字 - 力扣（Leetcode）](https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/solutions/96623/mian-shi-ti-03-shu-zu-zhong-zhong-fu-de-shu-zi-yua/?languageTags=python3)
