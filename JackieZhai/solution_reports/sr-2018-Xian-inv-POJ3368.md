# LETTers Solution Report

- Date: 10 April 2018
- Author: JackieZhai
- Problem ID: [POJ3368](http://poj.org/problem?id=3368)
## Description modeling

- 给出不上升序列，求区间内最多出现的次数

## Points in solving

- 注意用线段树解决的时候的变形，要加存：<br>
	1. 这段区间出现最多的次数的个数
	2. 最左边那个数在这段区间连续的个数
	3. 最右边那个数在这段区间连续的个数

## Warnings

- 无

```c++
#include<cstdio>
#include<cmath>
#include<algorithm>
#include<iostream>
using namespace std;

const int Max=100007;

struct Node
{
    int l,r;
    int amax, lmaxm, rmax;    //amax用来记录这段区间出现最多的次数的个数，lmax用来记录最左边那个数在这段区间连续的个数，rmax用来记录最右边那个数在这段区间连续的个数
}node[Max*4];
int a[Max];

void build(int u, int l, int r)
{
    node[u].l=l;
    node[u].r=r;
    if(l==r)
    {
        node[u].amax=node[u].lmaxm=node[u].rmax=1;
        return;
    }
    int mid=(l+r)/2;
    build(u*2, l, mid);
    build(u*2+1, mid+1, r);
    int tem;
    if(a[node[u*2].r]==a[node[u*2+1].l])
    {
        tem=node[u*2].rmax + node[u*2+1].lmaxm;
    }
    else
    {
        tem=0;
    }
    node[u].amax=max(max(node[u*2].amax,node[u*2+1].amax),tem);
    node[u].lmaxm=node[u*2].lmaxm; //大区间的最左边的那个数和左子区间那个数值相同的
    if(node[u*2].lmaxm==mid-l+1&&a[node[u*2].r]==a[node[u*2+1].l]) //判断左子区间里的数是否相同并且和右子区间最左边那个数相同，相同则大区间lmax需要变化
    {
        node[u].lmaxm+=node[u*2+1].lmaxm;
    }
    node[u].rmax=node[u*2+1].rmax; //大区间的最右边的那个数和右子区间那个数值相同的

    if(node[u*2+1].rmax==r-mid&&a[node[u*2].r]==a[node[u*2+1].l]) //判断右子区间里的数是否相同并且和左子区间最右边那个数相同，相同则大区间rmax需要变化
    {
        node[u].rmax+=node[u*2].rmax;
    }
}

int query(int u, int l, int r)
{
    if(node[u].l==l&&node[u].r==r)
    {
        return node[u].amax;
    }
    int mid=(node[u].l+node[u].r)/2;
    if(r<=mid)
        return query(u*2, l, r);
    else if(l>mid)
        return query(u*2+1, l, r);
    else
    {
        int a1=query(u*2, l, mid);
        int a2=query(u*2+1, mid+1, r);
        int a3=0;
        if(a[node[u*2].r]==a[node[u*2+1].l]) //比较
        {
            a3=min(node[u*2].rmax,mid-l+1) + min(node[u*2+1].lmaxm,r-mid);
        }
        return max(max(a1,a2),a3);
    }
}

int main()
{
    int n, p, x, y;
    while(scanf("%d",&n)!=EOF)
    {
        if(n==0)
            break;
        scanf("%d", &p);
        for(int i=1; i<=n; i++)
        {
            scanf("%d", &a[i]);
        }
        build(1,1,n);
        for(int i=0; i<p; i++)
        {
            scanf("%d%d", &x, &y);
            printf("%d\n", query(1, x, y));
        }
    }

    return 0;
}
```