# 26. Remove Duplicates from Sorted Array (06/30/2019) 补6/24

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/remove-duplicates-from-sorted-array)

## 难度

**简单 Easy**

## 问题描述

Given a sorted array *nums*, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each element appear only *once* and return the new length.</br>

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

## 示例数据

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

## 题意理解

移除数组中重复的元素。

## 题目分析

这个题思路跟之前的[No.27](https://github.com/halolong/Daily-LeetCode-Problem-With-Me/blob/master/Daily%20Notes/_27_RemoveElement.md)思路类似。但是这里的区别是，由于会出现重复，那么在有效的输入情况下，第一个元素是不会重复的，所以count（即前面用的res）一开始为1，作为待插入的位置。并且，i也是从1开始递增，找到与i-1不相等的情况，那么再赋值给待插入的地方。

## Test case

```
Given nums = [1,1,2]

count = 1, i = 1: 
不符合条件

count = 1, i = 2:
nums[i] != nums[i - 1], nums[count] = nums[i] = 2;
count = 2
nums = [1, *2*, 2]
结束
count = 2
nums = [1, 2, 2];
```

## 参考代码

```java
package com.leetcode.array;
import java.util.Arrays;

public class _26_RemoveDuplicateFromSortedArray {
    /**
     * LeetCode No.26
        When: 2019/2/11
        review 1: 2019/6/30

     * 错误思路： 最开始认为不能用nums[count-1]
     * 思路解析：count的位置就是待插入的
     * case: [0, 1, 1, 2, 2]
     *       [0, 1, 2]
     *                 c
     *                    i
     * result: [0, 1, 2]
     */
    public static int removeDuplicates(int[] nums){
        if (nums == null || nums.length == 0) return 0;
        int count = 1; 
      	//因为有序，所以至少第一个存在（即使 {1, 1, 1, 1}）
				//{1, 1, 2, 2, 3}
        for (int i = 1; i < nums.length; i++){
            if(nums[i - 1] != nums[i]){
                nums[count++] = nums[i];
            }
        }
        System.out.println(Arrays.toString(nums));
        return count;
    }
}

```



