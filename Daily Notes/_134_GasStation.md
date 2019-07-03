# 134. Gas Station (07/03/2019) 补6/29

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/gas-station)

## 难度

**中等 Medium**

## 问题描述

There are *N* gas stations along a circular route, where the amount of gas at station *i* is `gas[i]`.<br/>

You have a car with an unlimited gas tank and it costs `cost[i]`of gas to travel from station *i* to its next station (*i*+1). You begin the journey with an empty tank at one of the gas stations.<br/>

Return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1.<br/>

**Note:**

- If there exists a solution, it is guaranteed to be unique.
- Both input arrays are non-empty and have the same length.
- Each element in the input arrays is a non-negative integer.

## 示例数据

```
Input: 
gas  = [1,2,3,4,5]
cost = [3,4,5,1,2]

Output: 3

Explanation:
Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 4. Your tank = 4 - 1 + 5 = 8
Travel to station 0. Your tank = 8 - 2 + 1 = 7
Travel to station 1. Your tank = 7 - 3 + 2 = 6
Travel to station 2. Your tank = 6 - 4 + 3 = 5
Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.
Therefore, return 3 as the starting index.
```

## 题意理解

找到从哪一个加油站出发然后能够完全绕一圈，即走完全部车站。如果没有就返回-1，如果有则返回符合的出发加油站坐标。

## 题目分析

首先能够想到如何判断能够走完，其实就是gas的总和减去cost的综合大于等于0，则存在从某一个汽油站出发然后可以走完全部的情况。然后，继续分析，想到当前的gas如果小于当前的cost则说明该地方不适合出发，然后保留当前节点下一个。所以，就想到用剩余（remain）和亏欠（debt）来表示。其中remain用`gas - cost`表示，如果`remain < 0`则要算入debt，remain接着清空，结果位置向前移动一位（因为这里不可能符合，理由如前面第一点所述），有利于下一次计算。最后用remain - debt计算是否能够走到，并且返回结果。

## Test case

```
Input: 
gas  = [1,2,3,4,5]
cost = [3,4,5,1,2]

remain = 0;
debt = 0;
start = 0;

i = 0:
remain = -2;
满足小于0 
debt += remain; // debt = -2;
start = i + 1; // start = 1;
remain = 0;

i = 1:
remain = -2;
满足小于0
debt += remain; // debt = -4;
start = i + 1; // start = 2;
remain = 0;

i = 2:
remain = -2;
满足小于0
debt += remain; // debt = -6;
start = i + 1; // start = 3;
remain = 0;

i = 3:
remain = 3;
不满足

i = 4:
remain = 6;
不满足

6 - 6 >= 0 返回start，即3;
```

## 参考代码

```java
package com.leetcode.array;

public class _134_GasStation {
    /**
     *  134. Gas Station
     *  When: 2019/03/12

     * 解题思路：
     * 1. 首先通过累积和（总加油-总耗油）来计算是否存在这样的成立的情况
     * 2. 只要能够总的算下来 > 0 即可
     * 这个方法主要是表示只要在这个点之后的debt+remain都能做到 那就是从这个点出发即可
     * @param gas
     * @param cost
     * @return
     */

    //time: O(n) space:O(1)
    public static int canCompleteCircuit(int[] gas, int[] cost) {
        int start = 0; //起始位置
        int remain = 0; //当前剩余燃料
        int debt = 0; // 前面没能走完的路上欠的债
       	for (int i = 0; i < gas.length; i++) {
          	remain += gas[i] - cost[i];
          	if (remain < 0) {
              	debt += remain;
              	start = i + 1;
              	remain = 0;
            }
        }
        return remain + debt >= 0 ? start: -1;
    }
}

```



