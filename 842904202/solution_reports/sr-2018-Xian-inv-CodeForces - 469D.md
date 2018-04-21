
# LETTers Solution Report

- Date: 7 April 2018
- Author: Alice_Margatroid
- Problem ID: [CodeForces - 469D ](https://vjudge.net/contest/223580#problem/D)

## Description modeling

若干值，要放进两个集合。

但是要求集合A之中的任意数ai，存在a-ai属于A
同样，集合B之中的任意数bi，存在b-bi属于B

问能否分成两个集合。如果可以，以0代表在集合A，1代表在集合B输出。

## Points in solving

直接做就好……才怪呢，又不是水题。

这个题要这么想：如果数x在集合a中有a-x,在b中有b-x,那么我们无法知道它到底属于哪个集合。

以及，如果把数值视为点，求和关系视为边，它们一定是许多个链条。

比如说：
a=29,b=30
数据为 4 25 26 3 5 24 6 27 2 1 28

那么可以有：

1-28-2-27-3-26-4-25-5-24-6 

可知：数据的2i和2i-1的和是a。2i和2i+1的和是b。

那么如果符合条件，数字们一定是这种链条的形式。
这种链条可以用类似并查集的方式实现。

遍历链条在借助map的情况下很快。所以只要枚举开头，发现如果
1：没有另一个值
2：链条长度是奇数
这两种情况的时候，可以输出NO。
其他时候，将链条上的每两个数算进一个集合里就好了。

按照翟大佬的题解，这个题有几个小技巧：

1：用map的下标存值，里面存数组位置。这样找起来很方便。

2：以n+1作为a集合的父亲节点，n+2作为b集合的父亲节点。

以及，一个极其坑爹的情况是a有时会等于b。需要加一个特判。

```c++
#include<bits/stdc++.h>
using namespace std;
map<long long,long long> map1;
long long s[200005]={0},set1[200005]={0},sum[200005]={0};
int main()
{
	long long n,a,b,j,flag=1;
	scanf("%lld%lld%lld",&n,&a,&b);
	for(int i=1;i<=n;i++)
	{
		scanf("%lld",&s[i]);
		map1[s[i]]=i;
	}
	if(a!=b)
	{
	for(int i=1;i<=n;i++)
	{
		if(map1[a-s[i]]!=0&&map1[b-s[i]]==0&&set1[i]==0&&(s[i]!=a-s[i])&&(s[i]!=b-s[i]))//n+1-a    n+2-b
		{
			int temp=i;
			while(map1[s[temp]]!=0)
			{
				set1[temp]=n+1;
				if(map1[a-s[temp]]!=0)
					set1[map1[a-s[temp]]]=n+1;
				else
					{flag=0;break;}
				temp=map1[b-s[map1[a-s[temp]]]];
			}
		}
		if(map1[a-s[i]]==0&&map1[b-s[i]]!=0&&set1[i]==0&&(s[i]!=a-s[i])&&(s[i]!=b-s[i]))
		{
			int temp=i;
			while(map1[s[temp]]!=0)
			{
				set1[temp]=n+2;
				if(map1[b-s[temp]]!=0)
					set1[map1[b-s[temp]]]=n+2;
				else
					{flag=0;break;}
				temp=map1[a-s[map1[b-s[temp]]]];
			}
		}
		if(s[i]==a-s[i])
			set1[i]=n+1;
		if(s[i]==b-s[i])
			set1[i]=n+2;
		if(map1[a-s[i]]==0&&map1[b-s[i]]==0)
		{
			flag=0;break;
		}
		
	}}
	else
	{
		for(int i=1;i<=n;i++)
		{
			if(map1[a-s[i]]==0)
				flag=0;
			set1[i]=n+1;
		}
	}
	if(flag)
	{	
		printf("YES\n");
		for(int i=1;i<=n;i++)
		{
			printf("%lld ",set1[i]-n-1);
		}	
	}
	else
		printf("NO");
	return 0;
}
```
## Warnings

暂无。
