# LETTers Solution Report

- Date: 12 April 2018
- Author: JackieZhai
- Problem ID: [POJ3104](http://poj.org/problem?id=3468)

## Description modeling

- 有一些衣服，每件衣服有一定水量，有一个烘干机，每次可以烘一件衣服，每分钟可以烘掉M滴水
- 每件衣服没分钟可以自动蒸发掉一滴水，用烘干机烘衣服时不蒸发
- 问最少需要多少时间能烘干所有的衣服

## Points in solving

- 用二分法求解
- 题意是烘干机烘干的时候不会自然掉水
- 转化为烘干机每分钟掉M-1水，这样所有都是自然烘干掉1水了

## Warnings

- 注意烘干机烘的过程中，不会自动掉一滴水！

```c++
#include <cstdio>
#include <iostream>
#include <algorithm>
using namespace std;

const int INF=0x3f3f3f3f, MAX_N=100007;

int N, M;
long long x[MAX_N];

bool C(int minu)
{
	int coun=0;
	for(int i=0; i<N; i++)
	{
		if(x[i]-minu>0)
		{					   
			int xre=x[i]-minu; 
			if(xre%(M-1)==0)
				coun+=xre/(M-1);
			else
				coun+=xre/(M-1)+1;

			if(coun>minu)      
				return false;
		}
	}
	return true;
}

int main()
{
	scanf("%d",  &N);
	for(int i=0; i<N; i++)
		scanf("%lld", &x[i]);
	scanf("%d", &M);

	if(M==1)
	{
		int ans=0;
		for(int i=0; i<N; i++)
			if(ans<x[i])
				ans=x[i];
		printf("%d\n", ans);
	}
	else
	{

		int lb=0, ub=INF;
		while(ub-lb>1)
		{
			int mid=(ub+lb)/2;
			if(C(mid))
				ub=mid;
			else
				lb=mid;
		}

		printf("%d\n", ub);

	}

	return 0;
}
```