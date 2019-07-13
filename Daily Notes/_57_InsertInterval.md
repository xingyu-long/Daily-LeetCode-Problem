# 57. Insert Interval (07/13/2019) 
> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/insert-interval)

## 难度

**困难 Hard**

## 问题描述

Given a set of *non-overlapping* intervals, insert a new interval into the intervals (merge if necessary).</br>

You may assume that the intervals were initially sorted according to their start times.

## 示例数据

```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]

Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```

## 题意理解

插入新的区间，与之前进行合并操作。

## 题目分析

该题可以分为三种情况。newInterval 的开始都大于原来的 Interval 的结束，所以直接将其加入结果中；另外一种则是相交，经过观察发现，可以直接使用 newInterval 的结束大于等于原来的 Interval的开始表示其相交的状态，并且在这里需要更新其每次循环的目标；最后剩下的部分都属于大于原来，所以直接加入结果中。其中相交的情况，则需要计算出前面的最短以及后面的最大值，来保持 new

## Test case

```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]

resOfEach = {[]};
i = 0:
newInterval[0] = min(1, 2) = 1;
newInterval[1] = max(3, 5) = 5;
resOfEach = {[1, 5]};

i = 1:
不相交
直接加入
resOfEach = {[1, 5], [6, 9]}

res = [[1, 5],
			 [6, 9]
			];

```

## 参考代码

```java
package com.leetcode.array;

import java.util.ArrayList;
import java.util.List;

public class _57_InsertInterval {
    /**
     *  No.57 Insert Interval
     *  when: 2019/03/13 & 3/14
     *  Review1:2019/7/13
     * update: 2019/06/17 应该使用更加易懂的方式进行
     *
     * 解题思路：
     * 首先一个循环表示以前的每一个数组
     * 分三种情况：
     *  1. 原数组的end < 新数组的start 直接插入res
     *  2. 原数组的start <= 新数组的end 则是比较两个数组的start 最小作为首 两个数组的end 最大作为尾
     *  3. 原数组的start > 新数组的end 直接插入res
     *  这里的含义是数组 但是可以理解为就是interval对象 然后有start以及end 属性
     *  这里之前有while的方法容易超时，内存不够（应该是进入死循环）
     *  利用for循环来遍历Interval 然后分上面的三种情况进行处理。
     *
     *  涉及到的数据结构或者方法： ArrayList<>()
     * @param intervals
     * @param newInterval
     * @return
     */
    // time: O(n) space:O(n)
    public int[][] insert(int[][] intervals, int[] newInterval) {
        if (newInterval.length == 0) {
            return intervals;
        }
        List<int[]> resOfEach = new ArrayList<>();
        int index = 0;

        // 表明新数组的开头都大于前面的结尾，则一直添加原来的
        while (index < intervals.length && intervals[index][1] < newInterval[0]) {
            resOfEach.add(intervals[index]);
            index++;
        }

        // 表明各种能够交叉的情况,并且考虑重合的情况 所以要 <=
        while (index < intervals.length && intervals[index][0] <= newInterval[1]) {
            newInterval[0] = Math.min(intervals[index][0], newInterval[0]);
            newInterval[1] = Math.max(intervals[index][1], newInterval[1]);
            index++;
        }
        resOfEach.add(newInterval);

        // 表明新的数组与原来的没有交集，所以最后加入剩下的即可
        while (index < intervals.length) {
            resOfEach.add(intervals[index++]);
        }

        int[][] res = new int[resOfEach.size()][2];
        int i = 0;
        for (int[] each : resOfEach) {
            res[i++] = each;
        }
        return res;
    }
}
```



