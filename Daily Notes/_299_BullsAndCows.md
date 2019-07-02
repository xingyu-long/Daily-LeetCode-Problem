# 299. Bulls And Cows (07/01/2019) 补6/28

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/bulls-and-cows)

## 难度

**中等 Medium**

## 问题描述

You are playing the following [Bulls and Cows](https://en.wikipedia.org/wiki/Bulls_and_Cows) game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates **how many digits in said guess match your secret number exactly in both digit and position (called "bulls")** and **how many digits match the secret number but locate in the wrong position (called "cows")**. Your friend will use successive guesses and hints to eventually derive the secret number.</br>

Write a function to return a hint according to the secret number and friend's guess, use `A` to indicate the bulls and `B` to indicate the cows. </br>

Please note that both secret number and friend's guess may contain duplicate digits.

## 示例数据

```
Input: secret = "1807", guess = "7810"

Output: "1A3B"

Explanation: 1 bull and 3 cows. The bull is 8, the cows are 0, 1 and 7.
```

## 题意理解

找到同样位置、并且相同值的bulls值以及不同位置但值相同的cows值

## 题目分析

一开始都能想到的就是计算相同位置和相同值的bulls，因为可以直接循环以及比较实现。</br>

有一种暴力解法，则就是通过两个ArrayList来实现，一个保存相同的情况，一个保存不同的情况。使用guess的字符串中每个字符进行比较，当该值不存在于相同的ArrayList并且存在于不同的数组里面，所以就符合该情况（cow++ 然后不同的ArrayList里面删除该元素）。当元素存在于相同的ArrayList里面，则删除，防止重复计算。</br>

另外一种高超的解法，首先新建一个长度为10的数组（辅助计数）count，然后循环判断该位置的secret单个字符小于0的话，就cow加1，以及每次计算完后的加加操作。对于guess则是相反，该位置的guess单个字符大于0的话，就cow加1，以及每次计算完后的减减操作。有点类似于信号量的感觉（secret这一列出现的就加操作，guess出现的就减操作）。

## Test case

```
Input: secret = "1807", guess = "7810"

bulls = 0;
cows = 0;
index = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
				 0, 0, 0, 0, 0, 0, 0, 0, 0, 0
				 
i = 0: 
index = [0, 1, 2, 3]
				[1, 8, 0, 7]
				 *
				[7, 8, 1, 0]
				 * 
index = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
				 0, 1, 0, 0, 0, 0, 0, -1, 0, 0
				 
i = 1:
secret.charAt(1) == guess.charAt(1) 
bulls++; // bulls = 1;

i = 2:
index = [0, 1, 2, 3]
				[1, 8, 0, 7]
				 			 *
				[7, 8, 1, 0]
				       * 
index = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
				 1, 0, 0, 0, 0, 0, 0, -1, 0, 0
cows++;//cows = 1;

i = 3:
index = [0, 1, 2, 3]
				[1, 8, 0, 7]
				 			 		*
				[7, 8, 1, 0]
				      		* 
index = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
				 0, 0, 0, 0, 0, 0, 0, 0, 0, 0
cows++;//cows = 2;
cows++;//cows = 3;

return "1A3B";
```

## 参考代码

```java
package com.leetcode.array;

import java.util.ArrayList;
import java.util.Hashtable;
import java.util.Map;

public class _299_BullsAndCows {

    /**
     *  299. Bulls and Cows
        When: 2019/3/11-12
        review1: 2019/7/1
     * @param secret
     * @param guess
     * @return
     */

    //time: O(n) space: O(n)
    public static String getHint(String secret, String guess) {
        if (secret.length() == 0 || guess.length() == 0) return "0A0B";
        // 计算 Bull
        int bull = 0;
        // 计算 cow
        int cow = 0;
        // 保存secret中与guess不同的数组
        ArrayList<Character> diff = new ArrayList<>();
        // 记录相同的元素
        ArrayList<Character> same = new ArrayList<>();
        for (int i = 0; i < secret.length(); i++){
            if (secret.charAt(i) == guess.charAt(i)) {
                bull++;
                same.add(secret.charAt(i));
            }
            else {
                diff.add(secret.charAt(i));
            }
        }
        /**
         * 1. 利用guesss数组反着寻找
         * 2. 排除已经相同（为bull元素）
         * 3. arr含有temp就删除一个
         * 4. map里面含有temp的话 就删除一个元素并且cow+1
         */
        for (int i = 0; i < guess.length(); i++){
            char temp = guess.charAt(i);
            if(! same.contains(temp)){
                if(diff.contains(temp)){
                    cow++;
                    int index = diff.indexOf(temp);
                    diff.remove(index);
                }
            }else{
                //防止重复使用
                int index = same.indexOf(temp);
                same.remove(index);
            }
        }
        return bull+"A"+cow+"B";
    }

    //利用新的数组来记录其每个数组出现的次数，其中secret++，guess--即可
    public static String getHint2(String secret, String guess) {
         if (secret.length() == 0 || guess.length() == 0) return "0A0B";
      	int bulls = 0;
      	int cows = 0;
      	int[] count = new int[10]; 
      	for (int i = 0; i < secret.length(); i++) {
          	if (secret.charAt(i) == guess.charAt(i)) {
              	bulls++;
            } else {
              	if (count[secret.charAt(i) - '0']++ < 0) cows++;
              	if (count[guess.charAt(i) - '0']-- > 0) cows++;
            }
        }
      	return bulls + "A" + cows + "B";
    }
}

```



