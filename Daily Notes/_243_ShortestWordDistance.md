# 243.Shortest Word Distance(07/04/2019) 

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/majority-element-ii)

## 难度

**简单 Easy**

## 问题描述

Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

## 示例数据

```
Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

Given word1 = “coding”, word2 = “practice”, return 3.
Given word1 = "makes", word2 = "coding", return 1.
```

## 题意理解

找出两个元素存在的最小距离。

## 题目分析

这里存在 `O(n^2)` 和 `O(n) ` 的解法，其中的区别就是是否用常量来做记录位置，然后计算最小距离。第一种解法，则是两个 for 循环，当找到第一个目标字符，然后找第二个目标字符，其中都满足的情况，计算其距离，找出最小的距离值。

## Test case

```
Assume that words = ["practice", "makes", "perfect", "coding", "makes"].
Given word1 = "makes", word2 = "coding"

a = -1;
b = -1;
res = words.length;

当 i = 1 的时候:
a = 1;
b = -1;

当 i = 3 的时候:
a = 1;
b = 3;
res = 2;

当 i = 4的时候
a = 4;
b = 3;
res = 1;
结束
return res;
```

## 参考代码

```java
package com.leetcode.array;

import java.util.ArrayList;
import java.util.Collections;
import java.util.HashMap;
import java.util.List;

public class _243_ShortestWordDistance {

    /**
     * 243. Shortest Word Distance
     * When: 2019/03/18
     * Review1: 2019/7/4
     *
     */

    // solution2: 依然是n*n 的解法，具体思路跟上面一致，只是更加简单
    // time: O(n^2) space: O(1)
    public static int shortestDistance1(String[] words, String word1, String word2){
        int res = words.length;
        for (int i = 0; i < words.length; i++){
            if (words[i].equals(word1)){
                for (int j = 0; j < words.length; j++){
                    if (words[j].equals(word2)){
                        res = Math.min(res, Math.abs(i - j));
                    }
                }
            }
        }
        return res;
    }

    /**
     * solution3： 依然用获取其位置后然后比较的方式
     *
     * space: O(1)
     * time: O(n)
     * @param words
     * @param word1
     * @param word2
     * @return
     */
    public static int shortestDistance2(String[] words, String word1, String word2) {
        int res = words.length;
        int a = -1;
        int b = -1;
        for (int i = 0; i < words.length; i++) {
            if (words[i].equals(word1)) {
                a = i;
            } else if (words[i].equals(word2)) {
                b = i;
            }

            if (a != -1 && b != -1) {
                res = Math.min(res, Math.abs(a - b));
            }
        }
        return res;
    }
}

```



