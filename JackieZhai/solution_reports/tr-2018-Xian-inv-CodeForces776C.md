# LETTers Solution Report

- Date: 7 April 2018
- Author: JackieZhai
- Problem ID: [CodeForces776C](http://codeforces.com/problemset/problem/776/C)

## Description modeling

- 枚举连续和，用前缀和的方法最省时

## Points in solving

- 统计连续和的数量的时候用map，查找的时候快一些
- 1和-1注意要特判一下

## Warnings

- 自己瞎用线段树写了半天WA……之后发现即使不WA也会TLE

```c++
#include <bits/stdc++.h>
using namespace std;

const int maxn=100007;
typedef long long LL;
LL a[maxn],sum[maxn];
LL ans;
int n;

void solve(LL x)
{
	map<LL,int>mp;
	map<LL,int>::iterator it;
	for(int i=0; i<n; i++)
	{
		++mp[sum[i]];
		it = mp.find(sum[i+1]-x);
		if(it!=mp.end())//存在
			ans += it->second;
	}
}

int main()
{
	LL k;
	while(scanf("%d%I64d",&n,&k)!=EOF)
	{
		sum[0]=0;
		for(int i=1;i<=n;++i)
        {
			scanf("%I64d",&a[i]);
			sum[i]=sum[i-1]+a[i];
		}
		ans=0;
		if(k==1)
			solve(1);
		else if(k==-1)
		{
			solve(1);//对于子序列和为1的肯定也是-1的偶数次幂
			solve(-1);
		}
		else
		{
			LL cnt=1;
			while(cnt<=1e9*n)
			{
				solve(cnt);
				cnt*=k;
			}
		}
		printf("%I64d\n",ans);
	}
	return 0;
}
```