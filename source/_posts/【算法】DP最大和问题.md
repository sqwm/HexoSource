---
title: 【算法】DP最大和问题
date: 2019-03-17 19:55:27
tags: Knapsack
categories: 算法
thumbnail: "https://media-cdn.jiuzhang.com/course/dp3_LkMISIN.png"
comments: true
toc: true
---
### 动态规划
------------

<!-- more -->

#### 问题描述：
> 给定一个整数数字序列（用数组表示），在这个数列中选择若干个互不相邻的数，使得这些数的和达到最大值。

#### 分析：
> 属于01背包问题同类问题，对于每一个数，都有两种选择（选或不选）。假设给定数组set[]的长度为n，最终要求OPT(n-1)的结果,也就是从下标0到下标n-1这些数中能组成的最大和，而要求OPT(n-1)就分为两种情况：
> 1.选择set[n-1],因为不能出现相邻选项故OPT[n-1]的结果为set[n-1]与OPT[n-3]的和。
> 2.不选择set[n-1],则OPT[n-1]的结果就与OPT[n-2]相等。
判断出口：
不难看出，OPT[0] = set[0]，OPT[1] = max(set[0],set[1]);

![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/%E3%80%90%E7%AE%97%E6%B3%95%E3%80%91DP%E6%9C%80%E5%A4%A7%E5%92%8C%E9%97%AE%E9%A2%98/20190317082529638.png)
#### 因此其状态转移方程为：
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/%E3%80%90%E7%AE%97%E6%B3%95%E3%80%91DP%E6%9C%80%E5%A4%A7%E5%92%8C%E9%97%AE%E9%A2%98/20190317083401575.png)

------
#### 算法实现：
*递归实现：*
```c++
int OPT(int i)
{
	if(i == 0) return set[0];
	if(i == 1) return set[0]>set[1] ? set[0]:set[1];
	int a = OPT(i-1);
	int b = OPT(i-2)+set[i];
	return a>b?a:b;
}
```
*DP实现：*
```c++
int OPT_(int set[],int m)
{
	int *opt = new int[100];//状态数组
    //出口
	opt[0] = set[0];
	opt[1] = set[0]>set[1] ? set[0]:set[1];
	for(int i = 2;i < m;i++)
	{
		int a = opt[i-1];
		int b = opt[i-2] + set[i];
		opt[i] = a>b?a:b;
	}
	return opt[m-1];
}
```
*测试：*
> 输入：{1,5,8,9,7,8,2,1,6,3}
> 输出：
> ![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/%E3%80%90%E7%AE%97%E6%B3%95%E3%80%91DP%E6%9C%80%E5%A4%A7%E5%92%8C%E9%97%AE%E9%A2%98/20190317084336292.png)