# 78. Subsets (07/15/2019) 补7/14
> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/subsets/)

## 难度

**中等**

## 问题描述

Given a set of **distinct** integers, *nums*, return all possible subsets (the power set).</br>

**Note:** The solution set must not contain duplicate subsets.

## 示例数据

```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

## 题意理解

求数组 nums 元素的所有子集。

## 题目分析

由于该题需要求出所有的子集，并且满足一个条件，不能有重复的子集出现。该问题使用**回溯法**解决。并且由于子集的特征，可以使用 `i + 1` 作为下一次递归调用的参数。并且这里面每一次进入 helper 函数直接加入结果列表中。主要的思想为加入待尝试的数字，如果符合加入结果集，不符合将其移除，尝试下一个数字。

## Test case

```
Input: nums = [1,2]

nums.length = 2
			(1) res.add   # res = [[], ];
      (2) i = 0;
              list.add -> list = [1];
              (2.1)helper(res, list, nums, 1)
                    # res = [[], [1], ]
                    i = 1
                    list = [1,2]
                    helper(res, list, nums, 2)  res.add # res = [[], [1], [1, 2]] 没有进入循环
                    list.remove(1) list = [1]
              list.remove(list.size() - 1 = 0) list = [];
      (3) i = 1;
            list.add -> list = [2];
            (3.1) helper(res, list, nums, 2) -> res.add # res = [[], [1], [1,2], [2]] 没有进入循环
                    remove(list.size - 1= = 0) list = []

       res = [[], [1], [1,2], [2]];
```

## 参考代码

```java
package com.leetcode.backtracking;

import java.util.ArrayList;
import java.util.List;

public class _78_Subsets {

    /**
     *  78. Subsets
     *  When: 2019/04/26
     *  Review1: 2019/7/15
     *
        solution: 回溯法
     *  time : O(2 ^ n)
     *  space: O(n)
     * @param nums
     * @return
     */
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null || nums.length == 0) return res;
        helper(res, new ArrayList<>(), nums, 0);
        return res;
    }

    public static void helper(List<List<Integer>> res, List<Integer> list, int[] nums, int index) {
        res.add(new ArrayList<>(list));
        for (int i = index; i < nums.length; i++) {
            list.add(nums[i]);
            helper(res, list, nums, i + 1);
            list.remove(list.size() - 1);
        }
    }
}
```



