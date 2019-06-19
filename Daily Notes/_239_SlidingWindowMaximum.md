# 239. Sliding Window Maximum（06/19/2019）

> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/sliding-window-maximum/)

## 难度

**困难 Hard**

## 问题描述

Given an array *nums*, there is a sliding window of size *k* which is moving from the very left of the array to the very right. You can only see the *k* numbers in the window. Each time the sliding window moves right by one position. Return the **max sliding window.**

## 示例数据

```
Input: nums = [1,3,-1,-3,5,3,6,7], and k = 3
Output: [3,3,5,5,6,7] 
Explanation: 

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

## 题意理解

以k为大小的框进行移动，然后得到每次框中的最大值。

## 题目分析

首先的话，通过题目的意思，了解到需要保持一个为k大小的移动框，并且返回其中的最大值。所以，暴力解法则就是通过两个循环并且第二个循环以k为间距，进行比较，然后得到每次的最大值，但是这样的方法时间复杂度则会为`O((n - k + 1) * k)`，在最差的情况下，能够达到`O(n^2)`。</br>

第二种方法则是使用**Deque**(双向链表)，将其维持成一个以nums值递减的序列(里面保存着该nums对应的index)，在`i >= k - 1 `的时候进行peek操作加入到结果数组中，这里也需要注意维持以k为大小的框。所以，如果当前这个队列首的index等于i - k的话，则需要弹出一个，因为已经超过了以k大小的框。</br>

当然，为了方便理解我也找了较多的资料，其中我觉得较为不错的是这个人的视频[https://www.youtube.com/watch?v=J6o_Wz-UGvc](https://www.youtube.com/watch?v=J6o_Wz-UGvc)。

## Test case

```
Input: nums = [1,3,-1,-3,5,3,6,7], and k = 3

i = 0:
	queue: 0 ->

i = 1:
	弹出0 然后插入1 queue: 1 ->

i = 2:
	queue: 1->2
	res = [3, ];
	
i = 3: 
	queue: 1->2->3
	res = [3, 3, ];

i = 4:
	由于5比任何值都大，所以全部弹出。
	queue: 4->
	res = [3, 3, 5, ];

i = 5: 
	queue: 4->5->
	res = [3, 3, 5, 5, ];
	
i = 6:
	由于6比任何值都大，所以全部弹出。
	queue: 6->
	res = [3, 3, 5, 5, 6, ];

i = 7:
	由于7比任何值都大，所以全部弹出。
	queue: 7->
	res = [3, 3, 5, 5, 6, 7];
```

## 参考代码

```java
package com.leetcode.array.counter;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Deque;
import java.util.LinkedList;

public class _239_SlidingWindowMaximum {

    /**
     * 239. Sliding Window Maximum
     * when: 2019/03/26
     *
     * 涉及到的数据结构：
     * deque
     * @param nums
     * @param k
     * @return
     */

    public static int[] maxSlidingWindow(int[] nums, int k) {
        //solution2: deque Time: O(n) Space: O(n)
        // deque 存的是index 并且从大到小排列
        // https://www.youtube.com/watch?v=J6o_Wz-UGvc
        if (nums == null || nums.length == 0){
            return new int[0];
        }
        Deque<Integer> deque = new LinkedList<>();
        int[] res = new int[nums.length - k + 1];
        for (int i = 0; i < nums.length; i++){
            // 保持不能越界即k的大小；这种情况 [1, -1] k = 1会发生
            if (!deque.isEmpty() && deque.peekFirst() == i - k){
                deque.poll();
            }
            // 这里主要就是保持递减的排序
            // as long as nums[i] has value greater than deque, keep popping elements of deque
            while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]){
                deque.removeLast();
            }
            deque.offer(i);
          	// 这里已经满足了 k = 3 这个框
            if (i >= k - 1){
                res[i + 1 - k] = nums[deque.peek()];
            }
        }
        return res;
    }

  	// brute force solution
    //time: O( (n-k+1) * k) 当k= n/2 则是 n^2 space: O(1)
    public static int[] maxSlidingWindow2(int[] nums, int k) {
        if (nums.length < 1 || nums == null) return new int[0];
        ArrayList<Integer> res = new ArrayList<>();
        for (int i = 0; i < nums.length - k + 1; i++) {
            int max = nums[i];
            for (int j = i; j < i + k; j++) {
                max = Math.max(max, nums[j]);
            }
            res.add(max);
        }
        int[] result = new int[res.size()];
        for (int i  = 0; i < res.size(); i++){
            result[i]=res.get(i);
        }
        return result;
    }
}

```



