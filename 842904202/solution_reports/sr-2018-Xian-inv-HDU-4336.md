
# LETTers Solution Report

- Date: 18 April 2018
- Author: Alice_Margatroid
- Problem ID: [HDU - 4336](https://vjudge.net/problem/HDU-4336)

## Description modeling

一包里有a[0]——a[n-1]的概率获得卡片0——n-1。
现在给定这些概率，求获得所有卡片所需要抽取次数的期望sum。
多组数据。

样例：
input
1
0.1
2
0.1 0.4

output
10.000
10.500

说实话这是一道期望题。凭空想规律不太好想，对着样例看了半天，发现了一些规律：
大概是每种卡的期望减去每两种卡概率和的期望再加上每三种卡概率和的期望……

容斥原理。大概是这样。我没怎么理解背后的道理但是验算了一些似乎都是对的。

代码：
```c++
#include<stdio.h>
#include<stdlib.h>
double a[22]={0};
int main()
{
	int n,i,j;
	double sum,k=-1;
	while(scanf("%d",&n)==1)
	{
		sum=0;
		for(i=0;i<n;i++)
		{
			scanf("%lf",&a[i]);
		}
		int m=1<<n,t=1;
		
		while(t<m)
		{
			double sumn=0;
			int q=t,temp=0;
			i=0;
			while(q)
			{
				if(q&1)
				{	sumn+=a[i];	temp++;}
				i++;
				q=q>>1;						
			}
			if(temp%2==1)
				k=-1;
			else
				k=1;
			sum-=k/sumn;
			t++;
		}
		printf("%.5lf\n",sum);
	}	
	
	return 0; 
}



```


## Points in solving

但是交上去的时候错了很多很多次。错到我怀疑算法的地步。

想来想去决定看题解。发现题解的最后的printf是“%.5lf”。而我根据样例写的是"%.3f"……

于是很可能是四舍五入的问题导致错了。

## Warnings

以后不要对着样例想当然。
