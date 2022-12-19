---
title: 剑指Offer-30：包含min函数的栈
date: 2022-12-19 14:07:01
tags: 
- 栈
- Algorithm
- Leetcode
cover: https://images.unsplash.com/photo-1667747501985-40fa56e5cebc
---



### 问题：

[剑指 Offer 30. 包含min函数的栈 - 力扣（Leetcode）](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/description/?envType=study-plan&id=lcof&plan=lcof&plan_progress=y8llrks)

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

```python
# 示例
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

### 方法：辅助线

#### 理解栈结构先进后出的性质

- 对于栈来说，如果一个元素 `a` 在入栈时，栈里有其它的元素 `b, c, d`，那么无论这个栈在之后经历了什么操作，只要 `a` 在栈中，`b, c, d`就一定在栈中，因为在 `a` 被弹出之前，`b, c, d` 不会被弹出。

- 因此，在操作过程中的任意一个时刻，只要栈顶的元素是 `a`，那么我们就可以确定栈里面现在的元素一定是 `a, b, c, d`。

- 那么，我们可以在每个元素 `a` 入栈时把当前栈的最小值 `m` 存储起来。在这之后无论何时，如果栈顶元素是 `a`，我们就可以直接返回存储的最小值 `m`。

我们可以使用一个辅助栈，与元素栈同步插入与删除，用于存储与每个元素对应的最小值。

```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = [math.inf]

    def push(self, x: int) -> None:
        # 当一个元素要入栈时，我们取当前辅助栈的栈顶存储的最小值，与当前元素比较得出最小值，将这个最小值插入辅助栈中；
        self.stack.append(x)
        self.min_stack.append(min(x, self.min_stack[-1])) # min函数立大功

    def pop(self) -> None:
        # 当一个元素要出栈时，我们把辅助栈的栈顶元素也一并弹出；
        self.stack.pop()
        self.min_stack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def min(self) -> int:
        # 在任意一个时刻，栈内元素的最小值就存储在辅助栈的栈顶元素中。
        return self.min_stack[-1]
```

### 复杂度分析

- 时间复杂度：对于题目中的所有操作，时间复杂度均为 O(1)O(1)O(1)。因为栈的插入、删除与读取操作都是 O(1)O(1)O(1)，我们定义的每个操作最多调用栈操作两次。

- 空间复杂度：O(n)O(n)O(n)，其中 nnn 为总操作数。最坏情况下，我们会连续插入 nnn 个元素，此时两个栈占用的空间为 O(n)O(n)O(n)。

### 参考

- [剑指 Offer 30. 包含min函数的栈 - 力扣（Leetcode）](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/solutions/1398785/bao-han-minhan-shu-de-zhan-by-leetcode-s-i2fk/)
