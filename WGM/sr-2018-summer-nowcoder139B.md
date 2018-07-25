
# LETTers Solution Report

- Date: 25 July 2018
- Author: WGM
- Problem ID: [nowcoder - 139B](https://www.nowcoder.com/acm/contest/139/B)

## Description modeling

矩阵对称，且对角线都为0，符合**图的邻接矩阵**的特征，所以将条件看作每个结点度为2、有多重边且无自环，求其数量。

## Points in solving

- 结点度为2，必定成环（多重边可以视为只有两个节点的小环），因此有多个图，每个图都是一个环，没有单独的节点。明显可以分割成不同部分，再结合有效输入只有一个n，考虑DP。，
- 第i个节点一定要在某个环上，所以可以从i-1个节点中选出k个节点与i成环，剩下的i-1-k个节点的情况就是d[i-1-k]
  - 而k+1个节点成一个环的方案有k!/2种，简单推导一下，按顺时针或者逆时针顺序枚举下一节点k!，显然顺时针和逆时针应该算同一种,再除以2。
  - 特例k=1，有一种而不是1/2种。
  - 只需要考虑这k+1个节点成一个环，如果是成多个环会与不同k的值有重复。
- 推出状态转移方程为$d[i]=C_{i-1}^1d[i-2]+\sum_{k=2}^{i-3}{C_{i-1}^{k}d[i-1-k]\frac{k!}{2}}$,复杂度n²，肯定要优化
  - 先化简$d[i]=(i-1)d[i-2]+\sum_{k=2}^{i-3}{\frac{(i-1)!}{2(i-k-1)!}d[i-1-k]}$,观察d[i-1]，可以把d[i]减去(i-1)d[i-1]进行部分消去。
- 最终结论为$d[i]=(i-1)d[i-1]+(i-1)d[i-2]-\frac{(i-1)(i-2)d[i-3]}{2}$

## Warnings

- 循环变量用long long，否则(i-1)\*(i-2)部分会溢出
- 理解公式中除2的含义，只是为了除去枚举重复情况，并不是针对状态本身，因此不需要除法逆元取模
- 减法取模产生负数

## Codes

```c++
#include <bits/stdc++.h>
using namespace std;

const int MAXN = 100010;
long long MOD;
long long d[MAXN];
int main()
{
    int n;
    while(~scanf("%d %lld",&n,&MOD))
    {
        d[2] = 1;
        d[3] = 1;
        d[4] = 6 % MOD;
        for(long long i=5; i<=n; i++)
        {
            d[i] = (i-1) * (d[i-1] + d[i-2]) % MOD - (i-1) * (i-2) / 2 * d[i-3] % MOD;
            d[i] = (d[i] % MOD + MOD) % MOD;
            //printf("%lld %lld\n",i,d[i]);
        }

        printf("%lld\n",d[n]);
    }
    

    return 0;
}
```
