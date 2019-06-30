# 398. Random pick index (06/22/2019)

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/sliding-window-maximum/)

## 难度

**中等 Medium**

## 问题描述

Given an array of integers with possible duplicates, randomly output the index of a given target number. You can assume that the given target number must exist in the array.

**Note:**
The array size can be **very large**. Solution that uses too much extra space will not pass the judge.

## 示例数据

```
int[] nums = new int[] {1,2,3,3,3};
Solution solution = new Solution(nums);

// pick(3) should return either index 2, 3, or 4 randomly. Each index should have equal probability of returning.
solution.pick(3);

// pick(1) should return 0. Since in the array only nums[0] is equal to 1.
solution.pick(1);
```

## 题意理解

输出与target相同的索引i的值（其中相同的有多个值）

## 题目分析

这个问题属于典型的蓄水池抽样（reservoir sampling）问题。其中的核心特征就是总量n不确定，但是需要保证抽中的数等概率分布，即始终保持 `1 / n`。</br>

蓄水池抽样的主要过程：

* 抽取所需要的k个目标 (其中k <= n)
* 当开始获取第 k + 1个的时候，生成随机数，其范围在[0, k + 1)中
* 如果随机数属于 [0, k - 1]，则直接替换。

这个题中我们的目标则就是等于target的情况。并且一直循环，这样每个目标获得的几率是相同的。</br> 

## Test case

```
Input = [1,2,3,3,3], target = 3;
//这里生成的是索引i
count = 1; 由于随机是生成 [0, 1) 所以这一次只能生成0，则p(获得target = 3) = 1;
count = 2; p(获得target = 3) = 1/2;
count = 3; p(获得target = 3) = 1/3;
那么获得target = 3对于总的来说 则就是 1 * 1/2(第二次不得到3的概率) * 2/3(第三次不得到3的概率)  = 1/3。则保持了每个目标均等的概率。
// 这里理解为不同的几个3，然后需要保持其抽中的概率要为等同的。
```

## 参考代码

```java
package com.leetcode.random;

import java.util.Random;

public class _398_RandomPickIndex {
    private int[] nums;
    private Random rmd;

    /**
     *  398. Random Pick Index
        When: 2019/06/20

        solution: 蓄水池抽样法，让其概率均等
     * @param nums
     */
    public _398_RandomPickIndex(int[] nums) {
        this.nums = nums;
        rmd = new Random();
    }

    public int pick(int target) {
        // 这里就是先要找到等于target的情况，然后随机一个出来（每个机会均等）
        int res = -1;
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != target) continue; // 相当于一定要找到那个target相同的情况
            if (rmd.nextInt(++count) == 0) {
                res = i;
            }
        }
        return res;
    }

}

```



