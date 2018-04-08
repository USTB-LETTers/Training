# LETTers Solution Report

- Date: 8 April 2018
- Author: JackieZhai
- Problem ID: [HDU5239](http://acm.hdu.edu.cn/showproblem.php?pid=5239)

## Description modeling

- 维护一个数组，每次操作是在区间[l, r]内
- 把区间内的元素加到ans中，再分别平方，模取9223372034707292160
- 线段树学习教材选~

## Points in solving

- 关键在于看出来是任何数平方29次之后就不变了，标记一下，就大大降低了计算复杂度

## Warnings

- 注意爆long long，需要用unsigned long long
- 乘法的时候要用mod_mul，不然llu也会爆

```c++
#include <bits/stdc++.h>
using namespace std;

typedef unsigned long long ll;
const int MAX_N=100005;
const ll MOD=9223372034707292160ll;
ll sum[MAX_N<<2];
bool cover[MAX_N<<2];
int n, q;

ll mod_mul(ll a, ll k)
{
    ll c = 0;
    while(k)
    {
        if(k & 1) c = (c+a) % MOD;
        a = (a+a) % MOD;
        k >>= 1;
    }
    return c;
}

void build(int k, int l, int r)
{
    sum[k]=cover[k]=0;
    if(l==r)
    {
        scanf("%I64u", &sum[k]);
        return ;
    }
    int mid=(l+r)>>1;
    int ls=k<<1, rs=(k<<1)+1;
    build(ls, l, mid);
    build(rs, mid+1, r);
    sum[k]=(sum[ls]+sum[rs])%MOD;
}

int ql, qr;
ll query(int k, int l, int r)
{
    if(ql<=l && r<=qr)
    {
        return sum[k];
    }
    int mid=(l+r)>>1;
    int ls=k<<1, rs=(k<<1)+1;
    ll ret=0;
    if(ql<=mid)
        ret=(ret+query(ls, l, mid))%MOD;
    if(qr>mid)
        ret=(ret+query(rs, mid+1, r))%MOD;
    return ret;
}

void modify(int k, int l, int r)
{
    if(cover[k] && ql<=l && r<=qr)
        return ;
    if(l==r)
    {
        ll tmp=mod_mul(sum[k], sum[k]);
        if(tmp==sum[k])
            cover[k]=true;
        sum[k]=tmp;
        return ;
    }
    int mid=(l+r)>>1;
    int ls=k<<1, rs=(k<<1)+1;
    if(ql<=mid)
        modify(ls, l, mid);
    if(qr>mid)
        modify(rs, mid+1, r);
    cover[k]=cover[ls]&cover[rs];
    sum[k]=(sum[ls]+sum[rs])%MOD;
}

int main()
{
    int T;
    scanf("%d", &T);
    for(int kase=1; kase<=T; kase++)
    {
        printf("Case #%d:\n", kase);
        scanf("%d%d", &n, &q);

        build(1, 1, n);

        ll ans=0;
        while(q--)
        {
            scanf("%d%d", &ql, &qr);
            ans=(ans+query(1, 1, n))%MOD;
            printf("%I64u\n", ans);
            modify(1, 1, n);
        }
    }

    return 0;
}
```
