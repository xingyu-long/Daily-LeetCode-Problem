# 122. Best Time to Buy and Sell Stock II(07/08/2019) 

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

## 难度

**简单 Easy**

## 问题描述

Say you have an array for which the *i*th element is the price of a given stock on day *i*. </br>

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).</br>

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

## 示例数据

```
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4. Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
             

Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4. Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.
```

## 题意理解

先购买然后卖出，多次这样的交易，达到最大利益值。

## 题目分析

![Profit Graph](assets/122_maxprofit_1.PNG)

就如上图所示，主要的利益来自于 `peak - valley` 的差值之和，并且这个肯定大于”最高点减去最低点的值“，因为这中间有很多段。所以只需要一直找 `peak` 和 `valley`就可以了。

## Test case

```
Input: [1,2,3,4,5]

i = 0:
valley = price[0];

由于符合条件 
i = 4;
peak = price[4];

maxProfit = peak - valley = 5 - 1 = 4;
结束
return 4;
```

## 参考代码

```java
package com.leetcode.array;

public class _122_BestTimetoBuyandSellStockII {

    /**
     *  122. Best Time to Buy and Sell Stock II
     *  when: 2019/03/21
     *  Review1: 2019/7/8
     *
        solution1 :
        (1) Peak Valley 方法：相当于寻找每一个连续的valley和peak 然后算出profit再加在一起
        (2) 跟上面其实一样，只需要关注连续的部分即可
     *
     * @param prices
     * @return
     */
    // time:O(n) space:O(1)
    public int maxProfit(int[] prices) {
        // solution 1:
        // 判断边界条件
        if (prices == null || prices.length < 2) return 0;
        int i = 0;
        int valley = prices[0];
        int peak = prices[0];
        int maxProfit = 0;
        while (i < prices.length - 1) { //这里是因为后面的操作总是会有i+1
            while (i < prices.length - 1 && prices[i] >= prices[i + 1])
                i++;
            valley = prices[i];
            while (i < prices.length - 1 && prices[i] <= prices[i + 1])
                i++;
            peak = prices[i];
            maxProfit += peak - valley;
        }
        return maxProfit;
    }

    // time:O(n) space:O(1)
    public int maxProfit2(int[] prices) {
          if (prices == null || prices.length < 2) return 0;
          int maxprofit = 0;
          for (int i = 1; i < prices.length; i++){
               if(prices[i] > prices[i - 1])
                   maxprofit += prices[i] - prices[i - 1];
          }
          return maxprofit;
    }
}

```



