# 209. Minimum Size Subarray Sum（06/20/2019）

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/minimum-size-subarray-sum/)

## 难度

**中等 Medium**

## 问题描述

Given an array of **n** positive integers and a positive integer **s**, find the minimal length of a **contiguous** subarray of which the sum <font color="#dd0000">≥</font> **s**. If there isn't one, return 0 instead.

## 示例数据

```
Input: s = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

## 题意理解

找到最短连续的数组，同时满足其和**大于等于**给定**s**

## 题目分析

这里首先注意的条件是**≥**，这一点很重要。通过一个for loop更新其结果值`res`，并且当满足其条件的时候，需要从左边设置一个`left = 0`开始，逐渐递增，找到满足情况下最短的长度。这里也是采取**two pointer**的方法。

## Test case

```
Input: s = 7, nums = [2,3,1,2,4,3]

left = 0, sum = 0;

i = 0:
sum = 2;

i = 1:
sum = 5;

i = 2:
sum = 6;

i = 3:
sum = 8;
进入while循环 
	res = 4;
	sum = 8 - 2 = 6;
	left = 1;

i = 4:
sum = 6 + 4 = 10;
进入while循环
	(1)
	res = 4;
	sum = 10 - 3 = 7;
	left = 2;
	(2)
	res = 3;
	sum = 7 - 1 = 6;
	left = 3;

i = 5:
sum = 6 + 3 = 9;
进入while循环
	(1) 
	res = 3;
	sum = 6 - 2 = 4;
	left = 4;
	(2) 
	res = 2;
	sum = 4 - 4 = 0;
	left = 5;

return res;	
```

## 参考代码

```java
package com.leetcode.array.counter;

public class _209_MinimumSizeSubarraySum {

    /**
     * 209. Minimum Size Subarray Sum
     * When: 2019/03/26
     *
     * solution:
     *  滑动窗口：表示先加数字，然后判断其与s的大小，如果是大于的情况就while循环让其length减到最小
     *  并且符合sum >= s的情况
     * @param s
     * @param nums
     * @return
     */
    //time: O(n) space:O(1)
    public static int minSubArrayLen(int s, int[] nums) {
			int res = Integer.MAX_VALUE;
      int left = 0, sum = 0;
      for (int i = 0; i < nums.length; i++) {
        sum += nums[i];
        while (left <= i && sum >= s) {
          res = Math.min(res, i - left + 1);
          sum -= nums[left++];
        }
      }
      return res == Integer.MAX_VALUE ? 0 : res;
    }
}

```



