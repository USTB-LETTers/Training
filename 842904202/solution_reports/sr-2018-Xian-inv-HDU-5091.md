

# LETTers Solution Report

- Date: 18 April 2018
- Author: Alice_Margatroid
- Problem ID: [HDU - 4336](https://vjudge.net/problem/HDU-4336)

## Description modeling

（-20000，-20000）到（20000，20000）的网格，然后有n<=20000个点，问用一个W* H的方形网子最多能网住多少个点。

样例：
2 3 4
0 1
1 0
3 1 1
-1 0
0 1
1 0
-1

想了半天这算法那算法发现无一可行，上网查题解发现是线段树加扫描线，果然还是以力破巧一般的基本功问题。

大概思路：

在每个点向右W的位置即（x+w,y）建立映点，原点的p是1而映点的p是-1，之后从左至右，从下至上，先原点后映点地遍历所有点，每次在遍历的点对应的在y轴上的区间(y,y+h)上加上原点或者映点的p值。y轴用一个拥有80000个点的，维护区间最大值的线段树来存，每次改动更新最大值即可。

思想是扫描线加线段树，线段树基本是抄的大神的代码改了一下（线段树还不太熟练）。

代码：
```c++
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<algorithm>
#define maxn 100007 
#define ls l,m,rt<<1  
#define rs m+1,r,rt<<1|1 
using namespace std;
int Sum[maxn<<2],Add[maxn<<2],MAX=-1;
int A[maxn],n;
int w,h;
struct Node
{
	int x;
	int y;
	int p;      //p is the flag of point
}node[20005];
bool cmp(Node x,Node y)
{
	if(x.x==y.x)
	{
		if(x.p==y.p)
			return x.y<y.y;
		return x.p>y.p;
	}
	return x.x<y.x;
}
void PushUp(int rt){Sum[rt]=max(Sum[rt<<1],Sum[rt<<1|1]);}  
void Build(int l,int r,int rt){ 
    if(l==r) {
        Sum[rt]=0;
        return;  
    }  
    int m=(l+r)>>1;  
    Build(l,m,rt<<1);  
    Build(m+1,r,rt<<1|1);  
    PushUp(rt);  
}  
void Update(int L,int C,int l,int r,int rt){  
    if(l==r){
        Sum[rt]+=C;  
        return;  
    }  
    int m=(l+r)>>1;  
    if(L <= m) Update(L,C,l,m,rt<<1);  
    else       Update(L,C,m+1,r,rt<<1|1);  
    PushUp(rt); 
}   
void PushDown(int rt,int ln,int rn){  
    if(Add[rt]){  
        Add[rt<<1]+=Add[rt];  
        Add[rt<<1|1]+=Add[rt];  
	
        Sum[rt<<1]+=Add[rt];  
        Sum[rt<<1|1]+=Add[rt];  
        Add[rt]=0;  
    }  
}  
void Update(int L,int R,int C,int l,int r,int rt){
	
    if(L <= l && r <= R){
        Sum[rt]+=C;
        Add[rt]+=C;  
		for(int i=0;i<100;i++)
			printf("%d ",Sum[i]);
		system("pause");
        return ;   
    }  
    int m=(l+r)>>1;  
    PushDown(rt,m-l+1,r-m);
    if(L <= m) Update(L,R,C,l,m,rt<<1);  
    if(R >  m) Update(L,R,C,m+1,r,rt<<1|1);
    PushUp(rt);
}   

int Query(int L,int R,int l,int r,int rt){
    if(L <= l && r <= R){  
        return Sum[rt];  
    }  
    int m=(l+r)>>1;  
    PushDown(rt,m-l+1,r-m);   
    int ANS=0;  
    if(L <= m) ANS=max(ANS,Query(L,R,l,m,rt<<1));  
    if(R >  m) ANS=max(ANS,Query(L,R,m+1,r,rt<<1|1));  
    return ANS;  
}  

int main()
{
	int m,i,j;
	
	while(scanf("%d",&n)&&(n!=-1))
	{
		memset(Sum,0,sizeof(Sum));
		memset(Add,0,sizeof(Add));
		MAX=-1;		
		scanf("%d%d",&w,&h);
		for(i=0;i<n;i++)
		{
			scanf("%d%d",&node[i].x,&node[i].y);
			node[i].p=1;
			node[i+n].x=node[i].x+w;node[i+n].y=node[i].y;
			node[i+n].p=-1;
		}
		sort(node,node+2*n,cmp);
		Build(1,80005,1);
		for(i=0;i<2*n;i++)	
		{
			if(node[i].p==1)
			{
				Update(node[i].y+20001,node[i].y+h+20001,1,1,40001,1);
				MAX=max(MAX,Query(1,40001,1,40001,1));
			}
			if(node[i].p==-1)
			{
				Update(node[i].y+20001,node[i].y+h+20001,-1,1,40001,1);
			}
		}
		printf("%d\n",MAX);
	}
	return 0;
} 




```


## Points in solving

但是交上去的时候错了很多很多次。

我对比了一下网上的AC代码想起来线段树要开大好多………

然后我开了160000，超时。

弄得我心急如焚我说是不是查询效率太低了？
其实后来想想查询效率一点也不低因为每次就查Sum[0]一个值。

弄了半天我最后发现好像用不到160000个点，80000就够了。

改了一下试着交上去然后A了。

## Warnings

线段树开原数组的两倍就够了，大了小了都不好。

以及有时候这种看上去做不出来的题其实是因为没有找到方法。平心而论孙宇辉会线段树，说是扫描线的思想但其实没多复杂，我们完全有能力在赛时做出来，如果知道算法的话。

所以以后看见范围大，操作是区间加法的题，认真地考虑考虑线段树。
