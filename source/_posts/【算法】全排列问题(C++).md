---
title: 【算法】全排列问题
date: 2019-03-13 12:32:26
tags: Algorithm
categories: 算法
thumbnail: "http://pic.5577.com/up/2014-8/20148148468.jpg"
comments: 
toc: true
---
#### 算法思想：

<!-- more -->

> 设定一个数组p用来存放当前排列，并用一个数组Hash用来标记已填入p中的数字。
> 按顺序将数字填入数组p中的第0位置第Max-1位，现在假设已经填好了p[0]~p[index-1]，正准备将数字填入index位置，若index位置未及Max（数组边界），则枚举0~Max-1；判断是否有数字未填入，若有则将其填入p中，同时在Hash中将该数字置为已填入。其后继续填入下一个位置index+1；当递归完成时，将Hash[i]还原为false（将i置为未填入）。

#### 代码实现：
```c++
#include <iostream>
#include <cstdio>
#include <cstdlib>
#define Max 10
using namespace std;
//列举从0到Max-1的全排列
int p[Max];//保存当前排列
bool Hash[Max] = {false};//标记i是否已填入p中，是为真，否为假；

void generate_x(int index)
{
	if(index == Max)//递归边界，已生成一种排列可能
	{
		for(int i = 0;i < Max;i++)//输出该排列
		{
			cout << p[i] << ' ';
		}
		cout << endl;
		return;
	}

	for(int i = 0;i < Max;i++)
	{
		if(Hash[i] == false)//判断i是否还未已填入p中
		{
			p[index] = i;//填入
			Hash[i] = true;//标记已填入
			generate_x(index+1);//填写下一个数
			Hash[i] = false;//处理完P[index] = i 的子问题，还原状态
		}
	}
}

int main()
{
	generate_x(0);//从0开始填入
	return 0;
}
```
#### 输出结果：
![](/【算法】全排列问题(C++)/20190313012239824.png)