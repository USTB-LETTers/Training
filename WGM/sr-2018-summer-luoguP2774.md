
# LETTers Solution Report

- Date: 7 August 2018
- Author: WGM
- Problem ID: [luogu - P2763](https://www.luogu.org/problemnew/show/P2763)

## Description modeling

- 网络流经典二十四题之一，目的是最小割，通过最大流实现。
- 建图比较难，关键要想到黑白染色然后去除不符合规则的部分。

## Points in solving

更新了之前的一个小误区，最终答案可以通过每次的增广量累加得到。而之前错误认为每次更新路径，增广量对答案没有实际意义，但其实增广过程一定是使流增大的，即使之前的路径有所更新，但贡献仍然是对答案产生的。

## Warnings

仔细分析和思考建图过程。

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

const int MAXN = 1020 + 10;
const int INF = 0x3f3f3f3f;

int res[MAXN][MAXN],d[MAXN][MAXN],v[MAXN][MAXN],pre[MAXN],vis[MAXN];
int n,m,t,sum,maxflow;
int dre[4][2] = {0,1,0,-1, 1,0,-1,0};

bool find()
{
    memset(vis,0,sizeof(vis));
    memset(pre,0,sizeof(pre));
    queue<int> q;
    while(!q.empty())
        q.pop();

    q.push(0);
    while(!q.empty())
    {
        int now = q.front();
        q.pop();
        vis[now] = 1;

        for(int i=1; i<=t; ++i)
        {
            if(!vis[i] && res[now][i] > 0)
            {
                vis[i] = 1;
                pre[i] = now;
                q.push(i);

                if(i == t)
                {
                    int minflow = INF;
                    for(int j=t; j!=0; j=pre[j])
                        if(minflow > res[ pre[j] ][j])
                            minflow = res[ pre[j] ][j];
                    maxflow += minflow;
                    for(int j=t; j!=0; j=pre[j])
                    {
                        res[ pre[j] ][j] -= minflow;
                        res[j][ pre[j] ] += minflow;
                        d[ pre[j] ][j] += minflow;
                        d[j][ pre[j] ] -= minflow;
                    }
                    return true;
                }
            }
        }
    }

    return false;
}

int main()
{
    sum = 0;
    memset(d,0,sizeof(d));
    memset(res,0,sizeof(res));

    scanf("%d %d",&m,&n);
    t = n*m + 1;
    for(int i=1; i<=m; ++i)
        for(int j=1; j<=n; ++j)
        {
            scanf("%d",&v[i][j]);
            sum += v[i][j];
            int num = (i-1) * n + j;
            if((i+j) % 2)
                res[num][t] = v[i][j];
            else
                res[0][num] = v[i][j];
  
            for(int k=0; k<=3; ++k)
            {
                int xx = i + dre[k][0],yy = j + dre[k][1];
                if(1 <= xx && xx <= m && 1 <= yy && yy <= n)
                {
                    int numk = (xx-1) * n + yy;
                    if((i+j) % 2)
                        res[numk][num] = INF;
                    else
                        res[num][numk] = INF;
                }
            }
        }

    while(find());

    printf("%d\n",sum - maxflow);

    return 0;
}


```
