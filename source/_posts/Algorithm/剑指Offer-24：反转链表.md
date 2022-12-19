---
title: 剑指Offer-24：反转链表
date: 2022-12-19 16:56:24
tags:
- 链表
- Algorithm
- Leetcode
cover: https://images.unsplash.com/photo-1668076120526-41f1e4e20214
---

### 问题

[剑指 Offer 24. 反转链表 - 力扣（Leetcode）](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/description/)

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

```python
# 示例
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

### 方法：temp暂存

考虑遍历链表，并在访问各节点时修改 `next` 引用指向，算法流程见注释。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        cur, pre = head, None
        while cur:
            tmp = cur.next # 暂存后继节点 cur.next
            cur.next = pre # 修改 next 引用指向
            pre = cur      # pre 暂存 cur
            cur = tmp      # cur 访问下一节点
        return pre
```



### 复杂度分析：

- 时间复杂度 O(N) ： 遍历链表使用线性大小时间。
- 空间复杂度 O(1) ： 变量 pre 和 cur 使用常数大小额外空间。



### 参考

- [剑指 Offer 24. 反转链表 - 力扣（Leetcode）](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/solutions/476929/jian-zhi-offer-24-fan-zhuan-lian-biao-die-dai-di-2/?languageTags=python3)
