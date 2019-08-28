---
title: 33. Search in Rotated Sorted Array
date: 2019-08-21 16:42:49
tags: 
- Binary Search
- Leetcode
- Medium
categories: 
- Algorithm
---

## 思路
非典型二分查找，因为数组部分有序 (左右旋转)，但是某一点的左右两侧总是有序的。 具体思考看代码注释。

```python
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        l = 0
        r = len(nums) - 1
        while( l <= r):
        
            mid = (l+r)/2
            if nums[mid] == target:
                return mid
            print(mid)
            
            if nums[l] <= nums[mid]:
                if nums[l] <= target <= nums[mid]:
                    r = mid - 1
                else: # 这里要记住在第一次循环如果target < nums[l] (nums[0])时， 已经确定target是在mid的右侧（0，1，2...）中了
                    l = mid + 1
            else:
                if nums[mid] <= target <= nums[r]:
                    l = mid + 1
                else:# 同理在第一次循环如果target > nums[r]时， 已经确定target是在mid的左侧了
                    r = mid - 1
        return -1
```