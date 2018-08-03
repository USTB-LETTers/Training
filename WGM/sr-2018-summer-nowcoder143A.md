
# LETTers Solution Report

- Date: 3 August 2018
- Author: WGM
- Problem ID: [nowcoder - 143A](https://www.nowcoder.com/acm/contest/143/A)

## Description modeling

- 关键是要想到二分，因为删除当前课的优先级与目标成绩有关
- 二分答案为ans，移项后第i项贡献为s[i](c[i]-ans)，为负时就要考虑删除（就是小于加权平均分），选择最小的（负绝对值最大的）k个，或不满k个时所有负的，删除，将结果与期望值ans比较，进行二分。

## Points in solving

先求总和，每次二分把删除的课从综合中删除，减少求和的步骤。

## Warnings

题目中的变量名是反的= =读题注意

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

const int MAXN = 1e5 +10;

struct G
{
    long long s,c;
    double val;
}g[MAXN];

bool cmp(G a,G b)
{
    return a.val>b.val;
}

int n,k;
long long sumc=0,sums=0;
double find(double l,double r)
{
    double mid = (l+r)*1.0 / 2;
    if(fabs(l-r) <= 1e-6)
        return mid;

    long long ansfz=sumc,ansfm=sums;
    for(int i=1; i<=n; ++i)
        g[i].val = g[i].s * 1.0 * (mid - g[i].c); 

    sort(g+1,g+1+n,cmp);
    for(int i=1; i<=k; ++i)
    {
        if(g[i].val <= 0)
            break;
        ansfz -= g[i].s * g[i].c;
        ansfm -= g[i].s;
    }

    if(ansfz >= ansfm * mid)
        return find(mid,r);
    else
        return find(l,mid);
}

int main()
{
    scanf("%d %d",&n,&k);
    for(int i=1; i<=n; ++i)
    {
        scanf("%lld",&g[i].s);
        sums += g[i].s;
    }
    for(int i=1; i<=n; ++i)
    {
        scanf("%lld",&g[i].c);
        sumc += g[i].s * g[i].c;
    }

    if(k == 0)
        printf("%.6lf",sumc*1.0/sums);
    else
        printf("%.6lf",find(0,sumc));
    
    return 0;
}

```
