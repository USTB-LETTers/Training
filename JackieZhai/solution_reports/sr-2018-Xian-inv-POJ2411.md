# LETTers Solution Report

- Date: 19 April 2018
- Author: JackieZhai
- Problem ID: [POJ2411](http://poj.org/problem?id=2411)

## Description modeling

- 铺砖问题，比较经典
- 大白上题的弱化版

## Points in solving

- 状态压缩dp

## Warnings

- 注意不用ll会WA！

```c++
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;

typedef long long ll;

int h, w;
ll ans[15][15];

ll dp[2][1<<15];

int main()
{
    for(int n=1; n<=11; n++)
    {
        for(int m=1; m<=11; m++)
        {
            memset(dp, 0, sizeof(dp));
            ll *crt=dp[0], *next=dp[1];
            crt[0]=1;
            for(int i=n-1; i>=0; i--)
            {
                for(int j=m-1; j>=0; j--)
                {
                    for(int used=0; used<1<<m; used++)
                    {
                        if((used>>j&1))
                        {
                            next[used]=crt[used&~(1<<j)];
                        }
                        else
                        {
                            ll res=0;
                            if(j+1<m && !(used>>(j+1)&1))
                            {
                                res+=crt[used | 1<<(j+1)];
                            }
                            if(i+1<n && true)
                            {
                                res+=crt[used | 1<<j];
                            }
                            next[used]=res;
                        }
                    }
                    swap(crt, next);
                }
            }
            ans[n][m]=crt[0];
        }
    }

    while(scanf("%d%d", &h, &w)!=EOF)
    {
        if(h==0 && w==0)
            break;
        printf("%lld\n", ans[h][w]);
    }

    return 0;
}
```
