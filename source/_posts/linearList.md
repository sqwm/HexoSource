---
title: 【数据结构】线性表
tags: List
categories: 数据结构
toc: true
comments: true
thumbnail: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1548580411500&di=d3bc8a8fb160d662bf3ef1d14ff4ae37&imgtype=0&src=http%3A%2F%2Fs2.cdn.deahu.com%2Fshow%2Flfile%2F7E73DBAD83122DAF20DFDD33CF1E9C8D.jpg'
---

---
### 线性表的基本概念与实现
<!-- more -->
1.　**线性表的定义:**
    线性表是具有相同特性数据元素的一个有限序列，重点在“__有限序列__”。线性表可以是有序的，也可以是无序的。
2.　**线性表的逻辑特性:**
    除了表头和表尾的数据元素“结点”，所有元素都有一个*直接前驱*与一个*直接后继*。表头无前驱，表尾无后继。
1.  **线性表的存储结构：**



    * 顺序存储结构：（顺序表）
        1. 存储空间连续（空间为*一次性*分配的）
        2. 可以随机存取，也可以顺序存取
        3. 插入删除时平均需要移动近一半的元素，时间复杂度为:__O((n-1)/2)=O(n)__
        4. 存储密度为１
    * 链式存储结构：（链表）
        1. 存储空间可以不连续（存储空间是*动态*分配的）
        2. 每一个结点不仅包含数据还包含指向下一个结点的指针
        3. 只能够进行顺序存储
        4. 存储密度<1
        5. 插入删除时不需要移动元素，只需修改*指针*即可,时间复杂度为:__O(1)__
1.  **线性表的定义与实现：**
    a) *顺序表的定义：*

*结构体定义：*   
```C++
#defined MaxSize 100
typedef sturct Sqlist {
    int data[MaxSize]; //线性表最多能容纳的元素个数，即分配的空间大小
    int length ;　//元素的个数
}Sqlist;
```
*用的最多的简单定义：*
```c++
int A[MaxSize]; //直接利用数组就是顺序表的一种这一特性
int length;
```
---
 　  *b) 单链表的结点定义：*
```c++
typedef struct LNode {
  int data; //数据域
  struct LNode *next;　//指针域
}LNode;
```
---
  *c) 双链表结点定义：*
    
```C++
  typedef struct DLNOde {
    int data; //数据域
    struct DLNOde *prior;　// 指向前驱结点的指针
    struct DLNode *next;　//　指向后继结点的指针
  }
```
---
【注】　为结点分配存储空间：
```c++
  LNode *A = (LNOde*)malloc(sizeof(LNode));
  //malloc 函数返回一个空间的地址，让指针Ａ来指向它
```
### 线性表的相关操作
---

* 查找操作：
```c++
int findElem (Sqlist a, int x){
  for (int i = 0;i<l.length;++i){
    if (a[i]==x){
      return i; //找到了，返回所在的下标
    }
  }
  return 0;　//　没找到，返回０
}
```
* 插入操作：
```c++
int  insertElem(Sqlist &L,int i ,int x){
  if (i<0 || i > L.length){
      return -1; //如果插入位置不合法，返回－１
  }
  if (L.length == MaxSize){
      int newL[L.length+MaxSize]
      for (int j=0;j<L.length;++j){
          newL[j] = L[j]; //如果发现顺序表已经满了，就构造一个更大的顺序表并把原顺序表的元素放进去
      }
  L = newL;
  }
  for (int k = L.length-1; k>=i; --k){
      L[k+1] = L[k];　//从某位开始将插入位置至末尾的元素向后移动一个位置
  }
  L[i] = x;　// 插入ｘ到ｉ处
  L.length++; // 插入后该表表的长度
}
```
* 删除操作：
```c++
//　通过索引下标删除元素，并返回所删元素的值
int deleteElem_by_index (Sqlist &L,int i){
    int q = L[i];　// 保留ｉ位置的元素
    for (int j = i+1;j<L.length;++j){
        L[j-1] = L[j]; //　从待删除元素的右边开始每个元素向左移动一个位置，覆盖掉ｉ位置的元素
    }
    L.length--; //　顺序表长度减一，完成删除操作
    return q; //　返回被删除元素的值

}
// 通过值来删除元素，并返回所删元素的下标
int deleteElem_by_value (Sqlist &L, int e){
    int index = findElem(L,e); //利用findELem() 函数找到要删除元素的下标
    int value = L[index]; 
    deliteElem_by_index (L,index);　// 用下标索引法删除元素
    return value;
}
```
* 初始化顺序表：
```c++
void initList (Sqlist &L){
    L.length = 0;
}
```
* 求指定位置元素：
```c++
int getElem (Sqlist L , int index){
    if (index < 0 || index > L.length-1) return Error;
    rerurn L[index];
}
```
### 单链表的相关操作
---
###### 以下所有的算法用的都是带头结点的单链表
---
* 尾插法建立单链表：
```c++
// 给定数组ａ[] 为数据源，建立单链表
void creatListR(LNode *&C , int a[], int length){
    LNode *s,*r; //用ｓ指向新建的结点，ｒ始终指向链表的尾部结点
    C = (LNode*)malloc(sizeof(LNode));　// 建立链表头结点
    C -> next = NULL;　//　将链表滞空
    r = C;　// r 指向头结点，也就是空链表的头结点
    for (int i = 0 ; i<length ; ++i){
        s = (LNode*)malloc(sizeof(LNode));　//　用malloc函数循环分配结点空间
        s -> next = NULL;
        s -> data = a[i];
        //　尾插法的核心算法：
        r -> next = s;
        
        r = r -> next; //r 指向当前尾结点
    }
    // r -> next ==　NULL;
}
```
* 头插法建立单链表：
```c++
void creatListH(LNode *&C ,int a[] ,int length){
    LNode *s;
    C = (LNode*)malloc(sizeof(LNode));　// 建立链表头结点
    C -> next = NULL;　//　将链表滞空
    for (int i = 0 ; i < length ; ++i){
        s = (LNode*)malloc(sizeof(LNode));
        s -> data = a[i];
        // 头插法的核心算法：
        s -> next = C --> next;
        C -> next = s;
    }
}

```
* 删除结点：
```c++
// 按值索引删除链表结点
void deleteNode(LNode &L , int elem){
    LNode *p,*q;
    p = L;
    if (L -> next == NULL) return 0; //如果链表为空，返回０；
    while (p -> next != NULL){　// 循环遍历链表结点
        if (p -> next -> data == elem){　// 如果ｐ指向的结点的下一个结点的数据域与带删除数据相等，删除该下一个结点，释放空间
           // 删除操作的核心算法：
            q = p -> next;
            p -> next = p -> next -> next;
          　
            free(q);　// 释放内存
            break;　//删除成功，退出循环
        }
        p = p -> next;　//该节点不是待删除结点，令ｐ指向下一个结点
    }
}
```
* 插入结点：
```c++
// 在链表的指定元素前插入结点
void insertNode(LNode &L , int we,int e){
    LNode *r;
    r = L;
    LNode *s = (LNode*)malloc(sizeof(LNode));
    q -> data = we;
    q -> next = NULL;
    while (r -> next != NULL ){
        if (r -> next -> data == e){
        //插入操作的核心算法：
            s -> next = r -> next;
            r -> next = s;
        }
        r = r -> next;
    }
}
```
### 双链表的相关操作
---
* 尾插法建立双链表：
```c++
//　给定数据源数组，建立双链表
void creatDListR (DLNode ＆L , int a[], int length){
    DLNode *s,*r; //用ｒ始终指向链表末尾结点，ｓ接受新分配的结点
    L = (DLNode*)malloc(sizeof(DLNode));　// 申请头结点空间，并将链表滞空
    L -> prior = NULL;
    L -> next = NULL;
    r = L;　//r 指向头结点
    for (int i = 0; i< length;++i){
        s = (DLNode*)malloc(sizeof(DLNode));
        s -> data = a[i];
        // 尾插发的关键步骤：
        s -> prior = r;
        r -> next = s;
        r = r -> next; // r = s;　令ｒ　指向下一个结点
        r -> next = NULL;　//滞空末尾结点的ｎｅｘｔ指针域
    }
}
```
* 头插法建立双链表：
```c++
void creatDListH (DLNode ＆L , int a[], int length){
    DLNode *s ;
    L = (DLNode*)malloc(sizeof(DLNode));　// 申请头结点空间，并将链表滞空
    L -> prior = NULL;
    L -> next = NULL;
    for (int i = 0 ; i<length; ++i){
        s = (DLNode*)malloc(sizeof(DLNode));
        s -> data = a[i];
        //关键步骤：
        s -> next = L -> next;
        L -> next -> prior = s;
        s -> prior = L;
        L -> next = s;
    }
}
```
* 查找结点的算法：
```c++
// 在双链表中查找第一个值为ｘ的结点，从第一个结点开始，边扫描边比较，若找到返回该结点的指针，没找到返回　ＮＵＬＬ
DLNode* findNode(DLNode *L, int x){
    DLNode *p;
    p = L -> next;
    while (p != NULL){
        if (p -> data == x){
            return p;
        }
        p = p -> next;
    }
    return NULL;
}
```
* 插入结点的算法：
```c++
//在双链表中ｐ所指结点后插入新的结点ｓ
//关键步骤如下：
              s -> next = p -> next;
              s -> prior = p;
              p -> next -> prior = s;
              p -> next = s;
```
* 删除结点：
```c++
//在双链表中的删除指针ｐ所指结点的后继结点,并用ｓ指针返回被删除的结点
//关键步骤如下：
              s = p -> next ;
              s -> next -> prior = p;
              p -> next = s -> next;
              free(s);
```
---
