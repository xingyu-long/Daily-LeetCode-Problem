# 287. Find the
Duplicate Number (07/11/2019) 

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/find-the-duplicate-number)

## 难度

**中等 Medium**

## 问题描述

Given an array *nums* containing *n* + 1 integers where each integer is between 1 and *n* (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

## 示例数据

```
Input: [1,3,4,2,2]
Output: 2

Input: [3,1,3,4,2]
Output: 3
```

## 题意理解

找出重复的数字。

## 题目分析

这个题有好几种方法，其中 Set 比较常见，只需要验证是否能够加入 (add)，如果不可以，说明已经存在，只是这样的时间复杂度为 O(n)。其中 slow, fast 的方法也可以做出来，后面会补充！

## Test case

```
Input: [1,3,4,2,2]

i = 0:
set = [1, ];

i = 1:
set = [1, 3, ];

i = 2:
set = [1, 3, 4, ];

i = 3:
set = [1, 3, 4, 2, ];

i = 4:
2重复了 
结束
return 2;
```

## 参考代码

```java
package com.leetcode.array;

import java.util.HashSet;

public class _287_FindtheDuplicateNumber {

    /**
     *  287. Find the Duplicate Number
     *  When:2019/7/11
     *  Difficulty: Medium
     *
     *  Solution:
     *  (1) sort
     *  (2) set
     *  (3) fast & slow (like the Linked List Cycle II.)
     * @param nums
     * @return
     */
    //time: O(n) space:O(n)
    public int findDuplicate(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        HashSet<Integer> set = new HashSet<>();
        int res = 0;
        for (int num : nums) {
            if (!set.add(num)) {
                res = num;
                break;
            }
        }
        return res;
    }
}
```



