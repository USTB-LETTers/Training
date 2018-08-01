

# LETTers Solution Report

- Date: 01 August 2018
- Author: Alice_Margatroid
- Problem ID: [nowcoder-141-G ]https://www.nowcoder.com/acm/contest/141/G

## Description modeling

求排列组合的个数。

简单来说，广搜遍历每个节点，在每个节点进行小范围深搜，最后将每个节点的值相乘得到结果

至于广搜为什么可行可以看https://www.nowcoder.com/discuss/88556?type=101&order=0&pos=1&page=1里面大佬的证明。


## Points in solving

卡超时快卡死我了，最后用了c++11并优化了一个无关的mumset之后，凑合a了。

## Warnings

暂无。



##code

```c++
#include <bits/stdc++.h> 
using namespace std; 
int tree[5005],sett[5005],set2[5005],set3[5005],ans[5005],n,k,arr[5005],hash1[5007][5007];
vector<int>v[5005];
void visit(int x,int d)
{
	int i;
	if(d==0)
		return;
	for(i=0;i<v[x].size();i++)
	{
		if(set2[v[x][i]]==0)
		{	
			if(set3[v[x][i]]==0)
				ans[v[x][i]]--;
			set2[v[x][i]]=1;
			visit(v[x][i],d-1);
			set2[v[x][i]]=0;
		}
	}
}
int solve(int x,int d)
{
	int i,j,head,tail;
	long long sum=1;
	head=0;tail=1;
	sett[x]=1;
	arr[head]=x;
	while(head<tail)
	{
	//	memset(set2,0,sizeof(set2));
		set2[arr[head]]=1;
		visit(arr[head],d);
		set2[arr[head]]=0;
		set3[arr[head]]=1;
		for(i=0;i<v[arr[head]].size();i++)
		{
			if(sett[v[arr[head]][i]]==0)
			{
				sett[v[arr[head]][i]]=1;
				arr[tail++]=v[arr[head]][i];
			}
		}
		
		
		head++;
	}	
	for(i=1;i<=n;i++)
	{
		sum=(sum*(k+ans[i]))%1000000007;
//		printf("%d %d\n",i,ans[i]+k);
	}
	return sum;
}
int main() 
{ 
	int i,d,t,x,y;
	scanf("%d%d%d",&n,&k,&d);
	for(i=0;i<n-1;i++)
	{
		scanf("%d%d",&x,&y);
		v[x].push_back(y);
        v[y].push_back(x);
	}
	int a=solve(x,d-1);
	memset(sett,0,sizeof(sett));
	memset(set2,0,sizeof(set2));
	memset(set3,0,sizeof(set3));
	memset(ans,0,sizeof(ans));
	memset(arr,0,sizeof(arr));
	int b=solve(x,d);
	printf("%d\n",((a-b)+1000000007)%1000000007);
	return 0;
}

```
