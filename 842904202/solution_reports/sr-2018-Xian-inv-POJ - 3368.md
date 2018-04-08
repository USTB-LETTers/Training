# LETTers Solution Report

- Date: 8 April 2018
- Author: Alice_Margatroid
- Problem ID: [POJ - 3368](https://vjudge.net/contest/221157#problem/H)

## Description modeling

题目要求求出区间内众数出现的次数。所给数据单调。

这是一道基于ST表的RMQ。先预处理，把序列的众数求出来。之后面对查询区间[s,e],需要把[s,e]分成两个部分。
一个部分是[s,m]，m是从p开始的第一个不同的数字。
另一部分是[m,e]，这个时候，把[m,m+k]和[e-k，e]中较大的那个付给ans。k是第一个小于m到e的区间的长度的2的幂。

最后拿ans和s到m的长度进行比较。取较大值输出即可。

要注意多组数据的问题。因为样例里的结尾有一个“0”。

## Points in solving
代码如下：

```c++
#include<stdio.h>
#include<stdlib.h>
#include<math.h>
int a[100005]={0},b[100005][20]={0};
int max(int a,int b)
{
    return a>b?a:b;
}
int main()
{
	int n,q,i,j,temp=0,sum=0,sum1,sum2,s,e;
	while(scanf("%d",&n)&&n)
	{
	scanf("%d",&q);
	scanf("%d",&a[0]);
	b[0][0]++;
	for(i=1;i<n;i++)
	{
		scanf("%d",&a[i]);
		if(a[i]!=a[i-1])
			b[0][i]=1;
		else
			b[0][i]=b[0][i-1]+1;
	}
	for(i=1;i<(log10(n)/log10(2));i++)
	{
		for(j=0;j<n-(1<<(i-1));j++)
		{
			b[i][j]=b[i-1][j]>b[i-1][j+(1<<(i-1))]?b[i-1][j]:b[i-1][j+(1<<(i-1))];
		}
	}
	
	for(i=0;i<q;i++)
	{
		j=0;sum1=0;sum2=0;
		scanf("%d%d",&s,&e);
		s--;e--;
		j=s;
		if(j==0)
			j++;
		while(a[j]==a[j-1])
		{
			j++;
		}
		if(j>e)
			printf("%d\n",e-s+1);
		else
		{
			int lenth=e-j+1;
			int dep=(int)(log10(lenth)/log10(2));
			int qujian=(1<<(dep))-1;
			
			int ans=max(b[dep][j],b[dep][e-qujian]);
			printf("%d\n",max(j-s,ans));
		}	
	}
	for(i=0;i<(log10(n)/log10(2));i++)
	{
		for(j=0;j<n;j++)
		{
			b[i][j]=0;
		}
	}
	for(j=0;j<n;j++)
		{
			a[j]=0;
		}
	}
	return 0;	
}
```

## Warnings

暂无。
