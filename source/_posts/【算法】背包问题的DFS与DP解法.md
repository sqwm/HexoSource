---
title: 【算法】背包问题的DFS与DP解法
date: 2019-03-14 20:03:54
tags: Algorithm
categories: 算法
thumbnail: "https://upload.wikimedia.org/wikipedia/commons/thumb/f/fd/Knapsack.svg/250px-Knapsack.svg.png"
comments: true
toc: true
---
### Kanapsack Problem
-----------------------

<!-- more -->

#### 问题描述：

> 有n件物品，每件物品重w[i]，价值为c[i]。现在需要选出若干件物品放入一个容量为V的背包中，使得在选入背包的物品总重量不超过背包限重的情况下，让背包内的物品总价值达到最大。

##### DFS解法：
##### 算法思想：
> 对于每件物品，有两种情况（选，或不选）。若选择该物品，则将更新背包内的总重与总价值量，若不选择该物品，则跳过它去判断下一件物品，当处理完n件物品后，此时记录的sumW和sumC就是所选物品的总质量和总价值。如果sumW不超过V且sumC比MaxValue还大，就更新MaxValue。
> 
```c++
#include <iostream>
#include <string>
#include <cstdio>
#define Maxn 10
using namespace std;

int n,V,MaxValue = 0;//n为物品的总件数，V为背包的容量，MaxValue为最大价值
int w[Maxn],c[Maxn];//w[i]为每件物品的重量,c[i]为每件物品的价值

void DFS_Kanapsack(int index,int sumW,int sumC)
{
	if(index == n)//已完成对n件物品的选择
	{
		if(sumW <= V && sumC > MaxValue)
		{
			MaxValue = sumC;//更新最大价值
		}
		return;
	}
	//
	DFS_Kanapsack(index+1,sumW,sumC);//不选择第index件物品
	DFS_Kanapsack(index+1,sumW + w[index],sumC + c[index]);//选择第index件物品
}

int main()
{
	cin >> n >> V;
	for(int i = 0;i < n;i++)//输入每件物品的重量
	{
		cin >> w[i];
	}
	for(int i = 0;i < n;i++)//输入每件的价值
	{
		cin >> c[i];
	}
	DFS_Kanapsack(0,0,0);//初始时为第0件物品，重量为0，价值为0;
	cout << MaxValue << endl;

	return 0;
}
```
----------------------
> 由于每种物品有两种选择，因而易得上述算法的时间复杂度为$2^n$;
> 这显然很是糟糕，因为在上述算法中，总是把对n件物品的选择全部确定后才去更新最大价值，但是却忽略了背包容量总是不能超过V这个点，也就是说，我们可以把选择index物品放入对上述条件的判断之中，若选择index后重量不超过V则才选择它。
#### 改进后的算法：
```c++
void DFS_Kanapsack(int index,int sumW,int sumC)
{
	if(index == n)
	{
		return;
	}
	DFS_Kanapsack(index+1,sumW,sumC);

	if(sumW + w[index] <= V)
	{
		if(sumC + c[index] > MaxValue)
		{
			MaxValue = sumC + c[index];
		}
		DFS_Kanapsack(index+1,sumW+w[index],sumC+c[index]);
	}
}
```
---------------

