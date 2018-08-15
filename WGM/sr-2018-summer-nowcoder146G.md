
# LETTers Solution Report

- Date: 15 August 2018
- Author: WGM
- Problem ID: [nowcoder - 146G](https://www.nowcoder.com/acm/contest/146/G)

## Description modeling

- 赛时用oeis做的，赛后补一下思路。
- 明显用欧拉定理V-E+F=2。点数要考虑内部的交点，而边数则是内部交点都有贡献且贡献都为1，所以关键是求内部交点的数量。考虑从一个顶点引出的边，会把多边形外围的交点分成i和n-i-2两部分，只要是从这两部分各取一个点相连，必会和这条边有内部交点，方案数为i*(n-i-2)。这样可以求出每个顶点的贡献，其中每个内部点会被重复记录4次。

## Points in solving

除法过程要逆元

## Warnings

3次方和4次方不能直接算，要每乘一次取一次模。

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

const long long MOD = 1e9 + 7;
int main()
{
    
    long long ans,n;
    scanf("%lld",&n);

    long long n2= n * n % MOD;
    long long n3= n2 * n % MOD;
    long long n4= n3 * n % MOD;

    (ans = 24 - 42*n) %= MOD;
    (ans += 23*n2) %= MOD; 
    (ans -= 6*n3) %= MOD;
    (ans += n4) %= MOD;
    (ans *= 41666667) %= MOD;
    (ans += MOD) %= MOD;

    printf("%lld",ans);

    return 0;
}


```
