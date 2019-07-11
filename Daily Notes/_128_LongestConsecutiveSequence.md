# 128. Longest Consecutive Sequence(07/11/2019) 补07/10

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/longest-consecutive-sequence/)

## 难度

**困难 Hard**

## 问题描述

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.</br>

Your algorithm should run in O(*n*) complexity.

## 示例数据

```
Input: [100, 4, 200, 1, 3, 2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

## 题意理解

找出数组的最长连续长度。

## 题目分析

因为需要在找寻连续的情况，所以一定会存在 x, x+1, x+2 等等。在这个问题中，可以反过来思考，如果找不到 x - 1 的数字，那么可以尝试 x, x + 1, x + 2等等，这样也确定唯一的计算方向。其中使用 HashSet 来验证是否存在 x - 1 的存在。

这个题需要注意的是时间复杂度，官方解释是 `O(n)`，这里本人理解还没有太透彻，所以就没给出理由。

## Test case

```
Input: [100, 4, 200, 1, 3, 2]

i = 0:
nums[0] - 1 = 99不存在，所以验证以100开头，不符合条件所以没有

i = 1:
nums[1] - 1 = 3 存在了，不符合继续的条件

i = 2:
nums[2] - 1 = 199不存在，所以验证以200开头，不符合条件所以没有

i = 3:
nums[3] - 1 = 0 不存在，所以验证以1开头的情况。
res = 4;

i = 4:
nums[4] - 1 = 1 存在了，不符合继续的条件

结束
return res;
```

## 参考代码

```java
package com.leetcode.array;

import java.util.HashSet;

public class _128_LongestConsecutiveSequence {

    /**
     *  128. Longest Consecutive Sequence
     *  when: 2019/03/25
     *  Review1: 2019/7/11
     *
     *  这里的时间复杂度为O(n)需要注意
     *  看每个元素最多访问两次，所以worst case: O(n + n)
     *  https://zxi.mytechroad.com/blog/hashtable/leetcode-128-longest-consecutive-sequence/
     *
     * hashset
     * @param nums
     * @return
     */

    //time: O(n) space: O(n)
    public int longestConsecutive(int[] nums) {
        if (nums.length == 0 || nums == null) return 0;
        int res = 0;
        HashSet<Integer> set = new HashSet<>();
        //赋值给HashSet
        for (int num: nums) set.add(num);
        for (int num: set){
                //表示没有存在 x-1 的数（后面表示一直是x+1, x+2 ....
            if (! set.contains(num - 1)){
                int currentNum = num;
                int currentRes = 1;

                //表示为持续+
                while (set.contains(currentNum + 1)){
                    currentNum += 1;
                    currentRes += 1;
                }
                res = Math.max(currentRes, res);
            }
        }
        return res;
    }
}

```



