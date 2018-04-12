# LETTers Solution Report

- Date: 12 April 2018
- Author: JackieZhai
- Problem ID: [POJ3468](http://poj.org/problem?id=3468)

## Description modeling

- 维护一个区间：
    1. 将区间内数字同时加一个数
    2. 查询区间的和

## Points in solving

### Method 1
- 运用线段树解决，还是比较容易的
```c++
#include <iostream>
#include <cstring>
#include <cstdio>
#include <cmath>
#include <set>
#include <queue>
#include <vector>
#include <cstdlib>
#include <algorithm>

#define ls u << 1
#define rs u << 1 | 1
#define lson l, mid, u << 1
#define rson mid + 1, r, u << 1 | 1

using namespace std;
typedef long long ll;
const int M = 1e5 + 100;
ll sum[M << 2],tmp[M << 2];

void pushup(int u)
{
    sum[u] = sum[ls] + sum[rs];
}

void pushdown(int l,int r,int u)
{
    int mid = (l + r) >> 1;
    if(tmp[u])
    {
        tmp[ls] += tmp[u];
        tmp[rs] += tmp[u];
        sum[ls] += (mid - l + 1) * tmp[u];
        sum[rs] += (r - mid) * tmp[u];
        tmp[u] = 0; //注意消除延迟标记.
    }
}

void build(int l,int r,int u)
{
    if(l == r)
    {
        scanf("%I64d",sum + u);
    }
    else
    {
        int mid = (l + r) >> 1;
        build(lson);
        build(rson);
        pushup(u);
    }
}


void update(int L,int R,int c,int l,int r,int u)
{
    int mid = (l + r) >> 1;
    if(L <= l && R >= r)
    {
        tmp[u] += c;
        sum[u] += 1LL * (r - l + 1) * c;
        return;
    }
    pushdown(l, r, u);
    if(L <= mid)
        update(L, R, c, lson);
    if(R > mid)
        update(L, R, c, rson);
    pushup(u);
}

ll query(int L,int R,int l,int r,int u)
{
    int mid = (l + r) >> 1;
    if(L <= l && R >= r)
    {
        return sum[u];
    }
    ll res = 0;
    pushdown(l, r, u);
    if(L <= mid)
        res += query(L, R, lson);
    if(R > mid)
        res += query(L, R, rson);
    return res;
}

int main()
{
    int n,m;
    char s[10];
    cin>>n>>m;
    memset(tmp,0,sizeof(tmp));
    build(1, n, 1);
    while(m--)
    {
        int x,y;
        scanf("%s %d %d", s, &x, &y);
        if(s[0] == 'C')
        {
            int c;
            scanf("%d", &c);
            update(x, y, c, 1, n, 1);
        }
        else
        {
            printf("%I64d\n",query(x, y, 1, n, 1));
        }
    }

    return 0;
}
```

### Method 2
- 运用树状数组解决
- 如果用一个BIT，更新区间的时候会O(nlogn)，所以需要用到两个线段树处理增量操作，降低为O(logn)
```c++
#include <cstdio>
#include <iostream>
#include <algorithm>
using namespace std;

typedef long long ll;

//index-1
ll bit[100007], n;
ll sum(int i)
{
    ll s=0;
    while(i>0)
    {
        s+=bit[i];
        i-=i&-i;
    }
    return s;
}
void add(int i, ll x)
{
    while(i<=n)
    {
        bit[i]+=x;
        i+=i&-i;
    }
}
//index-1
ll bit2[100007], n2;
ll sum2(int i)
{
    ll s=0;
    while(i>0)
    {
        s+=bit2[i];
        i-=i&-i;
    }
    return s;
}
void add2(int i, ll x)
{
    while(i<=n)
    {
        bit2[i]+=x;
        i+=i&-i;
    }
}

int q;

int main()
{
    scanf("%d%d", &n, &q);
    for(int i=1; i<=n; i++)
    {
        ll x;
        scanf("%lld", &x);
        add(i, x);
    }
    for(int i=1; i<=q; i++)
    {
        char type;
        getchar();
        type=getchar();
        if(type=='Q')
        {
            int l, r;
            scanf("%d%d", &l, &r);
            printf("%lld\n", (sum2(r)*r+sum(r))-(sum2(l-1)*(l-1)+sum(l-1)));
        }
        else
        {
            int l, r;
            ll ad;
            scanf("%d%d%lld", &l, &r, &ad);
            add2(l, ad);
            add2(r, -ad);
            add(l, ad*(-l+1));
            add(r, ad*r);
        }
    }

    return 0;
}
```

## Warnings

- 无