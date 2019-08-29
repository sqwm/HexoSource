---
title: 图解LeetCode295_Hard_MedianFinder
date: 2019-08-29 10:50:38
tags: LeetCode
categories: 算法
thumbnail: 
comments: 
toc: true
disqusId: ccyhweb
---

# [LC295] 数据流中的中位数(类设计）

## 题目描述：
中位数是有序列表中间的数。如果列表长度是偶数，中位数则是中间两个数的平均值。

<!-- more -->

**例如：**

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

void addNum(int num) - 从数据流中添加一个整数到数据结构中。
double findMedian() - 返回目前所有元素的中位数。
**示例：**
```c++
    addNum(1)
    addNum(2)
    findMedian() -> 1.5
    addNum(3) 
    findMedian() -> 2
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-median-from-data-stream

---
## 算法分析

维护两个堆（一个大顶堆bigger，一个小顶堆smaller）来保存数据流中流过来的数字。无论何时都要保持abs(bigger.size-smaller.size)<=1;并且保证大顶堆内的数字的值全都小于或等于小顶堆内的数字的值，这样就能保证大顶堆保存的是数据流中较小的一半数字，而小顶堆中保存的是另外较大的一半。

---
### findMedian 函数设计
&emsp;&emsp;如此一来，不难发现数据流的中位数查找函数 findMedian() 的逻辑就为(伪代码)：
```c++
if smaller.size == bigger.size:
    return (smalle.top + bigger.top)/2;
else if smaller.size > bigger.size:
    return smaller.top;
else
    return bigger.top;
```

---
### addNum 函数设计
&emsp;&emsp;addNum() 函数在添加元素的过程中保持两个堆的动态平衡：
```
Condition 1.保证两堆元素个数相差不超过 1
Condition 2.保证大顶堆中的元素小于等于小顶堆中的任何元素
```
#### case 1:
* 如果两堆中的元素个数相同。这个时候无论插入哪一个堆，条件 1 都不会被破坏,因此考虑条件 2 ，将待插入元素与两堆的堆顶比较:若待插入元素为 5，显然这个时候若插入smaller会破坏条件 2，因此因插入bigger中。而若待插入为 9 则显然应插入 smaller 中。

<center>

![](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/%5BLeetcode295_hard%5DMedianFinder/case1.png)

![](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/%5BLeetcode295_hard%5DMedianFinder/case1_1.png)

</center>

---
#### case 2:
* 如果大顶堆元素个数小于小顶堆的元素个数。此时，将待插入元素与两堆堆顶比较:
* 若小于等于Bigger.top则直接插入Bigger中；
* ![](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/%5BLeetcode295_hard%5DMedianFinder/case2.png)
* 若大于smaller.top则为了保证条件1,需将smaller中的最小值（根）转存至Bigger中。
* ![](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/%5BLeetcode295_hard%5DMedianFinder/case2_11.png)


---
#### case 3:
* 如果大顶堆的元素个数大于小顶堆的元素个数。此时，将待插入元素与两堆堆顶比较：
* 若其大于等于Smaller.top则直接插入Smaller中；
* ![](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/%5BLeetcode295_hard%5DMedianFinder/case3_1.png)
* 若小于Bigger.top则为了保证条件1，需将Bigger中的最大元素值（根）转存至Smaller中。
* ![](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/%5BLeetcode295_hard%5DMedianFinder/case3_2.png)

---
#### end