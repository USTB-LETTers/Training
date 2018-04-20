# LETTers Solution Report

- Date: 20 April 2018
- Author: JackieZhai
- Problem ID: [HDU4325](http://acm.hdu.edu.cn/showproblem.php?pid=4325)

## Description modeling

- 花开有一个区间，给定查询，问有几个花开
- 是区间修改、单点查询的问题，只不过修改的值都是1
- 可以二分、双线段树、双BIT实现(此处我用的是双BIT)

## Points in solving

- 需要进行坐标离散化，把10<sup>9</sup>的数据压成10<sup>5</sup>

## Warnings

- 无

```c++
//我的离散化写的是真的丑，应该写在函数里比较好
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

int N, M;

struct Node{
    ll n, x;
    friend bool operator < (const Node &a, const Node &b)
    {
        return a.n<b.n;
    }
}S[300007];
map<ll, ll> ma;


int L[100007], R[100007];
int Q[100007];

ll bit0[300007], bit1[300007];

ll sum(ll *b, int i)
{
    ll s=0;
    while(i>0)
    {
        s+=b[i];
        i-=i&-i;
    }
    return s;
}

void add(ll *b, int i, int v)
{
	while(i<=300007)
	{
		b[i]+=v;
		i+=i&-i;
	}
}



int main()
{
    int T;
    scanf("%d", &T);
    for(int kase=1; kase<=T; kase++)
    {
        printf("Case #%d:\n", kase);
        scanf("%d%d", &N, &M);
        memset(bit0, 0, sizeof(bit0));
        memset(bit1, 0, sizeof(bit1));
        ma.clear();



        int p=0;
        for(int i=1; i<=N; i++)
        {
            scanf("%d%d", &L[i], &R[i]);
            S[p++].n=L[i];
            S[p++].n=R[i];
        }
        for(int i=1; i<=M; i++)
        {
            scanf("%d", &Q[i]);
            S[p++].n=Q[i];
        }
        sort(S, S+p);
        int q=1;
        for(int i=0; i<p; i++)
        {
            if(i!=0 && S[i].n==S[i-1].n)
            {
                ;
            }
            else
            {
                S[i].x=q++;
                ma[S[i].n]=S[i].x;
            }
        }
        for(int i=1; i<=N; i++)
        {
            L[i]=ma[L[i]];
            R[i]=ma[R[i]];
        }



        for(int i=1; i<=N; i++)
        {
            add(bit0, L[i], -(L[i]-1));
            add(bit1, L[i], 1);
            add(bit0, R[i]+1, R[i]);
            add(bit1, R[i]+1, -1);
        }


        for(int i=1; i<=M; i++)
        {
            Q[i]=ma[Q[i]];
            ll res=0;
            res+=sum(bit0, Q[i])+sum(bit1, Q[i])*Q[i];
            res-=sum(bit0, Q[i]-1)+sum(bit1, Q[i]-1)*(Q[i]-1);
            printf("%lld\n", res);
        }

    }


    return 0;
}
```
