# 56. Merge Intervals (07/17/2019)

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/merge-intervals/ )

## 难度

**中等 Medium**

## 问题描述

Given a collection of intervals, merge all overlapping intervals.

```
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

## 题意理解

合并所有重复的区间。

## 题目分析

这个题和 [57.Insert Interval分析笔记](https://github.com/halolong/Daily-LeetCode-Problem-With-Me/blob/master/Daily%20Notes/_57_InsertInterval.md) 类似，主要的不同，这里是提供了全部 interval， 所以选择第一个作为之前解题里面的 newInterval 。并且，值得注意的是，需要一开始进行排序。排序之后，所以每个区间的开始都是按照升序排序，只需要考虑区间的结束。当选取的 newInterval 的结束大于等于循环区间的开始，则需要保留最大的结束值，相反，直接添加到结果集中，并且更新 newInterval 值。

## Test case

```
Input: [[1,3],[2,6],[8,10],[15,18]]

这里面已经有序，如果没有的话 按照interval[0]升序排序

newInterval = [1, 3]
start = 1;
end = 3;

for loop
第一个元素 [1, 3] end = 3;

第二个元素 [2, 6] 3 >= 2 所以相交 end = Math.max(3, 6) = 6;
newInterval = [1, 6];

第三个元素 [8, 10] 6 < 8 不相交，直接加入之前的newInterval 然后更新newInterval
res = [[1, 6]];
newInterval = [8, 10];

第四个元素 [15, 18] 10 < 15 不相交，直接加入之前的newInterval 然后更新newInterval
newInterval = [15, 18];
循环完毕

加入最后一个到结果集中
res = [[1, 6], [8, 10], [15, 18]];

```

## 参考代码

```java
package com.leetcode.array;

import java.util.*;

public class _56_MergeIntervals {
    /**
     * LeetCode No 56. Merge Intervals
     * when: 2019/03/14
     *
     * 思路：都与InsertIntervals 一致 只是从中抽出第一个就行（由于现在的数据是可能内部有overlap而不是像之前没有的情况）
     * 利用所谓的扫描线算法 （第一个的interval处理也很重要） 需要先排序
     * 这里需要先sort！！！(这里sort之后 第一个的start 就一直是第一个输入的start！)
     *
     * 涉及到的数据结构或者方法： 利用new comparator写sort 第一个对象-第二个对象则就是正序
     * @param intervals
     * @return
     */
    // time:O(nlogn) for sorting space: O(n)
    public static int[][] merge(int[][] intervals) {
        if (intervals == null || intervals.length < 1) return intervals;
        Arrays.sort(intervals, new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                if (o1[0] > o2[0]) return 1;
                else if (o1[0] < o2[0]) return -1;
                else return 0;
            }
        });
        int index = 0;
        int start = intervals[index][0];
        int end  = intervals[index][1];
        int[] newInterval = new int[]{start, end};
        List<int[]> resOfEach = new ArrayList<>();

        // 这里不用比较start是否最小 是因为前面排序了。而57题 插入的newInterval是不确定的，所以需要前后均比较
        for (int[] interval: intervals){
            if (interval[0] <= newInterval[1]){
                newInterval[1] = Math.max(newInterval[1], interval[1]);
            } else {
                resOfEach.add(new int[]{newInterval[0], newInterval[1]});
                newInterval[0] = interval[0];
                newInterval[1] = interval[1];
            }
        }
        // 插入最后一个
        resOfEach.add(newInterval);
        int[][] res = new int[resOfEach.size()][2];
        int i = 0;
        for (int[] each : resOfEach) {
            res[i++] = each;
        }
        return res;
    }
}
```



