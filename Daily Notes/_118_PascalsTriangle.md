# 118. Pascal‘s Triangle(07/04/2019) 补6/30

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/pascals-triangle)

## 难度

**简单 Easy**

## 问题描述

Given a non-negative integer *numRows*, generate the first *numRows* of Pascal's triangle.

![img](assets/PascalTriangleAnimated2.gif)

## 示例数据

```
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

## 题意理解

完成这样有规律的三角形的搭建。

## 题目分析

通过上面的动态演示，可以得知一个规律，每次都是从第2个开始计算并且前后都会保留1这个元素。其中的计算，则就是上层的元素累加。所以这个题可以直接暴力求解，每一层按照规律计算。但是👇的代码写出更加的优雅，代表了相同的含义。

## Test case

```
Input: 5

i = 0:
list = [1];
res = [[1], ];

i = 1:
list = [1, 1];
res = [[1], [1, 1]];

i = 2:
list = [1, 1, 1];
符合里面的计算
list = [1, *1 + 1*, 1] = [1, 2, 1];
res = [[1], [1, 1], [1, 2, 1]];

i = 3:
list = [1, 1, 2, 1];
符合里面的运算
list = [1, *1 + 2*, 2, 1] = [1, 3, 2, 1];
list = [1, 3, *2 + 1*, 1] = [1, 3, 3, 1];
res = [[1], [1, 1], [1, 2, 1], [1, 3, 3, 1]];

i = 4:
list = [1, 1, 3, 3, 1];
符合里面的运算
list = [1, *1 + 3*, 3, 3, 1] = [1, 4, 3, 3, 1];
list = [1, 4, *3 + 3*, 3, 1] = [1, 4, 6, 3, 1];
list = [1, 4, 6, *3 + 1*, 1] = [1, 4, 6, 4, 1];
res = [[1], [1, 1], [1, 2, 1], [1, 3, 3, 1], [1, 4, 6, 4, 1]];

结束 返回
res = [[1], [1, 1], [1, 2, 1], [1, 3, 3, 1], [1, 4, 6, 4, 1]];
```

## 参考代码

```java
package com.leetcode.array;

import java.util.ArrayList;
import java.util.List;

public class _118_PascalsTriangle {
    /**
     * LeetCode 118. Pascal's Triangle
     * When: 2019/03/16
     * Review1: 2019/7/4
     * 思路：就是按照算法演示来相加 保留current以及previous行然后依次计算
     * <p>
     * 涉及到的数据结构或者方法：ArrayList(), List<>
     *
     * @param numRows
     * @return
     */

    //time: O(n^2) space:O(n)
    public static List<List<Integer>> generate(int numRows) {
        List<List<Integer>> res = new ArrayList<>();
        // 这里应该返回空数组并非null值
        if (numRows < 1) return res;

        List<Integer> list = new ArrayList<>();

        //赋值第一行
        list.add(0, 1);
        res.add(list);

        // 每一行的中间部分
        for (int i = 1; i < numRows; i++) {
            // 一个是当前的行
            List<Integer> current = new ArrayList<>();
            // 添加每一行的第一个元素 1
            current.add(1);

            // 一个表示当前行的前一行
            List<Integer> previous = res.get(i - 1);

            //当前属于第几行就有几个元素
            for (int j = 1; j < i; j++) {
                int temp = previous.get(j - 1) + previous.get(j);
                current.add(temp);
            }

            //添加每一行的最后一个元素 1
            current.add(1);
            res.add(current);
        }
        return res;
    }

    /**
     * 更加巧妙的方法
     */
    public static List<List<Integer>> generate2(int numRows) {
        List<List<Integer>> res = new ArrayList<>();
      	if (numRows < 1) return res;
      	List<Integer> list = new ArrayList<>();
      	for (int i = 0; i < numRows; i++) {
          	list.add(0, 1);
          	for (int j = 1; j < list.size() - 1; j++) {
              	list.set(j, list.get(j) + list.get(j + 1));
            }
          	res.add(new ArrayList<>(list));
        }
      	return res;
    }
}

```



