# 26. Remove Duplicates from Sorted ArrayII (06/30/2019) 补6/25

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)

## 难度

**中等 Medium**

## 问题描述

Given a sorted array *nums*, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that duplicates appeared at most *twice* and return the new length.</br>

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

示例数据

```
Given nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.

It doesn't matter what you leave beyond the returned length.
```

## 题意理解

移除数组中重复两次以上的元素。

## 题目分析

这里的思路依然是采取`two pointer`，只是有些细节需要注意。在这里，条件判断语句中应该是`nums[count - 2]`与`nums[i]`作比较。因为这样才可以一直保持前方被选定的特征，如果是使用`nums[i - 2]`，到时候发生替换之后，会影响后面的处理，导致不能完成移除重复两次以上的元素。

## Test case

```
Given nums = [1,1,1,2,2,3],

count = 2, i = 2:
不符合条件

count = 2, i = 3:
满足nums[count - 2] != nums[i] 
nums[count] = nums[i] = 2;
nums = [1,1,*2*,2,2,3]
count = 3;

count = 3, i = 4:
满足nums[count - 2] != nums[i] 
nums[count] = nums[i] = 2;
nums = [1,1,2,*2*,2,3]
count = 4

count = 4, i = 5:
满足nums[count - 2] != nums[i] 
nums[count] = nums[i] = 3;
nums = [1,1,2,2,*3*,3]
count = 5

结束
nums = [1,1,2,2,3,3]

```

## 参考代码

```java
package com.leetcode.array;

import java.util.Arrays;

/**
 * Created by longxingyu on 2019/2/12.
 */
public class _80_RemoveDuplicateFromSortedArrayII {
    /**
     *  80. Remove Duplicates from Sorted Array II
        When: 2019/02/12
        Review1 : 2019/6/30
     * 错误思路：1. 我以为需要一个flag进行标记个数 2. 之前的count没有搞懂（应该类似于指针的东西） 3. 这里使用i的话，会有覆盖作用，导致i=4的时候等于i=2 4. return错误 应该是count才对
     * 解题思路： 一定有两位保留，所以count=2（相当于从第三个开始）
     * case: [1, 1, 1, 2, 2, 3]
     *              2
     *                 c
     *                    i
     * result: [1, 1, 2, 2, 3, 3]
     * @param nums
     * @return
     */
    public static int removeDuplicates(int[] nums) {
        //判断nums是否满足
        if (nums.length <= 2) return nums.length;
        int count = 2;
        for (int i = 2; i < nums.length; i++){
            if(nums[count - 2] != nums[i]){
                nums[count++] = nums[i];
            }
        }
        return count;
    }
}
```



