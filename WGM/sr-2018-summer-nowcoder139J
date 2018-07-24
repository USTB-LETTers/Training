
# LETTers Solution Report

- Date: 22 July 2018
- Author: WGM
- Problem ID: [nowcoder - 139J](https://www.nowcoder.com/acm/contest/139/J)

## Description modeling

将原数列复制成两倍并取中间的区间，即可转化为一般的“用树状数组求区间内不同数字的数量”。

## Points in solving

1.倍增，将不连续区间(左右两边)转化成连续区间
2.树状数组用法：将查询区间按区间右端升序排序，遍历每个数字，该数字在之前出现位置的贡献为0，在当前位置的贡献为1。因为不能计算重复的数字，而又按区间右端排序，所以只保留该数在当前位置之前最右边的一次出现。只要保证无重复，就可以前缀和记录出现了多少数字，就可以一边遍历数列一边求对应区间。

## Warnings

把之前出现位置的贡献变成0的时候，树状数组的更新应该是-1，而不是赋值0，因为树状数组记录的是和而不是值。

## Codes
```c++

#include<bits/stdc++.h>
using namespace std;

int lowbit(int x)
{
	if(x == 0)
		return 0;
	return x & (-x);
}

const int MAXN = 100000 + 7;
int tree[MAXN << 1],N;

int Query(int r)
{
	int sum = 0;
	while(r >= 1)
	{
		sum += tree[r];
		r -= lowbit(r);
	}

	return sum;
}

void Update(int x,int v)
{
	while(x <= (N << 1))
	{
		tree[x] += v;
		x += lowbit(x);
	}
	return;
}

int num[MAXN << 1];
struct Q
{
	int l,r,n,ans;
}q[MAXN << 1];

bool cmp(Q x,Q y)
{
	if( (x.r < y.r) || ( (x.r == y.r) && (x.l <= y.l) ) )
		return true;
	return false;
}

bool cmpn(Q x,Q y)
{
	return x.n < y.n;
}

int pos[MAXN << 1];
int vis[MAXN << 1];
int main()
{
	while(~scanf("%d",&N))
	{
		int M;
		scanf("%d",&M);
		for(int i=1; i<=N; i++)
		{
			scanf("%d",&num[i]);
			num[i+N] = num[i];
		}
		for(int i=1; i<=M; i++)
		{
			scanf("%d %d",&q[i].l, &q[i].r);
			int t = q[i].l;
			q[i].l = q[i].r;
			q[i].r = t + N;
			q[i].n = i;
		}
		sort(q+1, q+M+1, cmp);

		int nowq = 1; 
		memset(pos,0,sizeof(pos));
		memset(vis,0,sizeof(vis));
		memset(tree,0,sizeof(tree));
		
		for(int i=1; i<=(N << 1); i++)
		{
			if(pos[ num[i] ])
			{
				vis[ pos[ num[i] ] ] = 0;
				Update(pos[ num[i] ],-1);
			}
			vis[i] = 1;
			pos[ num[i] ] = i;
			Update(i,vis[i]);

			while(i == q[nowq].r)
			{
				q[nowq].ans = Query(q[nowq].r) - Query(q[nowq].l - 1);
				nowq++;
			}
			
		}

		sort(q+1,q+M+1,cmpn);
		for(int i=1; i<=M; i++)
			printf("%d\n",q[i].ans);
	}
		

	return 0;
}

```
