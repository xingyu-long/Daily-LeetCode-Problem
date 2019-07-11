# 11. Container With Most Water(07/10/2019) 补07/09

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/container-with-most-water/)

## 难度

**中等 Medium**

## 问题描述

Given *n* non-negative integers *a1*, *a2*, ..., *an* , where each represents a point at coordinate (*i*, *ai*). *n* vertical lines are drawn such that the two endpoints of line *i* is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water. </br>

**Note:** You may not slant the container and *n* is at least 2.

![img](assets/question_11.jpg)

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

## 示例数据

```
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```

## 题意理解

求解出能够承载的最大水量。

## 题目分析

根据上面图示，需要求水量最大，那么需要坐标轴的距离（即 i ）够远的情况下，能够有很高的纵坐标值 ，即 height[i] 。所以可以保持一个 max 值，并且使用 `two pointer` 的方法来循环，找到最大值。其具体面积的计算公式: `(j - i) * (Math.min(height[j], height[i]))`。

## Test case

```
Input: [1,8,6,2,5,4,8,3,7]

res = 0;
l = 0;
r = 8;

l < r:
height[0] = 1, height[8] = 7;
res = (8-0) * 1 = 8;
l++;// l = 1;

l < r:
height[1] = 8, hight[8] = 7;
res  = (8 - 1) * 7 = 49;
r--;// r = 7;

l < r:
height[1] = 8, height[7] = 3;
res = 49;// 49保持最大
r--; // r = 6;

l < r:
height[1] = 8, height[6] = 8;
res = 49; // 49保持最大
l++; // l = 2;

l < r:
height[2] = 6, height[6] = 8;
res = 49; // 49保持最大
l++; // l = 3;

l < r:
height[3] = 2, height[6] = 8;
res = 49; // 49保持最大
l++; // l = 4;

l < r: 
height[4] = 5, height[6] = 8;
res = 49; // 49保持最大
l++; // l = 5;

l < r:
height[5] = 4, height[6] = 8;
res = 49; // 49保持最大
l++; // l = 6;

不符合 l < r 
结束
return res;
```

## 参考代码

```java
package com.leetcode.array;

public class _11_ContainerWithMostWater {

    /**
     *  11. Container With Most Water
     *  when:2019/03/22
     *  Review:2019/7/10
     *
     * solution 1：
     * 两个for循环，分别计算每次的值，然后保留一个最大值即可
     * solution2:
     * 分别从前后开始扫描，计算其面积。
     * 然后左边小于右边则左边+1，反之同理
     *
     *
     * @param height
     * @return
     */
    //time:O(n^2) space:O(1)
    public int maxArea(int[] height) {
        //solution 1: 两个for循环
        int res = 0;
        for (int i = 0; i < height.length; i++)
            for (int j = i + 1; j < height.length; j++){
                res = Math.max(res, Math.min(height[i], height[j]) * (j - i));
            }
        return res;
    }

    //time:O(n) space:O(1)
    public int maxArea2(int[] height) {
        int res = 0;
        int l = 0;
        int r = height.length - 1;
        while (l < r){
            res = Math.max(res, Math.min(height[l], height[r]) * (r - l));
            if(height[l] < height[r]) l++;
            else r--;
        }
        return res;
    }
}
```



