
# LETTers Solution Report

- Date: 29 July 2018
- Author: Alice_Margatroid
- Problem ID: [nowcoder-142-C ]https://www.nowcoder.com/acm/contest/142/C

## Description modeling

给所给数列求前n项和。

所给数列是一个具有树形特征的数列。我们可以发现，其前2^N次幂-1项和很好求，用一种类似记忆化的办法就行了。

写一半发现我写的函数可以求得树每一层的和但是求不了总的，还得一项项加起来……囧

好在这么写到后面也很方便。接下来就是比较恶心人的地方，求完所给N最接近的2的若干次幂项和之后，得计算多出来的那些项的和。

我用了很麻烦很不美观的办法，最后还卡了一下溢出，终于a了。


## Points in solving

本来还有两个小时的时候做的这个，当时以为再给我一阵子就能出来，补题后发现再给两个小时也不一定。

## Warnings

暂无。



##code

```c++
#include <bits/stdc++.h> 
using namespace std; 
long long m,a[100005],hash1[1005][1005],u=0,ans[1005],last=0,sum[100006]; //sum[100005]
long long n;
long long SumC(long long k,long long h)
{
	if(hash1[k][h]!=0)
		return hash1[k][h];
	else
	{
		if(h==1)
			return k;
		else
		{
			if(k==0)
				return hash1[0][h]=(2*SumC(1,h-1))%1000000007;
			else
				return hash1[k][h]=(SumC(k-1,h-1)+SumC(k+1,h-1))%1000000007;
		}
	}
}
long long Depth(long long k)
{
	long long x=0;
	while(k)
	{
		k/=2;
		x++;
	}
	return x;
}
long long Calcu(long long k)
{
	long long s=k*(k+1)/2,flag;
	if(s%2==0)
		flag=1;
	else
		flag=-1;
	if(k==1)
		return 0;
	else
		return Calcu(k/2)+flag;

}
long long Check(long long k)
{
	while(k%2!=1)
	{
		k/=2;
	}
	return Calcu(k-1);
}

long long Mi(long long k)
{
	long long a=1;
	while(k)
	{
		k/=2;
		a*=2;
	}
	return a/=2;
}
long long SumT(long long k)
{
	long long i,ans=0,sd=0,t=0;
	long long dp=Depth(k+1)-1;
	ans+=sum[dp];
	long long k2=k-(Mi(k+1)-1);	
	long long km=Mi(k);
	long long km2=km;	
	if(k2!=0)
	{
		while(km)
		{
			
			km=km>>1;
			sd++;
			if(k2>=km&&km!=0)
			{
				ans=(ans+SumC(abs(Check(km2+km+t)),Depth(k)-sd))%1000000007;
				k2-=km;
				t+=km;
			}
		}
	}
	return ans;
}


int main() 
{ 
	long long i,t,sd,j=1,k=2;
	scanf("%lld",&t);
	for(i=1;i<100;i++)
	{
		sum[i]+=(sum[i-1]+SumC(0,i))%1000000007;
	}
	while(t--)
	{
		scanf("%lld",&n);
		printf("%d\n",SumT(n));
	}
	return 0;
}
 

```
