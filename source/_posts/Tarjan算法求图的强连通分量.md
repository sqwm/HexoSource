---
title: Tarjan算法求图的强连通分量
date: 2019-11-21 21:58:23
tags: Algorithm
categories: 算法
thumbnail: 
comments: 
toc: true
disqusId: ccyhweb
---



## 强连通分量简介

&emsp;&emsp;有向图强连通分量：在有向图G中，如果两个顶点$V_i, V_j$ 间（vi>vj）有一条从$V_i$到$V_j$的有向路径，同时还有一条从$V_j$到$V_i$的有向路径，则称两个顶点强连通(strongly connected)。如果有向图G的每两个顶点都强连通，称G是一个强连通图。有向图的极大强连通子图，称为强连通分量(strongly connected components)。

<!-- more -->

&emsp;&emsp;比如下图：

<center>
![](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Tarjan/%E8%BF%9E%E9%80%9A%E5%9B%BE.PNG#pic_center)
</center>

---

## Tarjan 算法
&emsp;Tarjan算法是用来求强连通分量的，它是一种基于DFS（深度优先搜索）的算法，每个强连通分量为搜索树中的一棵子树。并且运用了数据结构栈。由于栈的先进先出的性质可以保证当前在栈中的结点中先入栈的结点必然有一条通路通往后入栈的结点，这样一来判断后入栈的结点是否有一条路径通向先入栈结点就成了算法要解决的主要问题。
**算法思路：**
&emsp;首先引入两个数组 dfn[maxn] 和 low[maxn], 其中 dfn[i] 表示编号为 i 的节点被访问时的时间戳；low[i] 表示从编号为 i 的节点可追溯到（到达）的最早被访问到的节点的时间戳。下面通过上述例子跑一遍算法，描绘出每个时刻的DFS树状态和栈中的内容。

<center>

![第一步](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Tarjan/1.PNG#pic_center)
![第二步](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Tarjan/2.PNG#pic_center)
![第三步](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Tarjan/3.PNG#pic_center)
![第四步](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Tarjan/4.PNG#pic_center)
![第五步](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Tarjan/5.PNG#pic_center)
![第六步](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Tarjan/6.PNG#pic_center)

</center>

&emsp;由上述过程可得该图由三个连通分量：{5}，{4}，{2,3,1,0}

---

## 算法实现：
> 代码中有详细注释，可结合上述图例分析
> 

```c++
#include <iostream>
#include <vector>
#include <stack>
#include <algorithm>
using namespace std;

/*  求强连通分量： Tarjan算法
    Tarjan 算法， 以Robert Tarjan的名字命名的算法
    该算法用来在线性时间内求解图的连通性问题
*/

class Ssc{
public:
    void Tarjan(int);
    Ssc(int n_, vector<vector<int>> &g) : n(n_) {         // InitializeMG
        graph = g;
        dfn = vector<int>(n,0);
        low = vector<int>(n,0);
        scc = vector<bool>(n,false);
        time = 0;
        sscnum = 0;
    }
    vector<vector<int>>   Sscs;     // 所有连通分量
    vector<vector<int>>  graph;     // 有向图的邻接矩阵
    int                      n;     // 顶点总数
    vector<int>  dfn;               // 时间戳数组
    vector<int>  low;               // 最小时间戳数组（能够追溯到的最早栈中节点时间戳）
    vector<bool> scc;               // 在栈内标记数组
    int         time,               // 时间
              sscnum;               // 连通分量数
    stack<int>           stk;       // 遍历栈
};



void Ssc::Tarjan(int root)
{
    if( dfn[root] ) return;                     // 访问过了，直接返回
    dfn[root] = low[root] = ++time;
    stk.push(root);                             // 入栈
    scc[root] = true;
    
    for(int v = 0;v < n;v++)                    // 遍历 root 所指节点
    {
        if(!dfn[v] && graph[root][v])           // v 还未被访问过
        {
            Tarjan(v);
            low[root] = min(low[root], low[v]);
        }
        else if(scc[v] && graph[root][v])       // 如果 v 还在栈内
        {
            low[root] = min(low[root], dfn[v]);
        }
    }

    if(low[root] == dfn[root])                  // 后代不能找到更浅的节点了
    {
        sscnum ++;                              // 记数
        vector<int> sc;                         // 保存当前连通分量
        while(true)                             // 依次退栈至 root
        {
            int x = stk.top();
            scc[x] = false;
            stk.pop();
            sc.push_back(x);
            if(x == root) break;
        }
        Sscs.push_back(sc);
    }
}

int main()
{
    vector<vector<int>> graph = {
        {0,1,1,0,0,0},
        {0,0,0,1,0,0},
        {0,0,0,1,1,0},
        {1,0,0,0,0,1},
        {0,0,0,0,0,1},
        {0,0,0,0,0,0},
    };
    Ssc S(6, graph);
    S.Tarjan(0);
    int index = 1;
    for(auto i : S.Sscs)
    {
        cout << "SSC (" << index++ << ") : "; 
        for(auto j : i)
        {
            cout << j << " ";
        }
        cout << endl;
    }
    cout << "The Number of SSC : " << S.sscnum << endl;
    return 0;
}
```


---
## 运行结果


<center>
![Result](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Tarjan/Tarjan.PNG#pic_center)
</center>