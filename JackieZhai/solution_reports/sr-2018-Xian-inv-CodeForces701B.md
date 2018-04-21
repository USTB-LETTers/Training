# LETTers Solution Report

- Date: 21 April 2018
- Author: JackieZhai
- Problem ID: [CodeForces701B](http://codeforces.com/problemset/problem/701/B)

## Description modeling

- 在国际象棋棋盘上放Rock，求没有被占领的位置

## Points in solving

- 运用set防止标记重复，而且能快速的计算size()的值
- 根据size()值计算没有被占领的位置

## Warnings

- 注意数据范围问题，要ll

```c++
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

ll n, m;
set<ll> ac, bc;

int main()
{
    scanf("%lld%lld", &n, &m);
    for(int i=0; i<m; i++)
    {
        ll x, y;
        scanf("%lld%lld", &x, &y);
        ac.insert(x);
        bc.insert(y);
        ll a=ac.size(), b=bc.size();
        if(i!=0)
            printf(" ");
        printf("%lld", n*n-(a+b)*n+a*b);
    }
    printf("\n");


    return 0;
}
```