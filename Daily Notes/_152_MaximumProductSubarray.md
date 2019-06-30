# 152.Maximum Product Subarray（06/21/2019）

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/maximum-product-subarray/)

## 难度

**中等 Medium**

## 问题描述

Given an integer array `nums`, find the **contiguous** subarray within an array (containing at least one number) which has the largest product.

## 示例数据

```
Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```

## 题意理解

找到**连续**乘积数以达到最大乘积。

## 题目分析

其实这个题目跟之前的题目都有些相似，主要在连续的子数组里面找。所以，这种题目通用的方法可以使用两个for loop进行暴力求解，依次记录结果，并且使用`Math.max`得到结果。但是更好的方法是使用`O(n)`时间复杂度进行求解，需要保持两个数组，分别为max、min。通过这个，来记录前面的情况，并且每次通过比较当前值、前一个的最大值 * 当前值以及前一个的最小值 * 当前值。进而得到结果，其中，也不会出现跳跃的情况。例如` [2,3,-2,4]`，当运行到`-2`的时候，这时候的最大值只能在-`12, -6, -2`中选择，所以不存在跳跃导致不连续的情况。

## Test case

```
Input = [2, 3, -2, 4];
max = [2, ...];
min = [2, ...];
res = 2;

i = 1 (nums[1] = 3):
max[1] = 6;
min[1] = 3;
res = 6;

i = 2 (nums[2] = -2):
max[2] = (-12, -6, -2) = -2;
min[2] = -12;
res = 6;

i = 3 (nums[3] = 4):
max[3] = (-8, -48, 4) = 4;
min[3] = -48;
res = 6;
```

## 参考代码

```java
package com.leetcode;

public class _152_MaximumProductSubarray {

    /**
     * 152. Maximum Product Subarray
     * When: 2019/03/27
     *
     * solution:
     * 类似于No.53 可以用暴力解法
     * @param nums
     * @return
     */
    //time: O(n^2) space:O(1)
    public int maxProduct(int[] nums) {
         if (nums.length == 1) return nums[0];
         int res = nums[0];
         int prod = 1;
         for (int i = 0; i < nums.length; i++) {
            for (int j = i; j < nums.length; j++) {
                prod *= nums[j];
                res = Math.max(res, prod);
            }
            prod = 1;
         }
         return res;
    }
  
    // solution2: 三种情况，一种是最小，一种最大，一种当前数字 三个比较值则就是所求
    // time:O(n) space:O(n)
    public int maxProduct2(int[] nums) {
        int res = nums[0];
        int[] max = new int[nums.length];
        max[0] = nums[0];
        int[] min = new int[nums.length];
        min[0] = nums[0];
        for (int i = 1; i < nums.length; i++){
            max[i] = Math.max(Math.max(max[i - 1] * nums[i], min[i - 1] * nums[i]), nums[i]);
            min[i] = Math.min(Math.min(max[i - 1] * nums[i], min[i - 1] * nums[i]), nums[i]);
            res = Math.max(res, max[i]);
        }
        return res;
    }
}

```



