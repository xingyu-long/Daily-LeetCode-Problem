# 229. Majority Element II (07/04/2019) 补7/3

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/majority-element-ii)

## 难度

**中等 Medium**

## 问题描述

Given an integer array of size *n*, find all elements that appear more than `[ n/3 ]` times.

**Note:** The algorithm should run in linear time and in O(1) space.

## 示例数据

```
Input: [3,2,3]
Output: 3

Input: [1,1,1,3,3,2,2,2]
Output: [1,2]
```

## 题意理解

找出大于 n/3 个出现次数的所有元素。

## 题目分析

由于题目要求`time complexity : O(n) , space complexity: O(1)`所以使用前面的 HashMap 的方法明显不合适，只能采取 `Moore voting algorithm` 的变形。根据题目意思，需要找到超过出现 n/3 次的所有元素，那么只能存在最多两个数，因为这样才能保持 2/3 的比例。所以，这个题可以使用前面一样的思路，只是用多个变量，先找出两个number，然后再验证是否超过 n/3 次。 

## Test case

```
Input: [1,1,1,3,3,2,2,2]

number1 = 0, number2 = 0;
count1 = 0, count2 = 0;

i = 0:
count1 == 0成立
number1 = 1;
count1 = 1;

i = 1:
number1 == nums[1]成立
count++; // count = 2;

i = 2:
number1 == nums[2]成立
count++; // count = 3;

i = 3:
count2 == 0成立
number2 = 3;
count2 = 1;

i = 4:
number2 == nums[4]成立
count2++; // count2 = 2;

i = 5: 
不符合
count1--; //count1 = 2;
count2--; //count2 = 1;

i = 6:
不符合
count1--; //count1 = 1;
count2--; //count2 = 0;

i = 7:
count2 == 0 成立
number2 = 2

然后循环验证
结束
res = [1, 2];
```

## 参考代码

```java
package com.leetcode.array;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;

public class _229_MajorityElementII {

    /**
     * 229. Majority Element II
     * When: 2019/03/18
     *
     * 思路：
     * solution1： 可以使用之前相似的做法，然后用单独的ArrayList进行存储
     * solution2： 由于是 > 1/3*n次 可以使用Moore voting algorithm
     *
     * @param nums
     * @return
     */
    public List<Integer> majorityElement(int[] nums) {
        //判断边界条件
        if (nums == null || nums.length == 0){
            return new ArrayList<>();
        }
        /**
         *
         * solution 1：
         * 依然使用HashMap进行存储并且利用value存储，并且需要一个ArrayList来保存结果 (这里注意res里面可能会有重复的，所以需要排除这种情况)
         * time: O(n)
         * space: O(n)
         **/
        HashMap<Integer, Integer> map = new HashMap<>();
        ArrayList<Integer> res = new ArrayList();

        for (int num: nums){
            if (!map.containsKey(num)){
                map.put(num, 1);
            } else{
                map.put(num, map.get(num) + 1);
            }

            if (map.get(num) > nums.length / 3 && !res.contains(num)){
                res.add(num);
            }
        }
        return res;
    }

    /** 先找身为大多数的number1 和 number 2 然后再验证*/
    //time:O(n) space:O(1)
    public List<Integer> majorityElement2(int[] nums) {
        //由于要大于 n / 3的数字 所以只有两个数可以存在。因为这样才能占 2/3
        if (nums == null || nums.length == 0) {
            return new ArrayList<>();
        }
        List<Integer> res = new ArrayList<>();
        //先找出占多数的两个number
        int number1 = 0, number2 = 0;
        int count1 = 0, count2 = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == number1) {
                count1++;
            } else if (nums[i] == number2) {
                count2++;
            } else if (count1 == 0) {
                number1 = nums[i];
                count1 = 1;
            } else if (count2 == 0) {
                number2 = nums[i];
                count2 = 1;
            } else {
                count1--;
                count2--;
            }
        }

        //计算是否大于n/3个
        count1 = 0;
        count2 = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == number1) {
                count1++;
            } else if (nums[i] == number2) {
                count2++;
            }
        }
        if (count1 > nums.length / 3) {
            res.add(number1);
        }
        if (count2 > nums.length / 3) {
            res.add(number2);
        }
        return res;
    }
}

```



