# 88. Merge Sorted Array （06/18/2019）

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/merge-sorted-array/ )

## 难度

**简单 easy**

## 问题描述

Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array. </br>

**Note:**

- The number of elements initialized in *nums1* and *nums2* are *m* and *n* respectively.
- You may assume that *nums1* has enough space (size that is greater or equal to *m* + *n*) to hold additional elements from *nums2*.

## 示例数据

```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

## 题意理解

将两个有序的数组合并起来。并且这里统一合并到第一个数组中（不用额外开辟空间）

## 题目分析

正如题意，需要将两个数组合并起来，这里给定了有效长度`m, n `以及第一个数组m+n那么大。所以只需要循环比较然后插入到第一个数组里面。但是，这里由于是后面为空，所以应该从后边比较并且移动（这个跟以前的合并排序里面的从前到后刚好相反，但是原理相同）。并且，这里值得注意的是，由于第一个数组是被调整的数组，那么如果第二个数组的所有元素大于其第一个数组，则第一个数组的数字并不需要移动（相当于已经完成了移动的过程）。反而，如果第二个数组的所有元素小于第一个数组，则需要最后将第二个数组的所有元素单独赋值，完成循环。通常情况，不会那么极端，只是需要最后遍历第二个数组小于第一个数组的元素，将其赋值。

## Test case

```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

// 第一个数组和第二个数组的起始位置
i = 2; 
j = 2;
k = 2 + 2 - 1; // 记录其目标数组的起始位置

1. nums1[2] < nums2[2]:
目标数组：[1,2,3,0,0,*6*]
j--; // j = 1

2. nums1[2] < nums2[1]:
目标数组：[1,2,3,0,*5*,6];
j--; // j = 0;

3. nums1[2] > nums2[0]
目标数组：[1,2,3,*3*,5,6];
i--;// i = 1;

4. nums1[1] = nums2[0]
目标数组：[1,2,*2*,3,5,6];
i--; //i = 0;

5. nums1[0] < nums2[0]
目标数组: [1,*2*,2,3,5,6];
j--;// j = -1
由于 j < 0 跳出 while循环
这时候 i 相当于也完成扫描（因为之前自身有序的原因）
res = [1,2,2,3,5,6];
```

## 参考代码

```java
package com.leetcode;

public class _88_MergeSortedArray {

    /**
     * 88. Merge Sorted Array
     * When: 2019/03/28
     *
     * solution:
     * 从后往前比较，然后把大的放到nums1的后面（完成这样一次操作，index就需要--）
     * 也要考虑到nums2全都小于num1的情况 所以需要加while(j >= 0)
     * @param nums1
     * @param m
     * @param nums2
     * @param n
     */
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        // 从后往前相比较 大的数字就插到后面
        int i = m - 1; //记录nums1的最后不为空的位置
        int j = n - 1; //记录nums2的最后不为空的位置
        int k = m + n - 1; // 记录待插入的位置
        while (i >=0 && j >= 0){
            nums1[k--] = nums1[i] >= nums2[j] ? nums1[i--]: nums2[j--];
        }
        // 如果nums2全部都小于nums1 所以j需要继续填充到最前面
        while (j >= 0){
            nums1[k--] = nums2[j--];
        }
    }
}
```



