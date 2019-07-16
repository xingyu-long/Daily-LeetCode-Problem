# 387. First Unique Character In A String(07/16/2019)
> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/first-unique-character-in-a-string)

## 难度

**简单 Easy**

## 问题描述

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

```
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```

## 题意理解

求该数组中第一个非重复的字符。

## 题目分析

这个题主要需要记录每个字符所占的个数，并且再一次重复循环其数组的时候，如果该字符的个数只等于1，那么这个字符就是目标字符了。

## Test case

```
s = "leetcode"

count['l' - 'a'] = 1;
count['e' - 'a'] = 3;
count['t' - 'a'] = 1;
count['c' - 'a'] = 1;
count['o' - 'a'] = 1;
count['d' - 'a'] = 1;

结束
第一个则就是 'l' 字符的位置 
```

## 参考代码

```java
package com.leetcode.string;

public class _387_FirstUniqueCharacterInAString {

    /**
     *  387. First Unique Character in a String
     *  When:2019/7/16
     *  Difficulty: Easy
     *  solution:
     *  用一个字符数组记录个数，然后看==1的那个i输出即可
     * @param s
     * @return
     */
    public static int firstUniqChar(String s) {
        int[] count = new int[26];
        for (int i = 0; i < s.length(); i++) {
            count[s.charAt(i) - 'a']++;
        }
        for (int i = 0; i < s.length(); i++) {
            if (count[s.charAt(i) - 'a'] == 1) {
                return i;
            }
        }
        return -1;
    }
}
```



