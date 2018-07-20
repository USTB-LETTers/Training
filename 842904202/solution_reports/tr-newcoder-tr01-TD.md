# LETTers Solution Report

- Date: 8 April 2018
- Author: Alice_Margatroid
- Problem ID: [CodeForces - 415A  ](https://vjudge.net/contest/221157#problem/E)

## Description modeling

在B图中找和A图同构的子图。二者点集一致。


## Points in solving

找子图可以通过枚举点集的全排列，然后进行边的查找，如果某个点集排列的所有a图下的边都在B图中，那么可以视为一个可行解。

然而a图本身存在自同构的问题。孙宇辉做题的时候考虑到了第一个，第二个我们注意到了，但是没有想到可以用自同构来进行计算。用了哈希判重结果没对。

题目本身强调技巧，没做对很可惜。

## Warnings

暂无。



##code

```c++
#include<bits/stdc++.h>
using namespace std;
int v[100005];
int e1[105][105],e2[105][105];
int main()
{
	int n,i,j,k,ea,eb,mul=1,x,y,flag,sum1=0,sum2=0; 
	while(scanf("%d%d%d",&n,&ea,&eb)!=EOF)
	{
		memset(v,0,sizeof(v));
		for(i=0;i<100;i++)	
		{
			for(j=0;j<100;j++)
			{
				e1[i][j]=0;
				e2[i][j]=0;
			}
		}
		sum1=0;sum2=0;
		mul=1;
		for(i=0;i<ea;i++)
		{
			scanf("%d%d",&x,&y);
			x--;y--;
			e1[x][y]=1;
			e1[y][x]=1;
		}
		for(i=0;i<eb;i++)
		{
			scanf("%d%d",&x,&y);
			x--;y--;
			e2[x][y]=1;
			e2[y][x]=1;
		}
		for(i=0;i<n;i++)
		{
			v[i]=i;
			mul*=(i+1);
		}
		for(i=0;i<mul;i++)
		{
			next_permutation(v,v+n);
			flag=1;
			for(j=0;j<n;j++)
			{
				for(k=0;k<n;k++)
				{
					if(e1[j][k]==1)
					{
						if(e1[v[j]][v[k]]==0)
						{
							flag=0;
						}
					}	
				}
			}
			if(flag==1)
				sum1++;	
		}
		for(i=0;i<n;i++)
		{
			v[i]=i;
		}
		for(i=0;i<mul;i++)
		{
			next_permutation(v,v+n);
			flag=1;
			for(j=0;j<n;j++)
			{
				for(k=0;k<n;k++)
				{
					if(e1[j][k]==1)
					{
						if(e2[v[j]][v[k]]==0)
						{
							flag=0;
						}
					}	
				}
			}
			if(flag==1)
				sum2++;	
		}	
		printf("%d\n",sum2/sum1);
	}
	return 0;
}

```
