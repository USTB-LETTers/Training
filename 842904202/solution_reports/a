# LETTers Solution Report

- Date: 7 April 2018
- Author: Alice_Margatroid
- Problem ID: [CodeForces - 616B ](http://codeforces.com/problemset/problem/616/B)

## Description modeling

在一个矩阵中寻找最大的每行最小值。

直接模拟就行

## Points in solving

直接做就好

```c++
#include<stdio.h>
#include<stdlib.h>
int a[105][105]={0},max[105]={0},ans=-100;
int main()
{
	int n,m,i,j;
	scanf("%d%d",&n,&m);

	for(i=0;i<n;i++)
	{
		max[i]=2147482645;
		for(j=0;j<m;j++)
		{
			scanf("%d",&a[i][j]);
			if(max[i]>a[i][j])
				max[i]=a[i][j];
		}
		if(ans<max[i])
			ans=max[i];
	}
	printf("%d",ans);
	return 0;
}
```
## Warnings

暂无。
