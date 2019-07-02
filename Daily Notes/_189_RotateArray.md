# 189. Remove Duplicates from Sorted Array (07/01/2019) 补6/26

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/rotate-array)

## 难度

**简单 Easy**

## 问题描述

Given an array, rotate the array to the right by *k* steps, where *k* is non-negative.

## 示例数据

```
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

## 题意理解

将该数组翻转k步

## 题目分析

这个题有两个解法。第一种，则是把当前位置加上k，然后`结果 % nums.length`则就得到应该所在的位置，这里需要额外的一个辅助空间。第二种方法则是，先完全反转整个数组，然后反转前k个，最后反转剩下的，最后得到其翻转的结果。

## Test case

```
Input: [1,2,3,4,5,6,7] and k = 3

翻转全部
[7, 6, 5, 4, 3, 2, 1]

翻转前k个数
[5, 6, 7, 4, 3, 2, 1]

翻转剩下的数
[5, 6, 7, 1, 2, 3, 4]
```

## 参考代码

```java
package com.leetcode.array;
import java.util.Arrays;

public class _189_RotateArray {

    /**
     *  189. Rotate Array
        When: 2019/2/12
        review1: 2019/7/1

     思路：主要是求余运算刚刚能够达成这个目标并且空间复杂度也是O(n)
     * @param nums
     * @param k
     */
    //time: O(n) space:O(n)
    public static void rotate(int[] nums, int k){
        //通过求余运算
        int[] temp = new int[nums.length];
        for (int i = 0; i < nums.length; i++){
            //i + k就表示应该所在的位置，但是可能超出数组长度，所以这里再%即可。
            temp[ (i + k) % nums.length ] = nums[i];
        }
        //赋值给nums
        for (int i = 0; i < nums.length; i++){
            nums[i] = temp[i];
        }
    }

    /**
     * 思路：通过反转数组的方式，然后局部反转 达到效果。
     * @param nums
     * @param k
     */
    //time:O(n) space:O(1)
    public static void rotate2(int[] nums, int k){
        k %= nums.length;
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }

    public static void reverse(int[] nums, int start, int end){
        while (start < end){
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}

```



