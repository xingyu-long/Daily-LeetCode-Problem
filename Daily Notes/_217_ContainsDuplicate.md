# 217. Contains Duplicate (07/05/2019) 

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/contains-duplicate/)

## 难度

**简单 Easy**

## 问题描述

Given an array of integers, find if the array contains any duplicates.</br>

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

## 示例数据

```
Input: [1,2,3,1]
Output: true

Input: [1,2,3,4]
Output: false
```

## 题意理解

判断数组中是否存在重复元素。

## 题目分析

该问题具有三种常见的解法。</br>

（1） 使用 Java 中自带的 Arrays.sort(nums) 进行排序后，前后比较发现是否有相同元素。时间复杂度 `O(nlogn)`，空间复杂度 `O(1)`。

（2）利用 HashMap 的键值对特性进行计数，一旦进行 `++` 操作之后就返回。时间复杂度 `O(n^2)`（因为containsKey操作需要O(n)），空间复杂度O(n)。

（3）使用 HashSet 无法添加相同的特性。时间复杂度 `O(n)`，空间复杂度 `O(n)`。

## Test case

```
Input: [1,2,3,1]
由于该题过程简单，所以这里的过程就不写了。
```

## 参考代码

```java
package com.leetcode.array;

import java.util.Arrays;
import java.util.HashMap;
import java.util.HashSet;

public class _217_ContainsDuplicate {

    /**
     * 217. Contains Duplicate
     *  When: 2019/03/19
        Review1: 2019/7/5
     *
     * 解法：hashmap的key-value；set无法重复的特性；sort 然后前后比较
     *
     * 涉及到的数据结构或者方法：
     * hashmap：get(value), containsKey(value), put(key, value)
     * hashset: add(value)
     * Arrays.sort(array)
     * @param nums
     * @return
     */
    // time: O(n^2) space: O(n)
    public boolean containsDuplicate(int[] nums) {
        //solution1: 利用key-value的形式计数
         if (nums == null || nums.length < 1) return false;

         HashMap<Integer, Integer> map = new HashMap<>();
         for (int num: nums) {
             if (!map.containsKey(num)) { // o(n)
                map.put(num, 1);
             } else {
                map.put(num, map.get(num) + 1);
             }

             if(map.get(num) > 1) {
                return true;
             }
         }
         return false;
    }
    // time: O(nlogn) space: O(n)
    public boolean containsDuplicate2(int[] nums) {
        // 利用排序，然后前后两个找是否相同
        Arrays.sort(nums);
        for (int i = 1; i < nums.length; i++){
            if (nums[i] == nums[i-1]) return true;
        }
        return false;
    }
    // time: O(n) space: O(n)
    public boolean containsDuplicate3(int[] nums) {
				// 利用set不能放入重复的特性
        HashSet<Integer> set = new HashSet<>();
        for (int num : nums){
            if (! set.add(num)) return true;
        }
        return false;
    }
}
```



