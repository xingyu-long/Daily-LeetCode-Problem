# 219. Contains Duplicate II (07/06/2019) 

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/contains-duplicate-ii/)

## 难度

**简单 Easy**

## 问题描述

Given an array of integers and an integer *k*, find out whether there are two distinct indices *i* and *j*in the array such that **nums[i] = nums[j]** and the **absolute** difference between *i* and *j* is **at most** *k*.

## 示例数据

```
Input: nums = [1,2,3,1], k = 3
Output: true

Input: nums = [1,0,1,1], k = 1
Output: true
```

## 题意理解

判断数组中重复的元素距离是否存在小于等于k的情况。

## 题目分析

由于需要记录其中重复的位置，只能使用 HashMap 存储坐标值，然后使用 nums[i] 作为 key，这样就确保了找到重复的数，并且当遇到重复的时候，但是距离大于 k，则需要把当前的 map 里面更新 value，试着看能否在后面找到重复值以及距离小于等于k。

## Test case

```
Input: nums = [1,2,3,1], k = 3
i = 0,1,2
一直插入到 HashMap 中

i = 3:
发现有重复
i - map.get(nums[3]) = 3 <= k
符合条件
结束
return true
```

## 参考代码

```java
package com.leetcode.array;

import java.util.HashMap;

public class _219_ContainsDuplicateII {

    /**
     *
     * 219. Contains Duplicate II
     * when: 2019/03/19
     *
     *
     * 思路的问题：
     * 当时误以为是要求出里面相同数字的最远的长度与k做比较，但其实只需要第一次碰见相同的元素就可以与k比较即可！
     * 题目是否存在这样两个值之差小于k
     * @param nums
     * @param k
     * @return
     */
    // time : O(n * n) space: O(n)
    public static boolean containsNearbyDuplicate(int[] nums, int k){
        if (nums.length <= 1) {
            return false;
        }

        HashMap<Integer, Integer> hashMap = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            if (hashMap.containsKey(nums[i]) && Math.abs(i - hashMap.get(nums[i])) <= k) {
                return true;
            }
            // 表示在存在该key的情况下 也会更新
            hashMap.put(nums[i], i);
        }

        return false;
    }
}

```



