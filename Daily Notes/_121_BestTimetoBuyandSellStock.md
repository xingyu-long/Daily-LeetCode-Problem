# 121. Best Time to Buy and Sell Stock（06/16/2019）

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

## 难度

**简单 easy**

## 问题描述

Say you have an array for which the **i<sup>th</sup>** element is the price of a given stock on day *i*. </br>

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the **maximum profit**. </br>

Note that you cannot sell a stock before you buy one.

## 示例数据

```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```

## 题意理解

首先买一个物品然后再卖出去，找出最大的利润。

## 题目分析

正如题目要求，我们需要完成一次交易，首先是买入然后再卖出。其中需要达到利益最大化，则就是两者的差值达到最大，即需要买入的时候最少，卖出的时候钱最多。在这里首先能够想到的粗暴的解法就是两个`for`循环依次保存值，然后得到最大的。但是，这样的时间复杂度会很高，达到了`O(n * n)`。但是这也提供了一个思路，则就是我们需要一直保存最小买入值*min*和利益*profit*，通过这样的话，只需要循环一遍即可。

## Test case

```
Input: [7, 1, 5, 3, 6, 4]
min = prices[0] = 7;
profit = 0;

the inside of for loop
  min = Math.min(min, price);
  profit = Math.max(profit, price - min);
  
第1个元素 7 :
	min保持不变
	profit保持不变
	
第2个元素 1 :
	min = 1;
	profit保持不变
	
第3个元素 5 :
	min = 1;
	profit = 5 - 1 = 4;
	
第4个元素 3 :
	min = 1; 
	profit = 4;
	
第5个元素 6 :
	min = 1;
	profit = 6 - 1 = 5;

第6个元素 4 :
	min = 1;
	profit不变

return profit = 5;
```

## 参考代码

```java
package com.leetcode.array;

public class _121_BestTimetoBuyandSellStock {

    /**
     * 121. Best Time to Buy and Sell Stock
     * when: 2019/03/21
     *
     * solution: 利用min以及profit 初始化，然后找到最小的min
     * 并且跟着算最大的profit以之前的profit比较
     * 这个思路还是很值得考虑
     *
     * @param prices
     * @return
     */
    public int maxProfit(int[] prices) {
      	if (prices == null || prices.length < 2) return 0;
      	int min = prices[0];
      	int profit = 0;
      	for (int price : prices) {
         	min = Math.min(price, min);
          profit = Math.max(price - min, profit);
        }
      	return profit;
    }
}

```



