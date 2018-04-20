
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

直接做就好

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
