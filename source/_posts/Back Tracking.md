---
title: Back Tracking 问题思考
date: 2019-08-20 17:03:48
tags: 
- Back Tracking
- Leetcode
categories: 
- Algorithm
---

Leetcode 上的back tracking 相关题目总结。

## 思路

每一次递归就是进入一个维度，需要将每个维度中的所有符合条件的可能性遍历并加入结果，**如果结果是全局变量（或者说是堆上的变量），则在回溯时需要删除刚才添加的可能性**， 是深度优先搜索。

代码模板大概是:

```cpp
//list s是已取出的数，nums是原始数组，pos是当前取第几个位置的数
public void helper(List<Integer> s,int[] nums,int pos){
        //跳出条件
        if(……){
            ……
            return;
        }
        //遍历每个维度中的数
        for(int i=0;i<nums.length;i++){
            int num = nums[i];
            //取过的数不再取    
            if(s.contains(num)){
                continue;
            }
            //取出一个数
            s.add(num);
            //进行下一个位置的取数，pos+1
            helper(s,nums,pos+1);
            //重要！！遍历过此节点后，要回溯到上一步，因此要把加入到结果中的此点去除掉！
            s.remove(s.size()-1);
        }
    }
}

```

[案例分析介绍](http://xcx1024.com/ArtInfo/149620.html)