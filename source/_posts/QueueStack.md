---
title: 【数据结构】栈与队列
date: 2019-03-10 18:46:04
tags: List
categories: 数据结构
toc: true
comments: true
thumbnail: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1548581470072&di=ee7f02ae4ffa2ccc6257101f77c6b5d9&imgtype=0&src=http%3A%2F%2Fimg.mp.itc.cn%2Fupload%2F20170627%2Fa3e6109615584b62a5eb86fe79243270_th.jpg'
---


---
### 栈和队列的基本概念
---
<!-- more -->    
#### 栈的基本概念
1. *栈的定义*
* 只能在一端（栈顶Top）进行插入和删除操作的线性表
* 栈顶由一个称为栈顶指针的位置指示器top来指示，它是动态变化的
* 表的另一端栈底是固定不变的

1. *栈的特点*
* 先进先出（ＦＩＬＯ）
* 栈就如同一个狭窄的死胡同，最先进去的人（元素）只能够最后出来
3. *栈的存储结构*
* 可以用顺序表或者链表来存储栈：
    a) 顺序栈
    b) 链式栈
4. *栈的数学性质*
* 当ｎ个元素以某种顺序进栈，并且可以在任何时候出栈（在满足先进后出的前提下）时，所获得的元素排列的数目Ｎ恰好满足函数 Catalan() 的计算，即：
                                    $$
                                    N = { \dfrac{1} {n+1} }×C\binom{n} {2n}
                                    $$ 

      
---
#### 队列的基本概念
---
1. *队列的定义*
* 是一种操作受限的线性表，且只允许在表的一端进行插入，在另一端进行删除操作。
* 可以插入的一端称为队尾（ｒｅａｒ），可以删除的一端称为队头（ｆｒｏｎｔ）
* 插入元素称为进队，删除元素称为出队
2. *队列的特点*
* 先进先出（ＦＩＦＯ），就像食堂打饭要排队一样，先来的人先有饭吃
3. *队列的存储结构*
* 可用线性表或者链表来存储队列：
    a) 顺序队
    b) 链队
    
---
### 栈和队列的存储结构、算法与应用
---
1. **顺序栈的定义**
```c++
typedef struct SqStack {
  int data[Maxsize]; //一维数组用来存储数据
  int top;　// ｔｏｐ指针用来指向栈顶元素,规定top=-1　为栈空，top=Maxsize-1 为栈满
}
```
2. **链栈结点的定义**
```C++
typedef struct LNode {
  int data; // 数据域
  struct LNode *next;　// 指针域
}LNode;
```
3. **顺序队列的定义**
```c++
typedef struct SqQueue {
  int data[Maxsize]; //数组存放数据
  int front;　　// 队首指针
  int rear;　　// 队尾指针
}
```
4. **链队的定义**
  a) 链队结点定义：
```c++
typedef struct LQNode{
      int date; //数据域
      struct LQNode *next; //指针域
    }
```
   b) 链队类型定义：   
```c++
// 定义一个只包含两个指针域的结点来存放队头与队尾指针
    typedef struct LiQueue{
      struct LQNode *front; // 队首指针
      struct LQNode *rear;  //　队尾指针
    }　// 链队类型定义
```
### 顺序栈
---
##### 顺序栈的几个关键要素：
1. **三个状态**
  * 栈空状态：**st.top = -1**;
  * 栈满状态：**st.top = Maxsize - 1**;
  * 非法状态：栈满却继续入栈发生**上溢**；栈空继续出栈发生**下溢**；
2. **两个操作**
  * 元素进栈：++(st.top); st.data[st.top]=x;
  * 元素出栈：x=st.data[st.top]; --(st.top);
  
---
##### 初始化栈：
```c++
// 初始化一个栈，只需将栈顶指针置为－１即可
void initStack(){
  int top = -1;
}
```
##### 判断栈空代码：
```c++
int EmptyStack(SqStack ss){
  if (ss.top == -1)
      return 1; // 栈空返回１；
  
  else
      return 0;　// 栈非空返回０；
}
```
##### 进栈代码：
```c++
#defined Error 0
int push(SqStack &ss, int x){
  if (ss.top == -1) return Error; // 栈满时返回错误，无法入栈
  ss.top++;
  ss.data[ss.top] = x;
  // 也可一句话解决：　ss.data[++ss.top] = x;
  return 1;　//入栈成功返回１
}
```
##### 出栈代码：
```c++
int pop(SqStack &ss,int e){
  if (ss.top == -1) return Error; // 栈空不能出栈
  e = ss.data[ss.top];
  --ss.top;
  //　也可一句话解决：　e = ss.data[ss.top--];
  return 1;
}
```
【注】:
```c++
对于自增操作，入++a;总是比a++;的执行效率要高一些，因此在使用二者都可以的情况下优先选择++a;
```
---
### 链栈
---
###### 以下链栈都由带头结点的链表表示
---
##### 顺序栈的几个关键要素：
1. 两个状态
  * 栈空状态：lst --> next = NULL;
  * 栈满状态：不存在栈满状态，因为单链表的内存空间是动态分配的
2. 两个操作
  * 元素（由指针ｐ所指）的进栈操作：p -> next = lst -> next; lst -> next = p;//其实     就是头插法建立单链表的操作
  * 出栈操作：s = lst -> next; x = s -> data; lst -> next = s -> next;           free(s); //其实就是单链表的删除操作
  
---
#### 链栈的初始化代码：
```c++
// 实际上，链栈的初始化与单链表的初始化并无不同
void initLStack(LNode *&lst){
  lst = (LNode*)malloc(sizeof(LNode)); //制造一个头结点
  lst -> next = NULL;　// 将链栈滞空
}
```
#### 判断栈空代码：
```c++
int isEmpty(LNode lst){
  if (lst -> next == NULL) 
      return 1; //栈空返回１；
  else
      return 0;　// 栈不空返回０；
}
```
#### 进栈代码：
```c++
int push(LNode &lst,int x){
  LNode s = (LNode*)malloc(sizeof(LNode));
  s -> data = x;
  s -> next = lst -> next;
  lst -> next = s;
  return 1;
}
```
#### 出栈代码：
```c++
int pop(LNode &lst, int &e){ // 用e返回出栈元素的值
  if (lst -> next == NULL) return 0;
  e = lst -> next -> data;
  LNode *s = lst -> next;
  lst -> next = s -> next;
  free(s);
  return 1;
}
```
---
### 栈的应用
---

###### 栈的主要应用有：
1. 括号匹配
2. 表达式求值
3. 逆波兰转换算法

---
#### 括号匹配
---
##### 算法思想：
  * 扫描整个表达式，判断当前符号是否为括号
  * 如果不是，继续扫描下一个字符
  * 如果是，判断是左括号还是右括号，是左括号将其入栈，是右括号就判断栈是否为空
  * 若栈为空，说明此表达式的右括号多与左夸号
  * 若栈不空则判断当前操作符是否和栈顶操作符匹配，若不匹配说明左右括号不匹配，若匹配则继续判断     下一个操作符。最后，判断栈是否为空，若不空则说明左括号多余右括     号，栈为空说明匹配成功。
  
---
```c++
initStack(Stack stack){
  for (int i ;i<strlen(str);i++){
    if (str[i]=='{' || str[i]=='[' || str[i]=='('){
      push(stack,str[i]);
    }
    else {
      if (str[i]=='{' && getTopStack(stack) == '}')
          pop(stack);
      if (str[i]=='[' && getToPStack(stack) == ']')
          pop(stack);
      if (str[i]=='(' && getTopStack(stack) == ')')
          pop(stack);
    } 
      
  }
  // 最后，若栈空则匹配成功，否则失败
  if(isEmpty() == true){
      cout << "括号匹配成功　！！！"　<< endl;
  }
  else cout << "匹配失败　！！！" << endl;
}
```
---
#### 表达式求值
---
##### 算法思想：
  * 扫描表达式，当扫描到数时将其推入栈中，当扫描到一个运算符时，将该运算符作用于位于栈顶的两个数上，并将所得结果推入栈中
  * 以下将给出后缀表达式的求值程序
  
---
```c++
int calcExp(char* exp , Stack s){
  int i = 0;
  while (exp[i] != '\0'){ //
      if (exp[i]>='0' && exp[i]<='9'){
        s.push(s , exp[i]-'0'); //　若为数字，推入栈中
      }
      else if(exp[i] == '运算符'){
          int m = s.gettop(); //　取栈顶元素后将其出栈
          s.pop();
          int n = s.gettop(); //　取栈顶元素后将其出栈
          s.pop;
          s.push(s, n[运算符]m); //　将运算结果推入栈中
      } 
      i++; // 继续遍历
  }
      return s.top;
}
```
---
#### 逆波兰转换算法
---
##### 算法思想：
  * 设立一个栈，存放运算符，初始栈为空，编译程序从左往右扫描中缀表达式，若遇到数字，直接输出，并输出一个空格为两个操作数之间的分隔符；
  * 若遇到运算符，则与栈顶比较，若运算符级别比栈顶级别高则进栈，否则退出栈顶元素并输出，之后输出一个空额作分隔符
  * 所遇到左括号，紧张；
  * 若遇到右括号，则一直退栈粗出知道退出第一个左括号为止
  * 当栈为空时，输出的结果即为**后缀表达式**
  
---
```c++
void tranfExp (char* exp , Stack s){
    while (exp[i] != '\0'){
        if (exp[i] >= '0' && exp[i] <= '9'){
            //　若为数字，直接输出
        }
        else if (exp[i] == '('){
            //　若为左括号，进栈
        }
        else if (exp[i] == ')'){
            //　若为右括号，出栈直至第一个左括号
        }
        else if (exp[i] == '运算符'){
            //　判断与栈顶元素的优先级大小
            if (exp[i] > s.gettop())
                s.push(exp[i]);  // 优先级大于栈顶运算符，将该运算符进栈
            else  //　优先级小于栈顶运算符，退出栈顶元素并且输出
    while (s.isEmpty() == false)
        pop();//　把栈中剩余元素全部退出并输出
        }
    }
}
```
---

---
### 顺序队
---
#### 循环队列
---
##### 循环队列的基本要素
1. 两个状态：
  * 队空状态：qu.rear = qu.front;
  * 队满状态：(qu.rear+1)%front == qu.front ;
2. 两个操作：
  * 元素x进队操作：qu.rear = (qu.rear+1)%MaxSize; qu.data[qu.rear] = x;
  * 出队操作：qu.front = (qu.front+1)%MaxSize; elem = qu.data[qu.front];//elem 保     存出队的元素
 
---
#### 循环队列的基本操作实现
1. 初始化队列算法：
```c++
void initQueue(Queue &qu){
  qu.front = 0; 
  qu.rear = 0; 
}
```
2. 判断队空算法：
```c++
int isQEmpty(Queue qu){
  if (qu.front == qu.rear){
      return 1; //
  }
  return 0; //
}
```
3. 进队算法：
```c++
int enterQueue(Queue &qu , int x){
  if ((qu.rear+1)%MaxSize == front){
      cout << "队列已满" << endl;
      return 0;
  }
  qu.rear = (qu.rear+1)%MaxSize;
  qu.data[qu.rear] = x;
  return 1;
}
```
4. 出队算法：
```c++
int outQueue(Queue &qu , int e){
  if (qu.rear == qu.front){
      cout << "队空无法出队" << endl;
      return 0;
  }
  qu.front = (qu.front+1)%MaxSize;
  e = qu.data[qu.front];
  return 1;
}
```
---

---
### 链队
###### 采用链式存储方式来实现队列，特点是假设内存无限大的情况下不存在队满上限
---
##### 链队的基本要素
1. 两个状态：
  * 队满状态： 不存在队满状态
  * 队空状态：que.rear = NULL || que.front = NULL (两个满足一个即可)
2. 两个操作：
  * 元素q进队操作：　分两种情况
              1. 当前队为空：que --> rear = que --> front = q;
              2. 当前队不空：que --> rear --> next = p;que --> rear = p;
  * 元素出队操作： s = que --> front;  que --> front = s --> next;elem = s -->                      data; free(s);

---
#### 链队的基本操作实现
1.初始化链队算法：
```c++
void initLiQueue(LiQueue *&que){
    que = (LiQueue*)malloc(sizeof(LiQueue));
    que -> rear = NULL;
    que -> front = NULL; 
}
```
2.判断队空算法：
```C++
int isEmpty(LiQueue que){
    if (que.rear = NULL || que.front = NULL){
        cout << "队列为空"　<< endl;
        return 1;
    }
    return 0;
}
```
3.入队算法：
```c++
int enterLiQueue(LiQueue &que ， int x){
    LQNode* s = (LQNode*)malloc(sizeof(LQNode));
    if (isEmpty(que)){  // 若队列为空，进队操作比较特别
        que -> front = que -> rear = s;
        return 1;
    }
    else{
        que -> rear -> next = s;
        que -> rear = s;
        return 1;
    } 
        return 0;
}
```
4.出队算法：
```c++
int outLiQueue(LiQueue &que , int &elem){
    LQNode* s = que -> front;
    if (isEmpty()){
        cout << "队为空，无法出队" << endl;
        return 0;
    }
    if (que -> front == que -> rear){ // 若队列只有一个元素，出队操作比较特别
        que -> front = NULL;
        que -> rear = NULL;
    }
    que -> front = s -> next;
    elem = s -> data;
    free(s);
    return 1;
}
```

---
