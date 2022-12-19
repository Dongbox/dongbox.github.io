---
title: 剑指Offer-06：从尾到头打印链表
date: 2022-12-19 16:03:03
tags:
- 链表
- Algorithm
- Leetcode
cover:
---



### 问题

[剑指 Offer 06. 从尾到头打印链表 - 力扣（Leetcode）](https://leetcode.cn/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/description/)

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

```python
# 示例
输入：head = [1,3,2]
输出：[2,3,1]
```

### 方法：辅助栈法

#### 算法流程：

- 入栈： 遍历链表，将各节点值 push 入栈。（Python 使用 append() 方法，Java借助 LinkedList 的addLast()方法）。
- 出栈： 将各节点值 pop 出栈，存储于数组并返回。（Python 直接返回 stack 的倒序列表，Java 新建一个数组，通过 popLast() 方法将各元素存入数组，实现倒序输出）。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        stack = []
        while head:
            stack.append(head.val)
            head = head.next
        return list(reversed(stack))  # 
```

### 复杂度分析

- 时间复杂度 *O(N)*： 入栈和出栈共使用 *O(N)* 时间。
- 空间复杂度 *O(N)*： 辅助栈 `stack` 和数组 `res` 共使用 *O(N)* 的额外空间。

### 参考

- [python——python中list.reverse()函数得到的结果为None_qq_34872215的博客-CSDN博客](https://blog.csdn.net/qq_34872215/article/details/88792996)
- [剑指 Offer 06. 从尾到头打印链表 - 力扣（Leetcode）](https://leetcode.cn/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/solutions/97270/mian-shi-ti-06-cong-wei-dao-tou-da-yin-lian-biao-d/?languageTags=python3)
