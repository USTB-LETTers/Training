
# LETTers Solution Report

- Date: 21 April 2018
- Author: Alice_Margatroid
- Problem ID: [CodeForces - 699E ](http://codeforces.com/problemset/problem/699/E)

## Description modeling


题意：服务器中有n种视频，k个内存。每个内存可以放一个视频。

然后n种视频的需求概率分别给出。服务器的算法是这样的：每当有新的视频需求，释放内存中被最近被观看次数最低的视频，然后将需求视频纳入内存。

问在几乎无限次操作之后，内存中存在各个视频的概率。


## Points in solving

状压概率dp。

（我也不知道我怎么推出来的）
总之，设f[a1,a2,a3……an]代表内存中的视频为a1到an时的概率。

那么，最后每个视频分别的概率是所有包括它存在的视频组合的概率之和。

比方说，an的概率就是所有下标中包含an且有k个元素的f的和。

那么状态转移方程也就不是很难想了。比方说有7个视频，用二进制位表示它们存在与否。

那么，以1001101为例，它可以衍生出1101101,1011101,1001111这三种组合。那么，这三种组合的f值是f[1001101]分别乘以它们出现的概率。

注意，不是题目里给的那个概率，是那个概率再除以第2，3，6号元素的总概率之后的商。

答案呼之欲出了。

位运算的代码在大白p157。很好用。


最后注意当k值大于视频中概率不为0的数量的时候要把k值缩小。

```c++
#include<stdio.h>
#include<stdlib.h>
double a[1500000]={0},zgl;
double b[22]={0},sum[22]={0};
int main()
{
	int n=0,k=0,i,j=0,temp;
	char s[10]={0};
	scanf("%d%d",&n,&k);
	for(i=0;i<n;i++)
	{
		scanf("%lf",&b[i]);
		if(b[i]-0>1e-7)
		{	j++;}
		a[1<<i]=b[i];
	}
	if(k>j)
		k=j;
	for(i=1;i<=k;i++)
	{
		int comb= (1<<i)-1;
		while (comb<1<<n)
		{	
			zgl=0;
			temp=comb;j=0;
			while(j<n)
			{
				if((temp&1)==0)
					zgl+=b[j];
				j++;
				temp=temp>>1;
				
			}
			for(j=0;j<n;j++)
			{
				if(!(comb>>j&1)&&(zgl-0>1e-7))
				{
					a[comb|1<<j]+=a[comb]*b[j]/zgl;	
				}	
			}
			int x=comb&-comb,y=comb+x;
			comb=((comb&~y)/x>>1) | y;
			 
		} 
	}
	int comb= (1<<k)-1;
	while (comb<1<<n)
	{	
		for(j=0;j<n;j++)
		{
			if(comb>>j&1)
			{
				sum[j]+=a[comb];
			}	
		}
		int x=comb&-comb,y=comb+x;
		comb=((comb&~y)/x>>1) | y;
	} 
	for(i=0;i<n;i++)
	{
		printf("%.8lf ",sum[i]);
	}
	return 0;
}
```
## Warnings

小心发生除0现象
