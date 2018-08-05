
# LETTers Solution Report

- Date: 5 August 2018
- Author: WGM
- Problem ID: [nowcoder - 143F](https://www.nowcoder.com/acm/contest/143/F)

## Description modeling

- 考虑每个钻石对交换次数的贡献，需要知道在这个位置出现前的、比当前d值大的所有钻石概率取反之积。方案要么是按位置排序、想办法处理d的顺序，或者是按d排序、想办法处理位置的顺序。
- 用d排序，逐个插入原本的位置，因为先插入的都是d比当前大的，所以之前插入的都是会对现在产生影响的，而位置则通过存储位置(下标)体现。要支持单点修改和查询(前缀积)，用树状数组实现比较容易

## Points in solving

- 最关键的就是通过插入顺序和位置来控制两个量。
- 题目中解释的取模其实就是整除取模，由于后面的概率都是相乘，所以可以在插入的时候直接进行逆元处理。

## Warnings

学会了新的写法,把{a += b;a %= MOD;}写成(a += b) % MOD;两句简成一句，并且有时能省下大括号。

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

const int MAXN = 100000 + 10;
const int MOD = 998244353;
int n;
long long tree[MAXN];
struct Node
{
    int p,d,pos;
}a[MAXN];

bool cmp(Node a,Node b)
{
    return a.d>b.d;
}

long long ksm(long long a,long long b)
{
    long long ans=1;
    while(b)
    {
        if(b & 1)
            (ans *= a) %= MOD;
        (a *= a) %= MOD;
        b >>= 1;
    }
    return ans;
}

int lowbit(int x)
{
    return x & (-x);
}

void init()
{
    for(int i=1; i<=n; ++i)
        tree[i] = 1;
    return;
}

void Update(int i,int x)
{
    while(i <= n)
    {
        (tree[i] *= x) %= MOD;
        i += lowbit(i);
    }
    return;
}

long long Query(int i)
{   
    long long ans = 1;
    while(i > 0)
    {
        (ans *= tree[i]) %= MOD;
        i -= lowbit(i);
    }
    return ans;
}

int main()
{
    scanf("%d",&n);
    for(int i=1; i<=n; ++i)    
    {
        scanf("%d %d",&a[i].p,&a[i].d);
        a[i].pos = i;
    }
    sort(a+1,a+1+n,cmp);

    init();
    long long temp = ksm(100,MOD-2);
    long long ans = 0;
    for(int i=1; i<=n; ++i)
    {
        ans += (Query(a[i].pos-1) * a[i].p % MOD) * temp % MOD;
        ans %= MOD;
        Update(a[i].pos,temp * (100-a[i].p) % MOD);
    }

    printf("%lld\n",ans);

    return 0;
}


```
