
# LETTers Solution Report

- Date: 25 July 2018
- Author: Alice_Margatroid

## Description modeling

水题


## Points in solving

if(i-k>=0)dp[i][1]=dp[i-k][0];
		dp[i][0]=(dp[i-1][1]+dp[i-1][0])%mo;
		sum[i]=(dp[i][0]+dp[i][1]+sum[i-1])%mo;

## Warnings

暂无。



##code

```c++
 #include<bits/stdc++.h>
using namespace std;
int mo=1000000007; 
int dp[100007][2],sum[100007];
int main()
{
	int i,n,m,t,k,l,r;
	scanf("%d%d",&n,&k);
	dp[1][0]=1;sum[1]=1;
	for(i=2;i<100000;i++)
	{
		if(i-k>=0)dp[i][1]=dp[i-k][0];
		dp[i][0]=(dp[i-1][1]+dp[i-1][0])%mo;
		sum[i]=(dp[i][0]+dp[i][1]+sum[i-1])%mo;
	}
	for(i=0;i<n;i++)
	{
		scanf("%d%d",&l,&r);
		printf("%d\n",(sum[r+1]-sum[l]+mo)%mo);
	}
	return 0;
}

```
