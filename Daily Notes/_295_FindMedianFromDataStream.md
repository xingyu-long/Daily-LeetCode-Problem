# 295. Find
Median from Data Stream (07/12/2019) 
> 由于刷题习惯，题目均保持英文
>
> [LeetCode本文问题链接](https://leetcode.com/problems/find-median-from-data-stream)

## 难度

**困难 Hard**

## 问题描述

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.</br>

For example,</br>

```
[2,3,4], the median is 3
[2,3], the median is (2 + 3) / 2 = 2.5
```

Design a data structure that supports the following two operations:

- void addNum(int num) - Add a integer number from the data stream to the data structure.
- double findMedian() - Return the median of all elements so far.

## 示例数据

```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```

## 题意理解

找出一个数据流中的中位数。

## 题目分析

直接从问题出发，其实可以使用 sort 之后再寻找中位数，但是这样并不是最优解。如果使用堆排序，可以将其时间复杂度降为 logn。在这个题中，主要使用两个堆，分别是最大堆、最小堆。其中，最大堆存放数据中小的那一半，最小堆存放数据中大的一半。所以最小堆的堆顶大于最大堆的堆顶。</br>

这里面具体分三种情况。

* maxHeap.size() == minHeap.size()
  * 插入值 > maxHeap.peek()
    * 插入 minHeap
  * 插入值 <= maxHeap.peek()
    * 插入 maxHeap
* maxHeap.size() > minHeap.size()
  * 插入值 > maxHeap.peek()
    * 插入 minHeap
  * 插入值 <= maxHeap.peek()
    * 最大堆的堆顶 pop 出来然后 push 到最小堆
    * 插入 maxHeap
* maxHeap.size() < minHeap.size()
  * 插入值 < minHeap.peek()
    * 插入 maxHeap
  * 插入值 >= minHeap.peek()
    * 最小堆的堆顶 pop 出来然后 push 到最大堆
    * 插入 minHeap

## Test case

```
Input = [1,2,3,4]

i = 0: 
先加入 maxHeap
maxHeap:
	1
	/\

i = 1:
插入 minHeap
minHeap:
	2
	/\

i = 2:
插入到 minHeap
minHeap:
	2
	/\
	3
	
i = 3:
- 最小堆的堆顶 pop 出来然后 push 到最大堆
- 插入 minHeap
minHeap:
	3
	/\
	4
maxHeap:
	2
	/\
	1
return (2+3)/2;
```

## 参考代码

```java
package com.leetcode.stackPriorityQueue;

import java.util.Comparator;
import java.util.PriorityQueue;

public class _295_FindMedianFromDataStream {

    /**
     *  295. Find Median From Data Stream
     *  When:2019/7/12
     *  Difficulty: Hard
     *  Solution:
     *    two heaps
     */
    private PriorityQueue<Integer> minHeap;
    private PriorityQueue<Integer> maxHeap;

    /** initialize your data structure here. */
    public _295_FindMedianFromDataStream() {
        minHeap = new PriorityQueue<>(); //放置大的一半
        maxHeap = new PriorityQueue<>(new Comparator<Integer>() { // 放置小的那一半
            @Override
            public int compare(Integer o1, Integer o2) {
                if (o1 > o2) return -1;
                else if (o1 < o2) return 1;
                else return 0;
            }
        });
    }

    public void addNum(int num) {
        if (maxHeap.isEmpty()) {
            maxHeap.add(num);
            return;
        }

        if (maxHeap.size() == minHeap.size()) {
            if (num < maxHeap.peek()) {
                maxHeap.add(num);
            } else {
                minHeap.add(num);
            }
        } else if (maxHeap.size() > minHeap.size()) {
            if (num > maxHeap.peek()) {
                minHeap.add(num);
            } else {
                // 表示比最大堆的第一个元素小，所以应该在最大堆里面，但是由于这里本身元素就比最小堆多
                // 所以需要先把 maxHeap 的顶部弹出，放到 miniHeap，然后 num 加入到 maxHeap
                minHeap.add(maxHeap.poll());
                maxHeap.add(num);
            }
        } else { // maxHeap.size() < minHeap.size()
            if (num < minHeap.peek()) {
                maxHeap.add(num);
            } else {
                maxHeap.add(minHeap.poll());
                minHeap.add(num);
            }
        }
    }

    public double findMedian() {
        if (minHeap.size() == maxHeap.size()) {
            return (double)(maxHeap.peek() + minHeap.peek()) / 2;
        } else if (minHeap.size() > maxHeap.size()) {
            return minHeap.peek();
        } else {
            return maxHeap.peek();
        }
    }

    public static void main(String[] args) {
        _295_FindMedianFromDataStream find = new _295_FindMedianFromDataStream();
        find.addNum(1);
        find.addNum(2);
        System.out.println(find.findMedian());
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */

```



