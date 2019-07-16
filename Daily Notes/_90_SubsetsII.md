# 90. Subsets II (07/15/2019)
> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/subsets-ii/)

## 难度

**中等**

## 问题描述

Given a collection of integers that might contain duplicates, **nums**, return all possible subsets (the power set).</br>

**Note:** The solution set must not contain duplicate subsets.

## 示例数据

```
Input: [1,2,2]
Output:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

## 题意理解

求数组 nums 元素的所有子集。

## 题目分析

其实这个题与之前的 [Subsets解答笔记](https://github.com/halolong/Daily-LeetCode-Problem-With-Me/blob/master/Daily%20Notes/_78_Subsets.md) 差不多，只是需要额外处理重复的元素。首先需要排序，这样有利于后续跳过重复的元素，并且在递归中的目标选择模块加入 `if (i != index && nums[i] == nums[i - 1] continue;` 则进行剪枝操作，不再进行该次的递归操作。

## Test case

```
Input: nums = [1,2,2]

list = [];
#res = [[], ];

(1) index = 0, i = 0:
list = [1, ]
	进入helper
	(1.1) index = 1, i = 1;
		#res =[[], [1], ]
		list = [1, 2]
			进入helper 
			index = 2, i = 2;
			#res = [[], [1], [1, 2], ]
			list = [1, 2, 2];
				进入helper
				#res = [[], [1], [1, 2], [1, 2, 2]];
			remove -> list = [1, 2];
		 remove-> list = [1];
	(1.2) index = 1, i = 2;
			跳过
	remove -> list = [];

(2) index = 0, i = 1:
		list = [2, ];
		进入helper
		(2.1) index = 2, i = 2;
				#res = [[], [1], [1, 2], [1, 2, 2], [2], ];
				进入helper
					list = [2, 2];
					index = 3, i = 3;
					#res = [[], [1], [1, 2], [1, 2, 2], [2], [2, 2],];
				remove -> list = [2, ];
		remove -> list = [];
		
(3) index = 0, i = 2:
		continue 跳过

结束
#res = [[], [1], [1, 2], [1, 2, 2], [2], [2, 2]];
```

## 参考代码

```java
package com.leetcode.backtracking;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class _90_SubsetsII {

    /**
     *  90. Subsets II
     *  When: 2019/04/26
     *  Review1: 2019/7/15
     *
     * solution:
     * 也是用回溯法，只要的区别是去重的情况
     *
     * 这里记得注意当i=2的时候 会有continue的情况
     * 比较表示是 index = 0 与 i = 0, 1, 2的情况
     * @param nums
     * @return
     */
    //time: O(2^n) space:O(n)
    public static List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null || nums.length == 0) return res;
        // 一定要排序，这样利于去重
        Arrays.sort(nums);

        helper(res, new ArrayList<Integer>(), nums, 0);
        return res;
    }

    public static void helper(List<List<Integer>> res, List<Integer> list, int[] nums, int index) {
        res.add(new ArrayList<>(list));
        for (int i = index; i < nums.length; i++) {
            if (i != index && nums[i] == nums[i - 1]) continue;
            list.add(nums[i]);
            helper(res, list, nums, i + 1);
            list.remove(list.size() - 1);
        }
    }
}
```



