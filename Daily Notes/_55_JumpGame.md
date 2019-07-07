# 55. Jump Game(07/07/2019) 

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/jump-game/)

## 难度

**中等 Medium**

## 问题描述

Given an array of non-negative integers, you are initially positioned at the first index of the array.</br>

Each element in the array represents your maximum jump length at that position.</br>

Determine if you are able to reach the last index.

## 示例数据

```
Input: [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.

Input: [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum
             jump length is 0, which makes it impossible to reach the last index.
```

## 题意理解

是否能够最后跳跃到终点。

## 题目分析

由于这里的步数并没有说需要走满，所以其实可以选择（例如 nums[0] = 3，那我可以选择走1步、2步都可以）。在这里，计算每种情况，能够走到最远情况，这个是指从 0 出发的最长长度，并且一直循环找寻最大的值。

## Test case

```
Input: [3,2,1,0,4]

int max = 0;

i = 0: 
max = 3;

i = 1:
max = 3;

i = 2:
max = 3;

i = 3:
max = 3;

i = 4:
i > max (4) 
结束

return false;
```

## 参考代码

```java
package com.leetcode.array;

public class _55_JumpGame {

    /**
     *  55. Jump Game
     *  When: 2019/03/20
        Review1: 2019/7/7
        Difficulty: Medium

     * solution:
     * 首先初始化max=0；每一个地方能走最远的距离就是该索引i的值加上nums[i] 与 max 作比较 取最大
     * 最后比较到 index = i - 1 只要 i <= max 则表示可以到达
     * 有点“贪心算法”的意思
     * @param nums
     * @return
     */
    //time : O(n) space : O(1)
    public boolean canJump(int[] nums) {
        // 当前位置最大能走的长度就是max 与 当前的索引值加上对应的nums值 这里的max是指从index=0 走最长的长度
        int max = 0;
        for (int i = 0; i <  nums.length; i++){
            if (i > max) return false;
            max = Math.max(max, nums[i] + i);
        }
        return true;
    }
}
```



