# 169. Majority Element (07/04/2019) 补7/2

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/majority-element)

## 难度

**简单 Easy**

## 问题描述

Given an array of size *n*, find the majority element. The majority element is the element that appears **more than** `[ n/2 ]` times.</br>

You may assume that the array is non-empty and the majority element always exist in the array.

## 示例数据

```
Input: [3,2,3]
Output: 3

Input: [2,2,1,1,1,2,2]
Output: 2
```

## 题意理解

找出大于 n/2 个出现次数的元素。

## 题目分析

这里面存在的解法比较多。</br>

首先是使用 `HashMap<Integer, Integer>` 记录其每个出现的情况，并且判断是否存在该情况，存在就 break 然后输出。</br>

第二个方法，先通过 Java 自带的排序`Arrays.sort(nums)`，然后找到 n/2 位置的结果，这个即是结果。

第三个方法，即 `Moore voting algorithm` 。每次都找出一对不同的元素，从数组中删掉，直到数组为空或只有一种元素。不难证明，如果存在元素e出现频率超过半数，那么数组中最后剩下的就只有e。

## Test case

```
以下的过程是 solution 3的。

Input: [2,2,1,1,1,2,2]

count = 0;
res = 0;

i = 0:
count == 0 满足 
赋值res = 2;
count ++; // count = 1;

i = 1:
满足res == nums[1];
count++; // count = 2;

i = 2:
不满足
count--; // count = 1;

i = 3:
不满足
count--; // count = 0;

i = 4: 
count == 0 满足
赋值res = 1;
count++; // count = 1;

i = 5:
不满足
count--; // count = 0;

i = 6: 
count == 0 满足
res = 2;

结束
return res;
```

## 参考代码

```java
package com.leetcode.array;

import java.util.Arrays;
import java.util.HashMap;

public class _169_MajorityElement {

    /**
     * 169. Majority Element
     * when: 2019/03/17
     * Review1: 2019/7/4
     * <p>
     * 思路： 下面两种solutions
     * <p>
     * 涉及到的数据结构或者方法：
     * HashMap<>
     *
     * @param nums
     * @return
     */
    // time:O(n) space:O(n)
    public int majorityElement(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int res = 0;
        for (int num : nums) {
            if (!map.containsKey(num)) {
                map.put(num, 1);
            } else {
                map.put(num, map.get(num) + 1);
            }

            if (map.get(num) > nums.length / 2) {
                res = num;
                break;
            }
        }
        return res;
    }

    // solution2: 由于题目规定了一定会有大于n/2的情况，则目标数就在最中间！
    // time:O(nlogn) space:O(1)
    public int majorityElement2(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length / 2];
    }

    // Moore voting algorithm
    // solution 3: 利用count，一开始计算第一个的num存在的count 然后与后面比较
    // 相同就+1 不同就-1 并且导致res 取到后面。。。依次进行
    // 每次都找出一对不同的元素，从数组中删掉，直到数组为空或只有一种元素。
    // 不难证明，如果存在元素e出现频率超过半数，那么数组中最后剩下的就只有e。
    // time:O(n) space:O(1)
    public int majorityElement3(int[] nums) {
        int count = 0;
        int res = 0;
        for (int num : nums) {
            if (count == 0)
                res = num;
            if (res == num) count++;
            else count--;
        }
        return res;
    }

}

```



