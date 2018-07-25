
# LETTers Solution Report

- Date: 24 July 2018
- Author: WGM
- Problem ID: [nowcoder - 140A](https://www.nowcoder.com/acm/contest/140/A)

## Description modeling

直接DP

## Points in solving

记录前一状态是走还是跑

## Warnings

根据题意，k=1时也区分走和跑，不用特殊处理

## Codes

```c++
#include<bits/stdc++.h>
using namespace std;

const int MOD = 1000000007;
long long d[100010][2];
long long sum[100010];

int main()
{
	int Q,k;
	int i,j;
	memset(d,0,sizeof(d));
	memset(sum,0,sizeof(sum));
	scanf("%d %d",&Q,&k);

	d[0][0] = 1;
	d[1][0] = 1;
	if(k == 1)
		d[1][1] = 1,sum[1] = 2;
	else
		d[1][1] = 0,sum[1] = 1;
	sum[0] = 0;

	for(i=2;i<=100000;i++)
	{
		d[i][0] = (d[i-1][0] + d[i-1][1]) % MOD;
		if(i>=k)
			d[i][1] = d[i-k][0] % MOD;
		else 
			d[i][1] = 0;
		sum[i] = (sum[i-1] + d[i][0] +d[i][1]) % MOD;
	}

	while(Q--)
	{
		scanf("%d %d",&i,&j);
		printf("%lld\n",(sum[j] - sum[i-1] + MOD) % MOD);
	}

	return 0;
}
```
