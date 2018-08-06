
# LETTers Solution Report

- Date: 6 August 2018
- Author: Alice_Margatroid
- Problem ID: [144C ](https://www.nowcoder.com/acm/contest/144/C)

## Description modeling

计算某种特殊的排列组合

给定N个空集和M个数，每第i次操作选择M中的1个，将之放入i到n的每一个集合。
求最后不同的方案数。


## Points in solving

解出排列求和之后，利用已储存的逆元和不断迭代的Sum实现快速求和。

## Warnings

暂无。



##code

```c++
#include<bits/stdc++.h>
using namespace std;
long long a[10000],mod=998244353,inv[2000005];
long long A(long long a)
{
	if(a==0)return 1;
	if(a==1)return 1;
	else
		return A(a-1)*a;
}
long long C(long long a,long long b)
{
	return (A(a)/A(a-b))/A(b);
}
long long power_mod(long long a, long long b, long long mod)
{
    long long  ans = 1;
    while (b)
    {
        if (b & 1) ans = ans * a % mod;
        a = a * a % mod;
        b >>= 1;
    }
    return ans;
}

int main()
{
	long long i,t,n,m,k,ans,q=1;
	
	scanf("%lld",&t);
	inv[1]=  inv[0] = 1;
	for(int i = 2;i < 1000005; ++i) inv[i]=inv[mod%i]*(mod-mod/i)%mod;
	while(t--)
	{
		ans=0;
		scanf("%lld%lld",&n,&m);
		long long up=min(n,m);
		m=m%mod;
		n=n%mod;
		long long sum=m;
		for(i=1;i<=up;i++)
		{
			k=i;
			ans=(ans+sum)%mod;
			sum=sum*(n-k)%mod*(m-k)%mod*inv[k]%mod;
			
			
		//	printf("%d %d %d %d\n",C(n,k),A(k),C(m,k),C(n,k)*A(k)*C(m,k));
		}
		printf("Case #%lld: %lld\n",q++,ans);
	}
	
	
	return 0;
}

```
