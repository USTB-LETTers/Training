
# LETTers Solution Report

- Date: 25 July 2018
- Author: WGM
- Problem ID: [nowcoder - 140D](https://www.nowcoder.com/acm/contest/140/D)

## Description modeling

直接DP

## Points in solving

记录当前手上有没有商品

## Warnings

如果数据量大，可以考虑优化无用区间（贪心思想）

## Codes

```c++
#include<bits/stdc++.h>
using namespace std;

struct D
{
	long long m;
	int n;
}d[2],x,y;

long long a;

int main()
{
	int n,i,t;
	scanf("%d",&t);
	while(t--)
	{
		scanf("%d",&n);
		scanf("%lld",&a);
		d[0].m = 0;
		d[1].m = -a;
		d[0].n = 0;
		d[1].n = 1;

		for(i=2;i<=n;i++)
		{
			scanf("%lld",&a);

			x = d[0];
			y = d[1];

			if( (x.m > y.m + a) || ( (x.m == y.m + a)&&( x.n <= y.n + 1) ) )
				d[0].m = x.m,d[0].n = x.n; 
			else 
				d[0].m = y.m + a,d[0].n = y.n + 1;

			if( (x.m - a > y.m) || ( (x.m - a == y.m)&&( x.n + 1 < y.n) ) )
				d[1].m = x.m - a,d[1].n = x.n + 1; 
			else 
				d[1].m = y.m,d[1].n = y.n;
			
		}

		if( (d[0].m > d[1].m) || ( (d[0].m = d[1].m)&&(d[0].n <= d[1].n) ) )
			printf("%lld %d\n",d[0].m,d[0].n);
		else
			printf("%lld %d\n",d[1].m,d[1].n);

	}

	return 0;
}

```
