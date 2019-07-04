# 119. Pascal‘s Triangle II (07/04/2019) 补7/1

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/pascals-triangle-ii)

## 难度

**简单 Easy**

## 问题描述

Given a non-negative index *k* where *k* ≤ 33, return the *k*th index row of the Pascal's triangle. </br>

Note that the row index starts from 0.

![img](assets/PascalTriangleAnimated2.gif)

## 示例数据

```
Input: 3
Output: [1,3,3,1]
```

## 题意理解

输出该规律下的三角形某一行的数据。

## 题目分析

这个题跟[118题解法](https://github.com/halolong/Daily-LeetCode-Problem-With-Me/blob/master/Daily%20Notes/_118_PascalsTriangle.md)一样，但是由于从0开始。以输入的3为例，则就是第四行，所以计算的时候需要注意加1。

## Test case

```
Input: 3

i = 0:
list = [1];

i = 1:
list = [1, 1];

i = 2:
list = [1, 1, 1];
符合里面的计算
list = [1, *1 + 1*, 1] = [1, 2, 1];

i = 3:
list = [1, 1, 2, 1];
符合里面的运算
list = [1, *1 + 2*, 2, 1] = [1, 3, 2, 1];
list = [1, 3, *2 + 1*, 1] = [1, 3, 3, 1];
```

## 参考代码

```java
package com.leetcode.array;

import java.util.ArrayList;
import java.util.List;

public class _119_PascalsTriangleII {

    /**
     * LeetCode 119. Pascal's Triangle II
     * When: 2019/03/16
     * Time: O(n^2)
     * space: O(n)
     *
     * test case:
     * rowIndex=3
     * i = 0; i < 4
     *  (1) i = 0; res = [1,]
     *      未进入第二个循环
     *  (2) i = 1; res = [1, 1, ]
     *      未进入第二个循环
     *  (3) i = 2; res = [1, 1, 1, ];
     *      j = 1; j < 2;
     *      res = [1, 2, 1];
     *  (4) i = 3; res = [1, 1, 2, 1];
     *      j = 1; j < 3;
     *      res = [1,3,2,1]
     *
     *      res = [1,3,3,1]
     *
     * @param rowIndex
     * @return
     */
    public static List<Integer> getRow2(int rowIndex) {
        List<Integer> res = new ArrayList<>();
        if (rowIndex < 0) return res;
        for (int i = 0; i < rowIndex + 1; i++) {
            res.add(0, 1);
            for (int j = 1; j < res.size() - 1; j++) {
                res.set(j, res.get(j) + res.get(j + 1));
            }
        }
        return res;
    }
}

```



