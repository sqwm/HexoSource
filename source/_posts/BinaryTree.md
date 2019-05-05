---
title: 【数据结构】树
tags: Tree
categories: 数据结构
toc: true
comments: true
thumbnail: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRBLDbFr6CW_eRLtMdxvN1k9RSobzPNrCVdZsQQUEx8ZBqb5p2Q'
---

#### 树的基本概念
<!-- more -->
---
**树的定义：**
前面所提到的线性结构的元素是一种一对一的关系，而树是一种一对多的非线性结构，下面将通过一个具体的树的例子讲解到底什么样的结构才是树以 及树的一些相关术语：

![](https://i.loli.net/2019/01/28/5c4e5b7679982.png)

上图就是个树结构的概图了，我们可以看到它是由唯一的一个根节点和若干棵互不相交的子树组成的，由此可知树的定义是地柜的，即在树的定义中又用到了树的定义。这里需要注意的是，树的结点数可以是零，若为零时，称为一棵**空树**。
**结点：**上图中的每一个橙色圆圈都是结点，结点中不仅有数据域，还存在几个或零个指向其子树的指针；
**结点的度：**该节点所引申出的分支数目，如上图中的B结点，向下引申出了E和F，故其度为2；
**树的度：**树的度为树中所有结点的度的最大值，如上图树的度为A结点的度为3；
**叶子结点：**又称为*终端结点*，指的是度为零的结点
**非终端结点：**又称为分支结点，指的是度不为零的结点，上图中的ABCDEG都是非终端结点。另外，非终端结点除去根节点A之外的所有结点又称为*内部结点*。
**祖先：**从树的根节点到某一节点的路径上的所有结点都成为该结点的祖先结点，如E的祖先节点为：
A和B，因为路径为：A--B--E；
**层次：**根处为第一层，以此类推......，如上图树的层次为4层；
**结点的深度和高度：**联系实际，只需记住，高度是从底往上数；而深度是从上往下数；比如结点B的高度为3；而深度为2。根节点A的高度为树的高度为4；
**有序树：**树中结点的子树从左到右都是有次序的不能交换
**无序树：**树中结点的子树没有次序，可以任意交换
**丰满树：**理想的平衡树，要求除了最底层外，其他层都是满的
**森林：**若干棵互不相交的树的集合，若吧上图中的根节点A去掉，就成了一个森林

---
#### 树的存储结构
* 顺序存储：
双亲存储结构，亦称双亲表示法(克鲁斯卡尔算法)
* 链式存储：
孩子存储结构（孩子表示法）
孩子兄弟存储结构（孩子兄弟表示法）

---
#### 二叉树
* 二叉树的五种基本形式
* 满二叉树的概念
* 完全二叉树的概念
#### 二叉树的几个重要性质
* **性质一：**非空二叉树上叶子结点的数量等于双分支结点数加 1，即为$ n_0 = n_2 + 1$；
* **性质二：**二叉树的第$i$层上最多有$2^{i-1}$;
* **性质三：**高度（或深度）为$k$的二叉树最多有$2^k-1$个结点，换句话说就是一个深度为k的满二叉树的结点为$2^k-1$.
* **性质四：**该性质与二叉树的顺序存储结构相关，在下面会提到，这里不再赘述；
* **性质五：**函数$Catalan( ):$给定$n$个结点，能构成$h(n)$种不同的二叉树，其中：$h(n)=\frac{1}{n+1}×C_{2n}^n$ ;
* **性质六：**具有$n$个结点的完全二叉树的高度（或深度）为$[\log_2{n}]+1$(向下取整)；

#### 二叉树的存储结构
* **顺序存储结构：**
用一个数组来存储*完全二叉树*，将完全二叉树的结点值按编号依次存入一个一维数组中。
![](https://i.loli.net/2019/01/28/5c4e5b768378b.png)

如果要从一维数组中还原二叉树的本来结构，按照以下规则：
$i$ 为某结点的编号，若$i\not=1$，则该结点的双亲结点的编号为$i/2$向下取整；
如果$2i\leq n$,则该结点的左孩子编号为$2i$,否则该结点没有左孩子；
如果$2i+1 \leq n$,则该结点的右孩子编号为$2i+1$;否则该结点无右孩子；
下面给出将数组还原成二叉链树的代码：
```c++
void creatBTree(int BT[],int n,BTNode *&e){
  BTNode *BTNode_array[maxsize];
  for(int i = 1;i <= n;++i ){
    BTNode_array[i] = (BTNode*)malloc(sizeof(BTNode));
    BTNode_array[i] -> data = BT[i];
    BTNode_array[i] -> lchild = NULL;
    BTNode_array[i] -> rchild = NULL;
  }
  for (int i = 1;i <= n;++i){
    if(2*i <= n ){
      BTNode_array[i] -> lchild = BTNode_array[2*i];
    }
    if((2*i+1) <= n){
      BTNode_array[i] -> rchild = BTNode_array[2*i+1];
    }
  }
  e = BTNode_array[1];
}
```
* **链式存储结构：**
为了能够存储任意形式的二叉树结构，且根据二叉树一对多的非线性关系，设计出了二叉树的链式存储结构，结点定义如下：
```c++
typedef struct BTNode{
	int data; //数据域
	struct BTNode *lchild;//指向左孩子的指针
	struct BTNode *rchild;//指向右孩子的指针
};
```
#### 二叉树的遍历算法(递归实现)：
**深度优先遍历：**
* 前序遍历：
```c++
void preorder(BTNode *p){
	if(p != NULL){
		Visit(p);
		preorder(p -> lchild);
		preorder(p -> rchild);
	}
}
```
* 中序遍历：
```c++
void inorder(BTNode *p){
	if(p != NULL){
		inorder(p -> lchild);
		Visit(p);
		inorder(p -> rchild);
	}
}
```
* 后序遍历：
```c++
void postorder(BTNode *p){
	if(p != NULL){
		postorder(p -> lchild);
		postorder(p -> rchild);
		Visit(p);
	}
}
```
**广度优先遍历：**

* 算法流程图解：
![](https://i.loli.net/2019/01/28/5c4e5b76a92a2.png)
```c++
void level (BTNode *p){
	if(p != NULL){
		BTNode *que[maxsize];
		int front = 0;
		int rear = 0;
		BTNode *q;
		rear = (rear + 1)%maxsize;
		que[rear] = p;
		while(front != rear){
			front = (front + 1)%maxsize;
			q = que[front];
			Visit(q);
			if(q -> lchild != NULL){
				rear = (rear + 1)%maxsize;
				que[rear] = q -> lchild;
			}
			if(q -> rchild != NULL){
				rear = (rear + 1)%maxsize;
				que[rear] = q -> rchild;
			}
		}
	}
}
```

---

#### 二叉树的遍历算法(非递归实现)
![](https://i.loli.net/2019/01/28/5c4e5b768378b.png)
###### 上图而查处将作为例子方便讲解下面的算法

---
**深度优先遍历算法：**
* 先序遍历：
![](https://i.loli.net/2019/01/28/5c4e5b76b04b4.png)
```c++
void preorderNonrecursion(BTNode *bt){
	if(bt != NULL){
	BTNode *Stack[maxsize];
	int top = -1;
	BTNode *p;
	Stack[++top] = bt;
	while(top != NULL){
	    p = Stack[top--];
	    Visit(p);
	    if(p -> rchild != NULL){
	        Stack[++top] = p -> rchild;
	    }
	    if(p -> lchild != NULL){
	        Stack[++top] = p -> lchild;
	    }
	}
	}
}
```

* 后序遍历：
先序遍历算法遍历例子二叉树将得到：A B D E C F G
后序遍历例子二叉树：D E B F G C A
将后序遍历序列逆置：A C G F B E D
可以发现，如果将先序遍历序列中对左右子树的遍历顺序交换一下，就可以得到逆后序遍历序列，再将逆后序序列逆置即可得到后序遍历序列。
![](https://i.loli.net/2019/01/28/5c4e5b7746fce.png)
```c++
void postorderNonrecursion(BTNode *bt){
	if(bt != NULL){
		BTNode Stack1[maxsize];
		BTNode Stack2[maxsize];
		int top1 = -1;
		int top2 = -1;
		BTNode *p = NULL;
		Stack1[++top1] = bt;
		while(top1 != -1){
			p = Stack1[top--];
			Stack2[++top] = p;
			if(p -> lchild != NULL){
				Stack1[++top] = p -> lchild;
			}
			if(p -> rchild != NULL){
				Stack1[++top] = p -> rchild;
			}
		}
		while(top2 != -1){
			p = Stack2[top--];
			Visit(p);
		}
	}
}
```
* 中序遍历：
![](https://i.loli.net/2019/01/28/5c4e5b775c25b.png)
```c++
void inorderNonrecursion(BTNode *bt){
	if(bt != NULL){
		BTNode *Stack[maxsize];
		int top = -1;
		BTNode *p;
		p = bt;
		while(top != -1 || p != NULL){
			while(p -> lchild != NULL){
				Stack[++top] = p;
				p = p -> lchild;
			}
			if(top != -1){
				p = Stack[top--];
				Visit(p);
				p = p -> rchild;
			}
		}
	}
}
```
#### 线索二叉树
---
对于二叉链表存储结构，$n$个结点的二叉树有$n+1$个空链域，能不能把这些空链域有效地利用起来，使二叉树的遍历更加高效呢？答案是肯定的，这就是线索二叉树的由来。
* 线索二叉树的优势：二叉树被线索化后近似于一个线性结构，分支结构的遍历操作就被转化成了近似线性结构的遍历操作，通过线索的辅助使得寻找当前结点的前驱或者后继的效率大大提高。
**线索二叉树的构造：**
![](https://i.loli.net/2019/01/28/5c4e5b7758a61.png)
**结点定义：**
```c++
typedef struct TBTNode{
	int data; // 数据域
	struct TBTNode *lchild; // 左孩子（前驱结点）指针
	struct TBTNode *rchild; // 右孩子（后继结点）指针
	int ltag , rtag; //线索标记
};
```
* 根据二叉树的遍历方式的不同，线索二叉树可以分为先序线索二叉树、中序线索二叉树和后序线索二叉树。对一棵二叉树中的所有结点的空指针按照某种遍历方式加上线索的过程叫做二叉树的线索化，被线索化的二叉树就称为线索二叉树。
**通过中序遍历对二叉树线索化代码：**
```c++
void InThread(TBTNode *p,TBTNode *&pre){
	if(p != NULL){
		InThread(p -> lchild,pre); // 递归地线索化左子树
		if(p -> lchild == NULL){ // 建立当前结点前驱线索
			p -> lchild = pre;
			p -> ltag = 1;
		}
		if(pre != NULL && pre -> rchild == NULL){ // 建立前驱结点的后继线索
			pre -> rchild = p;
			pre -> rtag = 1;
		}
		pre = p; // pre 跟上 p，之后p会指向下一个结点
		InThread(p -> rchild,pre); // 递归地线索化右子树
	}
}
```
**通过中序遍历线索二叉树的主程序如下：**
```c++
void creatTBTNode(TBTNode *root){
	TBTNode *pre = NULL;
	if(root != NULL){
		InThread(root,pre); //递归建立线索二叉树
		pre -> rchild = NULL; // 处理最后一个结点
		pre -> rtag = 1;
	}
}
```
**遍历中序线索二叉树：**
*寻找中序线索二叉树 root 的第一个遍历结点：*
```c++
TBTNode *First(TBTNode *root){
	while( root -> ltag == 0){
		root = root -> lchild;
	}
	return root;
}
```
*在中序线索二叉树中，求结点p在中序下的后继结点的算法：*
```c++
TBTNode *Next(TBTNode *p){
	if(p -> rtag == 0){
		return First(p -> rchild);
	}
	else
		return p -> rchild;  // rtag = 1; 直接返回后继线索
}
```
*在中序线索二叉树上执行中序遍历：*
```c++
void Inoreder(TBTNode *root){
	for (TBTNode *p = First(root);p != NULL;p = Next(p)){
		Visit(p);
	}
}
```
**通过前序遍历对二叉树线索化**
```c++
void preInThread(TBTNode *p,TBTNode *&pre){
	if (p != NULL){
		if(p -> lchild != NULL){
			p -> lchild = pre;
			p -> ltag = 1;
		}
		if (pre != NULL && pre -> rchild == NULL){
			pre -> rchild = p;
			pre -> rtag = 1;
		}
		pre = p;
		if (p -> ltag == 0){
			preThread(p -> lchild,pre);
		}
		if (p -> rtag == 0){
			preThread(p -> rchild,pre);
		}
	}
}
```
**遍历前序线索二叉树算法：**
```c++
void preorder(TBTNode *root){
	if(root != NULL){
		TBTNode *p = root;
		while(p != NULL){
			while(p -> ltag == 0){
				Visit(p);
				p = p -> lchild;
			}
			Visit(p);
			p = p -> rchild;
		}
	}
}
```
#### 树与森林的互相转换
---

---
#### 树与二叉树的应用
---
##### 二叉排序树与二叉平衡树
---
##### 赫夫曼树与赫夫曼编码
---
**赫夫曼树的相关概念及介绍：**
赫夫曼树又被称为最优二叉树，它的特点是**带权路径最短**。下面介绍几个相关概念：
* **路径：**指从树中一个结点到另一个结点的分支所构成的路线
* **路径长度：**路径上的分支数目
* **树的路径长度：**从根到**每个结点**的路径长度之和
* **带权路径长度：**结点具有**权值**，从该结点到**根结点**的路径长度乘于该结点的权值就是该结点的带权路径长度
* **树的带权路径长度（WPL）：**树中所有**叶子结点**的带权路径长度之和

**赫夫曼树的构造方法：**
给定$n$个权值，用这些个权值来构造赫夫曼树：
首先了解一下赫夫曼树的一些特点：
* 权值越大的结点距离根节点越近
* 树中没有度为1的结点
* 树的带权路径长度最短

根据上述特点反推我们是如何来构造一个赫夫曼树：
* 从最底层开始构造
* 最底层结点离根节点月远故其路径长度最大，而为使其带权路径长度最短，应选择权值最小的结点作为最底层结点
* 权值最大的结点离根节点最近

有了上述导论我们就可以开始构造一棵赫夫曼树了：
![](https://i.loli.net/2019/01/28/5c4e5b7780558.png)
上图构建的赫夫曼树的WPL为：$8×1+7×2+5×3+4×4+2×4=61$,这是这些结点所能构造的所有不同的树中树的带权路径长度最小的构造方式。

##### 赫夫曼编码：
---
###### * 利用赫夫曼树的特点来对文件进行压缩存储

---
看个例子：如果有这样一串字符将要被存储于计算机中$AECCBCDEEDECCCBAEEEBECDDBB$
选三位长度的二进制数为A到E编码：
![](https://i.loli.net/2019/01/28/5c4e5b7755d25.png)
根据上表我们可以将该字符串编码为：
$000100010010001010011100100011100010010010001000100100100001000100100100001100010011011001001$
解码时每三位一个字符解码
总共需要78位来存储这个字符串，是否有根节省空间的编码形式呢？

答案是肯定的，我们统计一下这个字符串中各个字符出现的频率（权值）：
![](https://i.loli.net/2019/01/28/5c4e5bf2c8c41.png)
利用上表的信息构建一棵霍夫曼树，并将树中每个结点的左右分支进行编号（左0右1）：
![](https://i.loli.net/2019/01/28/5c4e5bf2d25e8.png)
到此我们得到了对A到E的霍夫曼编码规则：
![](https://i.loli.net/2019/01/28/5c4e5bf2c9721.png)
根据上表的编码规则可将字符串编码为：
$1110010101101011110011110101010110111000011001011111111110110$
只需61位的空间就能存储该字符串，可以直观地发现比普通编码短了很多。

**解码霍夫曼编码：**
解码霍夫曼编码需要用到上诉的那棵霍夫曼树，从左至右依次读取字符串编码，从根结点开始，读取到1则向右分支走，读取到0则向左分支走，直到走到叶子结点并读取该结点。

---
* [注] *对于同一组结点，构造出的霍夫曼树是不唯一的。但是，得到的不同的霍夫曼树的WPL却是相同的*

##### 霍夫曼$n$叉树
* *霍夫曼树不都是二叉树，霍夫曼二叉树只是霍夫曼$n$叉树的一种特例*

---
构造霍夫曼$n$叉树的逻辑与构造霍夫曼二叉树并无二异，我们知道对于结点数目大于等于2的待处理序列都可以构造霍夫曼二叉树。但却不一定能用来构造霍夫曼n叉树，构造n叉树的结点数目要求为大于等于3的奇数，若非奇数可以加上一个权值为0的结点。
![](https://i.loli.net/2019/01/28/5c4e5bf2d661c.png)

