# 27. Remove Element (06/30/2019) 补6/23

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/remove-element)

## 难度

**简单 Easy**

## 问题描述

Given an array *nums* and a value *val*, remove all instances of that value [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.</br>

The order of elements can be changed. It doesn't matter what you leave beyond the new length.</br>

示例数据

```
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.
```

## 题意理解

移除数组中与val相同的元素并且返回剩下的有效长度值。

## 题目分析

本题是典型的`two pointer`的方法解决。一个指针用来保留待插入的位置，一个指针用来循环该数组并且寻找与val不相同的时候，就可以赋值给待插入位置并且指针向右移动一位。

## Test case

```
Given nums = [3,2,2,3], val = 3,

res = 0, i = 0:
不符合条件

res = 0, i = 1:
nums[1] != 3 满足条件、nums[res] = nums[1] = 2;
修改后
nums = [*2*,2,2,3]
res = 1;

res = 1, i = 2: 
nums[2] != 3 满足条件、nums[res] = nums[2] = 2;
修改后
nums = [2,*2*,2,3]
res = 2;

res = 2, i = 3:
不符合条件
结束

res = 2, nums[2,2,2,3];
```

## 参考代码

```java
package com.leetcode.array;
import java.util.Arrays;

public class _27_RemoveElement {

    /**
     *  27. Remove Element
     *  difficulty: Easy
        When: 2019/02/11
        review 1: 2019/06/30

        solution:
            利用two pointer： 一个从前往后扫描（i）一个记录结果（r）
            相当于当val等于nums[i]的时候res当前对应的数组值被替换并且向前移动一位
     * @param nums
     * @param val
     * @return
     */
    public int removeElement(int[] nums, int val){
        if (nums == null || nums.length == 0) return 0;
      	int res = 0;
      	for (int i = 0; i < nums.length; i++) {
          if (nums[i] != val) {
            nums[res++] = nums[i];
          }
        }
      	return res;
    }
}
```



