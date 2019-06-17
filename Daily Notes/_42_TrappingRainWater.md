# 42. Trapping Rain Water（06/17/2019）

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/trapping-rain-water/)

## 难度

**困难 hard**

## 问题描述

Given *n* non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

![img](assets/rainwatertrap.png)

The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

## 示例数据

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

## 题意理解

计算出上图蓝色的部分。

## 题目分析

正如上图所示，需要计算其水在这些缝隙的含量。一开始想的就是只能取相对低的地方开始计算(因为这里是低洼，把低的那一方作为宽)。所以需要保留一个变量即`max`，但是仔细思考发现，如果这个max达到了较大的时候刚好又走到了右边则就会导致计算失误。例如，当走到`height[i] = 3`后面的计算就错误了，因为会默认右边可以关闭(就看那个点紧接着的后一个)，就会计算出 `3 - 2 = 1`但其实这一部分没有封闭，所以不能算作其中。到这里的时候，发现如果两边分别保留`max`并且使用*two pointer*就可以达到这个目的了。

## Test case

```
Input = [0,1,0,2,1,0,[1],[3],2,1,2,1]
left = 0;
right = 11;
leftMax = 0;
rightMax = 0;
res = 0;
while (0 < 11) 
1. 满足height[left] < height[right],计算左边
		leftMax = 0;
		res = 0;
		left++;// left = 1;
2. 不满足，计算右边
		rightMax = 1;
		res = 0;
		right--// right = 10;
3. 满足，计算左边
		leftMax = 1;
		res = 0;
		left++; // left = 2;
4. 满足，计算左边
		leftMax = 1;
		res += leftMax - height[2] = 1 - 0 = 1;
		left++; // left = 3;
5. 不满足，计算右边
		rightMax = 2;
		res = 1;
		right--; // right = 9;
6. 不满足，计算右边
		rightMax = 2;
		res = 1 + rightMax - height[9] = 1 + 2 - 1 = 2;
		right--; // right = 8;
7. 不满足，计算右边
		rightMax = 2;
		res = 2;
		right--; // right = 7;
8. 满足，计算左边
		leftMax = 2;
		res = 2;
		left++; // left = 4;
9. 满足，计算左边
		leftMax = 2;
		res = 2 + 1 = 3;
		left++; // left = 5;
10. 满足，计算左边
		leftMax = 2;
		res = 3 + 2 = 5;
		left++; // left = 6;
11. 满足，计算左边
		leftMax = 2;
		res = 5 + 1 = 6;
		left++; // left = 7;

return res; // 这里通过左右max，然后可以形成封闭空间
```

## 参考代码

```java
package com.leetcode.array;

public class _42_TrappingRainWater {

    /**
     * 42. Trapping Rain Water
     * when: 2019/03/25
     *
     * solution: two-pointer
     * 分别设置左右max，然后与当前的进行相差则就是对应的乘水量
     * @param height
     * @return
     */
    // time: O(n) space: O(1)
    public static int trap(int[] height) {
        int res = 0;
        int left = 0;
        int right = height.length - 1;
        int leftMax = 0;
        int rightMax = 0;
      	while (left < right) {
         	if (height[left] < height[right]) {
          	leftMax = Math.max(leftMax, height[left]);
            res += leftMax - height[left];
            left++;
          } else {
            rightMax = Math.max(rightMax, height[right]);
            res += rightMax - height[right];
            right--;
          }
        }
      return res;
    }
}

```



