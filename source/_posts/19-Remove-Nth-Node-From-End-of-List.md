---
title: 19. Remove Nth Node From End of List
date: 2019-08-21 10:56:21
tags: 
- Linked List
- Leetcode
- Medium
categories: 
- Algorithm
---


## 思路
尽量一次pass就解决，所以使用了递归（利用栈的性质以及递归时会把程序状态存储在函数所在内存中）。每次返回时从后向前记录个数（倒数第n个），如果是需要删除的节点，则返回当前节点下一个节点，通过`node.next = remove(node.next)` 这个代码使得（当前状态下）上个节点的next等于当前节点的next，完成删除操作。如果不是要删除的节点，则直接返回当前节点。

这样在最后一次返回时，返回的依旧是head节点（如果head没被删除）。

### 遇到了坑的用例
> [1]
> 1
> Output: [] 或者 None

需要再第一次调用时将`head = remove(head)` (能track到head节点被删除)

## python 代码

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        self.num = 0
        
        def remove(node):
            if not node:
                self.num += 1
                return node
            node.next = remove(node.next)
            if self.num == n:
                self.num += 1
                return node.next
            else:
                self.num += 1
                return node
            
        head = remove(head)
        return head
        
```

## 优化
1. 可以不用全局 `num`
2. 可以用python 三元表达式 `[x, y](condition)`