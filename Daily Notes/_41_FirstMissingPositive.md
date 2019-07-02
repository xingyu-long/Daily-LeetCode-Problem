# 41. First Missing Positive  (07/01/2019) 补6/27

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/first-missing-positive)

## 难度

**困难 Hard**

## 问题描述

Given an unsorted integer array, find the smallest missing positive integer.

## 示例数据

```
Input: [1,2,0]
Output: 3

Input: [3,4,-1,1]
Output: 2

Input: [7,8,9,11,12]
Output: 1
```

## 题意理解

找出该数组中缺少的最小正整数（从1开始的数字）

## 题目分析

使用桶排序的思想解决，则就是对应的位置应该是对应的数，这里面就是i = 0 nums[0]应该为1，则都是这样的一一对应，最后再验证，如果中途有断，则直接返回 `i + 1`。如果一直对应，则返回该长度 + 1作为结果。

## Test case

```
Input: [3,4,-1,1]

index= [0, 1, 2, 3]
nums = [3, 4, -1, 1]

i = 0:
由于nums[nums[0] - 1] != nums[0] 
交换
nums = [*-1*, 4, *3*, 1]
由于nums[0] = -1 while循环结束

i = 1:
由于nums[nums[1] - 1] != nums[1] 
交换
nums = [-1, *1*, 3, *4*]
继续交换
nums = [*1*, *-1*, 3, 4]
由于nums[1] = -1 while循环结束

i = 2:
不变

i = 3:
不变

结束
return 2;
```

## 参考代码

```java
package com.leetcode.array;

public class _41_FirstMissingPositive {
    //time:O(n) space:O(1)
    public static int firstMissingPositive(int[] nums){
        if (nums == null || nums.length == 0) return 1;
        for (int i = 0; i < nums.length; i++){
            while (nums[i] > 0 && nums[i] <= nums.length && nums[nums[i] - 1] != nums[i]){
                int temp = nums[nums[i] - 1];
                nums[nums[i] - 1] = nums[i];
                nums[i] = temp;
            }
        }
        for (int i = 0; i < nums.length; i++){
            if(nums[i] != i + 1){
                return i + 1;
            }
        }
        return nums.length + 1;
    }
}
```



