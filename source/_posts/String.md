---
title: 【数据结构】 字符串
date: 2019-03-11 18:46:04
tags: String
categories: 数据结构
toc: true
comments: true
thumbnail: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1548580675099&di=6efdd9be8a2394de553173ab69c0bb70&imgtype=0&src=http%3A%2F%2Fs1.knowsky.com%2F20170206%2Fp3rqnw1kmbl32.png'
---

#### 串的定义
<!-- more -->
```c++
// 通常用一个字符数组来表示
char str[] = "hello";
// 数组str内存储的字符为{'h','e','l','l','o','\0'} ,故有6个数组元素，其中'\0'是串的结束标志，告知编译器串结束了。
// 但是串str的长度为5，“hello”，
```
* 【注】以上定义方式一般不用，因为用该方式单纯以 '\0' 结尾的串如果要得到字符串的长度较为麻烦（需要遍历整个串，时间复杂度为O(n)，故一般情况下我们用自己定义的结构体来定义串，下面会谈到。

---

* 【注】空格也是串中的元素，由一个或多个空格组成的串称为空格串，空格串不是“空串”。

---

* 串的逻辑结构与线性表类似，串是限定了元素为字符的线性表。但从操作对象上来说，串与线性表有着很大的不同：线性表的主要操作对象是单个元素，而串的主要操作对象是该串的一个“**子串**”。

---
#### 串的存储结构
---
**1. 定长顺序存储表示：**
```C++
typedef struct Str{
  char str[maxsize+1]; // 用来存放字串的字符数组，maxsize 为字符串最大长度，maxsize+1为数组最大长度，+1 用于存储 '\0'.
  int length; // 字符串长度，可用Str.length方法直接访问 length <= maxsize;
}
```
**2. 动态分配存储表示：**
```c++
typedef struct LStr{
  char *ch; // 指向malloc();动态分配存储区的首地址的指针
  int length; // 字符串长度
}
```
---
#### 串的基本操作
---
**1. 赋值操作：**
```c++
int strassign(LStr& str,char* ch){ // 需返回的变量带引用符号&
  if (str.ch){
    free(str.ch); // 释放原有空间
  }
  int len = 0;
  char *c = ch;
  while(c){ // 计算ch的长度
    ++len;
    ++c;
  }
  if (len == 0 ){
    str.ch = NULL; // 如果ch为空，则直接返回一个空的串
    str.len = 0;
    return 1;
  }
  else {
    str.ch = (char*)malloc(sizeof(char)*(str.len+1)); // 用malloc函数分配一块连续的存储空间，str.len+1是为了容纳'\0'
    if (str.ch == NULL) {
      return 0; //分配失败
    }
    else {
      c = ch;
      for (int i = 0; i <= len;i++){ //遍历并赋值
        str.ch[i] = *c; // *c 表示c指针所指的位置的值
        ++c; // c指针指向下一个位置
      }
      str.len = len; // 被赋值的串长度等于ch的串长
    }
  }
  return 1; // successfully
}
```
**2. 取串长度操作：**
```c++
int StrLength(LStr str){
    // 有给串长度信息的情况：
    return str.len; // 返回str串的长度
    
    //在没有给出串长度信息的情况下：
    int len = 0;
    char = *c;
    c = str.ch;
    while(c){
      ++len;
      ++c;
    }
    return len;
}
```
1. **串的比较操作**：
```c++
int strCompare(LStr str1,LStr str2){
    //啰嗦版:
    for (int i = 0;i < str1.len && i < str2.len){
        if(str1.ch[i] - str2.ch[i] == 0) i++;
        else if(str1.ch[i] - str2.ch[i] > 0){
            cout << "str1 > str2" << endl;
        }
        else {
            cout << "str1 < str2" << endl;
        }
    }
    if (str1.len - str2.len > 0){
      cout << "str1 > str2" << endl;
    }
    else if (str1.len - str2.len < 0){
      cout << "str1 < str2" << endl;
    }
    else cout << "str1 = str2" << endl;
    return 1;
    // 简洁版：
    for (int i = 0; i < str1.len && i < str2.len ;i++){
        if (str1.ch[i] != str2.ch[i]){
            return str1.ch[i] - str2.ch[i];
        }
        return str1.len - str2.len;
    }
}
```
**4. 串的连接操作：**
```c++
int concat(LStr &str,LStr str1,LStr str2){  // 将两个字符串连接并用一个新的字符串str返回
    if(str.ch) { // 清除原有空间
      free(str.ch);
      str.ch = NULL;
      str.len = 0;
    }
    str.ch = (char*)malloc(sizeof(char)*(str1.len+str2.len+1)); // 分配连续空间，+1是为了多分配一个位置空间存放‘\0’
    int i = 0;
    while(i < str1.len){ // 插入str1;
      str.ch[i] = str1.ch[i];
      ++i;
    }
    int j = 0;
    while(j <= str2.len){ // 插入str2，注意这里用"<="是为了吧'\0' 也加到末尾
      str.ch[i+j] = str2.ch[j];
      ++j;
    }
    str.len = str1.len + str2.len; // 更新字符串长度
    return 1; // 成功连接
}
```
**5. 求子串操作：**
```c++
int subStr(LStr &substr,LStr str,int pos,int len){
    if (pos + len > str.len || pos < 0 || len < 0 || pos >= str.len){
        return 0;  //判断输入是否合法
    }
    if (substr.ch){ // 清空原空间
      free(substr.ch);
      substr.ch = NULL;
    }
    if (len == 0){ // 若子串长度为0.直接返回空子串
      substr.ch = NULL;
      substr.len = 0;
      return 1;
    }
    else{
    substr.ch = (char*)malloc(sizeof(char)*(len+1)); // 分配连续的内存空间
    
    int i = 0;
    int j = pos;
    while(i<len){ // 从pos处开始遍历并赋值给子串
        substr.ch[i] = str.ch[j];
        ++i;
        ++j;
    }
    substr.ch[i] = '\0'; // 这个千万别忘了加进去
    substr.len = len; // 更新子串长度
    return 1; // 成功
  }
}
```
6. 串的清空操作：
```c++
// 串的清空操作在上诉各函数中均有用到
int clearStr(LStr &str){
  if (str.ch){
      free(str.ch);
      str.ch = NULL;
  }
  str.len = 0;
  return 1;
}
```
---
#### 串的模式匹配算法(重点)
###### 何为模式匹配：
* 对一个串中某子串的定位操作称为串的模式匹配，其中待匹配的子串称为“模式串”。
###### 串的模式匹配算法分为：
1. 简单模式匹配算法
2. KMP算法

---
**1. 简单模式匹配算法：**
* _算法思想_：
* 从主串的第一个位置起开始遍历字符串，若该字符与模式串的第一个字符相同，则继逐一比较后续字符，   否则从主串的下一个位置开始，重复上一步操作，以此类推，直到比较完模式串的所有字符。若匹配成     功，返回模式串在主串中的位置。匹配失败 ......,随便你想咋样。
```C++
int subStr_Match(Lstr str,LStr substr){
    if (substr.ch == NULL || str.ch == NULL){
    return 0;
  }
  int i ,j , pos = 0;
  for (i = 0 , j = 0;i < str.len && i < substr.len; ){
    if (str.ch[i] == substr.ch[j]){
        ++j;
        ++i;
    }
    else {
      j = 0; // 匹配失败，j 重新指向模式串起始位置
      i = ++pos; // pos 记录上一次匹配的起始位置，在匹配失败后将i指向上一轮匹配的初始位置pos的后面一个位置++pos开始新一轮匹配
    }
  }
  if (j >= substr.len){
    return pos; // 匹配成功，返回模式串在主串中的位置
  }
  return 0;
}
```
---
2. ***KMP算法***：
* _算法思想解析_ :
* 上述的匹配算法称为“简单模式匹配算法（BF）”，其时间复杂度为O(mn),其中m为主串长度，n为模式串长度。由此可知简单模式匹配算法虽然易于理解但是效率很低，无法满足当已知数据异常庞大时的效率要求。所以就诞生了接下来登场的KMP算法。
* 我们知道，在BF算法中每次发生不匹配i与j都要回溯到该轮匹配的初始位置，并且在回溯之后的后几次匹配同样有可能导致（不必要的）不匹配状态，这是导致算法效率低下的主要原因，那么如何直接跳过这些不必要的不匹配状态而直接到达可能解决不匹配位置的的状态呢？
* 解决办法就是利用匹配失败后的信息，那么如何利用呢？
* 为了使问题变得更加直观，我们假想匹配过程就是模式串在主串上的移动(实际上并不会移动，全是指针在变化)，如果在某一次匹配时在模式串的第j位置发生了不匹配（j位置前的所有元素都已匹配成功），如果照着BF算法来做，我们会抛弃掉j位置前的匹配“成果”直接将i与j回溯重新开始下一轮比较。但现在我们不这么做，因为我们完全可以将j之前的匹配成果利用起来
* 不不妨假设模式串为“ABABABB”，并且该模式串在与主串的一次匹配流程中第4个元素B与主串发生了不匹配，很显然这个时候主串i位置前的三个元素跟模式串是完全匹配的，为了利用这个成果，就是在模式串向后移动后尽可能地保留这些匹配成果，我们观察这三个元素“ABA”的特点，发现他的前缀与后缀出现了相同的字符序列“A”，这时候我们应该意识到，要时上一次的成果得到最大限度的保留，我们只能将模式串移动到前缀与后缀重合的状态，这样子就保留了一个匹配成果“A“，同时i根本就不需要回溯（原地不动就好），因为i无需从模式串头部重新开始与其匹配，而只需从保留的成果后开始匹配也就是模式串的第二个位置（A的后一个位置）开始匹配。
* 但问题又来了，怎么知道模式串该怎么移动呢，从上面的分析我们发现，对于模式串移动的分析完全没有涉及到主串，那我们是怎么做到视主串而不见的呢(它可是”主“串啊给点面子好不好)。事实上，我们用到他了，因为我们的假设是”j位置前的元素与主串完全匹配“，竟然这样那么不就说明j位置前的模式串部分与主串的那一部分完全一样吗，所以我们可以用一个所谓”假模式串“来代替主串，而模式串只要在这个”傀儡身上移动就好了。所以，模式串在哪个位置与主串发生不匹配后模式串应该怎么移动，这个问题就可以脱离主串而背单独拿出来分析了，这就是后面要谈到的next数组（用与存放当j位置发生不匹配时，j指针应该重新调整到那个位置上）。有了next数组，我们就可以知道当模式串在J处与主串发生不匹配之后，为了最大限度地保留之前的匹配成果，模式串该怎么移动（指针该怎么变化）。

---
**KMP算法代码**：
```C++
int KMP (LStr str,LStr substr,int next[]){ // 函数接受主串，模式串，next数组
  
  int i = 1 ,j = 1; // i 扫描主串，j 扫描模式串
  for (i < str.len && i < substr.len){
    if (j == 0 || str.ch[i] == substr.ch[j]){  
// j=0;的情况就是模式串中的第一个字符与主串中的第i个字符不匹配，应从
// 主串的下一个位置与模式串的第一个位置继续比较，故++i(主串的下一个位置);
// ++j(模式串第一个位置0+1=1(很强))
        ++j;
        ++i;
    }
    else {
      j = next[j]; // j 被调整到合适位置，这里的i不需要回朔，这也是KMP算法的一大特点
    }
  }
  if (j >= substr.len){ // j 的长度超过了模式串，显然匹配成功
    return i - substr.len; // 匹配成功，返回模式串在主串中的位置
  }
  return 0;
}
```
---
**next数组的求法**:
* 经过前面的分析我们知道，只需要模式串本身我们就可以求出next数组，并不需要主串的参与。所以我们可以定义一个函数将next数组一次性求出，从此一劳永逸......
* 这里我们要用到一个算法思想，那就是**递推**,我们知道数列就是一种有着递推关系的数的序列。现在假设等差数列{An},给你一个递推公式(实际上就是前一个元素与后一个元素的关系)：A(n+1) = An + 1;其中n={1,2,3,...}然后告诉你第一个元素A1 = 0(实际上告诉你任何一个位置上的元素值都可以); 有了这两个已知条件你可以知道这个数列的所有元素就是非负整数集{0,1,2,3, ...}。
* 那我们如何在求解next数组上面应用这个思想呢？ 首先看看我们有什么已知条件？
* 显然我们需要知道两个相邻状态Sk与Sk+1之间的关系，假设模式串为p1～pm，问题转化为两个模式串之间的匹配问题。如果在Sk时，已经求得了next[j] = t；若要求得Sk+1状态的next[j+1]，我们需要分两种状态来考虑：
1. 若Pj = Pt；则next[j+1] = t+1;
2. 若Pj != pt;这时候就又回到了我们讨论模式串与主串匹配出现匹配失败的经典情形了，不匹配发生在t处，我们应该去查next数组看看t应该怎样调整位置了，显然next[t]我们已经求得了，所以令t = next[t],继续比较pj与pt，若不相等重复第二种情况，直到t = 0;或者pj = pt 满足第一种情况，从而求得next[j+i];

---

**next求数组代码**:
```c++
void getNext(LStr substr,int next[]){
    int j = 1;
    int t = 0;
    int next[1] = 0; // 特殊情况，模式串的第一个位置发生不匹配
    while(i < substr.len){
        if(t==0 || substr.ch[t] == substr.ch[j]){ // t=0;是因为next数组中可能有0元素,也说明没有重合的前后缀
            next[j+1] = t+1; 
            ++j;
            ++t;
        }
        else{
            t = next[t];
        }
    }
}
```
---
#### KMP 算法的改进
---
* KMP算法就还有什么地方需要改进的？
* 为了回答这个问题我们先来看一种特殊情况：模式串为（A A A A A B）,该模式串所对应的next数组为{0,1,2,3,4,5}。可以遇见的是当在模式串第j=5个位置A处发生不匹配时，next数组指导j指向4；而4处的元素依然不匹配（因为4处元素与5处相等），j来到了3（同样不匹配），紧接着来到了2（不匹配），来到1（依然不匹配），最后j=0(++i,++j)到此才结束了之前陷入的“尴尬”局面。
* 由上分析我们不难想到，如何才能让j直接跳到0；而免去从1-4的多余的比较呢？这就是KMP算法需要改进的地方
* 也就是说，对KMP算法的改进主要就是对求next数组的方法的改进，于是就有了改进版的next数组，我们称之为 **nextval 数组**

---
##### getNextval() 算法核心思想：
---
* 通过上面那个特殊情况，我们知道当j处发生不匹配时，若next数组指导的下一个位置的值与j处的值是相等的，那么显然这次比较就是多余的（因为显然还是会不匹配），所以我们应该跳过next数组所指向的那个位置，换一种思路就是我们应该让next[j] 所指向的位置与Pj不相等，就是改变next[j] 的值；改变后的next数组就是nextval数组.
* 求解nextval数组的一般步骤：
1. 当j等于1时，nextval[j]赋值为 0 ，作为特殊标记；
2. 当j大于1 时：
      若Pj不等于P(next[j]),则nextval[j] 等于 next[j];
      若Pj等于P(next[j]),则nextval[j] 等于 nextval[next[j]];
      
```c++
void getNextval(LStr substr,int nextval[]){
  int j = 1;
  int t = 0;
  nextval[1] = 0;
  while(i<substr.len){
      if (j == 0 || substr.sh[j] == substr.ch[t]){
          if(substr.ch[j+i] != substr.ch[t+1])
              nextval[j+1] = t+1;
          else
              nextval[j+1] = nextval[t+1];
              
              ++j;
              ++t;
      }
      else 
          t = nextval[t];
  }
}
```

---
