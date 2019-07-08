# 45. Jump Game II（06/15/2019）

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/jump-game-ii/)

## 难度

**困难 hard**

## 问题描述

Given an array of non-negative integers, you are initially positioned at the **first index** of the array. Each element in the array represents your maximum jump length at that position. Your goal is to reach the last index in the **minimum number** of jumps.

## 示例数据

```
Input: [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2.
    Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

## 题意理解

问题描述中被加粗的部分则是重要内容，即从第一个开始进行跳跃和找出到终点的最小跳跃次数。

## 题目分析

这里面涉及到选择的问题，就是在能够达到的情况下选择最小的跳跃。其中，经过观察，每一步最大的行走距离是前面的 index 加上其值，则是 `i + nums[i]`。例如，当 `i = 0` 这时候值为2，和为2，则表示从这个点跳出最远的地方就是`i = 2`则就是第一个1的位置。知道这些条件只能帮助判断出是否能够达到其终点，但这里需要最优，则是需要看前面什么时候达到最优。所以需要保持两个变量，一个是当前能走最远的距离curMaxArea，以及能走全程最远的距离maxNext。并且当 `i == curMaxArea` 就说明已经到达了当前的最大情况，然后结果加1，再把maxNext赋值给当前能够最远的距离。(相当于尽量走最长的情况，在跳跃下一次之前找到能更远的情况就直接先跳这一步，例如这里面的`2->3`）

## Test case

```
Input: [2, 3, 1, 1, 1, 6, 11]

res = 0;
cur = 0;
max = 0;
i = 0 (i < 6)
	max = 2;（因为第一步肯定需要走）
	cur == 0 执行条件 res++; cur = 2;
	
i = 1 (i < 6)
	max = 4; (这里表示找到了可以走更远的地方，即i=4的位置)
	1 != cur 不执行
	
i = 2 (i < 6)
	max = 4; 
	cur == 2 执行条件 res++; cur = 4;
	
i = 3 (i < 6)
	max = 4;
	3 != cur 不执行
	
i = 4 (i < 6)
	max = 5; 
	cur == 4 执行条件 res++; cur = 5;
	
i = 5 (i < 6)
	max = 11;
	cur == 5 执行条件 res++; cur = 11;
```

## 参考代码

```java
package com.leetcode.array;

public class _45_JumpGameII {

    /**
     * 45. Jump Game II
     * when: 2019/03/20
     *
     * @param nums
     * @return
     */
    // time: O(n) space: O(1)
    public int jump(int[] nums) {
        if (nums == null || nums.length < 2) return 0;
        int res = 0;
        int curMaxArea = 0; //当前能走的最大距离
        int maxNext = 0; //记录最长走多远（从i=0这个位置开始）
        // 这里的nums.length - 1 很重要，这里的cur表示当前能走的最长距离，
        // 所以当等于i的时候，使用全局最长距离来替换
        for (int i = 0; i < nums.length - 1; i++){
            maxNext = Math.max(maxNext, i + nums[i]);
            if (i == curMaxArea){
                res++;
                curMaxArea = maxNext;
            }
        }
        return res;
    }
}
```



