
# LETTers Solution Report

- Date: 24 July 2018
- Author: WGM
- Problem ID: [nowcoder - 139E](https://www.nowcoder.com/acm/contest/139/E)

## Description modeling

- 与简单DP相比，不好处理的是删了不同位置的相同元素，导致子序列重复。
    比如序列12a345a，转移到第二个a的位置即d[7]时，如果删除了两个a包含的部分a345a，则剩下的12-----部分的状态情况会与d[2]的12部分状态一样，即重复。所以要去重的部分为去掉两个相同元素间所有元素的之前状态。 
- d[i][j]表示当前位置i，已经删除j个，不删除s[i]则由d[i-1][j]转移来，删除s[j]则由d[i-1][j-1]转移来。

## Points in solving



## Warnings

减法取模可能有负数,不妨在每次状态转移最后都用DP += MOD; DP %= MOD;

## Codes

```c++
#include<bits/stdc++.h>
using namespace std;

const int MAXN = 100010;
const int MOD = 1000000000 + 7;

int s[MAXN],pos[15];
int d[MAXN][15],pre[MAXN];

int main()
{
    int N,M,K;

    while(~scanf("%d %d %d",&N,&M,&K))
    {
        memset(pos,0,sizeof(pos));
        memset(pre,0,sizeof(pre));
        memset(d,0,sizeof(d));

        for(int i=1; i<=N; i++)
        {
            scanf("%d",&s[i]);
            pre[i] = pos[ s[i] ];
            pos[ s[i] ] = i;
        }

        d[0][0] = 1;
        for(int i=1; i<=N; i++)
        {
            d[i][0] = 1;
            for(int j=1; j<=(i<M?i:M); j++)
            {
                d[i][j] += (d[i-1][j-1] + d[i-1][j]) % MOD;
                if( (pre[i] != 0) && (j - (i - pre[i]) >= 0) )
                    d[i][j] -= d[ pre[i] -1 ][ j - (i - pre[i]) ];
                d[i][j] += MOD;
                d[i][j] %= MOD;
            }
        }

        /*
        for(int i=1; i<=N; i++)
        {
            for(int j=0; j<=M; j++)
                printf(" %d ",d[i][j]);
            printf("\n");   
        }
        */

        printf("%d\n",d[N][M]);
    }

    return 0;
}
```
