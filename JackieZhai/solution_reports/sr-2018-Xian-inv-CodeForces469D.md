# LETTers Solution Report

- Date: 14 April 2018
- Author: JackieZhai
- Problem ID: [CodeForces469D](http://codeforces.com/problemset/problem/469/D)

## Description modeling

- 题意是要给你一组数：其中x要想加入集合A，数a-x也要在集合A中；要想加入集合B，数b-x也要在集合B中，问你能不能恰好分为两种集合
- 主要有以下几种情况：
    1. a-x和b-x都不属于这一组数中，直接返回NO
    2. a-x和b-x有一个属于这一组数中，只需要把x和相对应的数加到集合里就可以了
    3. a-x和b-x都属于这一组数中，那就得再看看有没有集合A和集合B重复的情况了，要是重复就还是不行

## Points in solving

- 运用并查集，由于数值范围到10<sup>9</sup>，所以无法把数作为并查集元素，只好用下标
- 运用map把num[]数组的下标和值反向，可以方便之后用值查找下标，完成并查集的操作unite()
- 运用并查集的0~n-1存下标、n存A集合、n+1存B集合，之后如果能够恰好分为两组，那么肯定有!same(n, n+1)为真

## Warnings

- 只有一个集合有元素，另一个集合没有元素的时候要特判一下（详见代码中的注释）

```c++
#include <bits/stdc++.h>
using namespace std;

const int MAX_N=100007;

int n, a, b;
int num[MAX_N];
map<int, int> m; //reverse of num

//DUS
int par[MAX_N];
int ran[MAX_N];
void init(int n)
{
	for(int i=0; i<n; i++)
	{
		par[i]=i;
		ran[i]=0;
	}
}
int find(int x)
{
	if(par[x]==x)
		return x;
	else
		return par[x]=find(par[x]);
}
void unite(int x, int y)
{
	x=find(x);
	y=find(y);
	if(x==y)
		return ;
	if(ran[x]<ran[y])
		par[x]=y;
	else
	{
		par[y]=x;
		if(ran[x]==ran[y])
			ran[x]++;
	}
}
bool same(int x, int y)
{
	return find(x)==find(y);
}
//DUS


int main()
{
    scanf("%d%d%d", &n, &a, &b);
    for(int i=0; i<n; i++)
    {
        scanf("%d", &num[i]);
        m[num[i]]=i;
    }

    init(n+7);//n->setA, n+1->setB

    for(int i=0; i<n; i++)
    {
        int am, bm;
	//exsit or not?
        if(m.find(a-num[i])!=m.end())
            am=m[a-num[i]];
        else
            am=-1;
        if(m.find(b-num[i])!=m.end())
            bm=m[b-num[i]];
        else
            bm=-1;
        //cout<<am<<" "<<bm<<endl;
        if(am!=-1)
            unite(i, am);
        else
            unite(i, n+1);
        if(bm!=-1)
            unite(i, bm);
        else
            unite(i, n);
    }
    if(same(n, n+1))
    {
        printf("NO\n");
    }
    else
    {
        printf("YES\n");
        for(int i=0; i<n; i++)
        {
            if(i!=0)
                printf(" ");
            if(same(n, i))
                printf("0");
            else //此处不能写"else if(same(n+1, i)"，因为这样全在一个集合情况就会WA
                printf("1");
        }
        printf("\n");
    }


    return 0;
}
```
