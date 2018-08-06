
# LETTers Solution Report

- Date: 6 August 2018
- Author: WGM
- Problem ID: [luogu - P2756](https://www.luogu.org/problemnew/show/P2756)

## Description modeling

- 网络流经典二十四题之一
- 二分图匹配模板题，作为一个简单的最大流来练手，再忽略权值的情况下，注意一下整体实现结构和细节。

## Points in solving

- 要区分好实际网络和残余网络，并且保证同步更新。
- 这题用BFS其实更复杂，但主要是练手，所以没有考虑优化。

## Warnings

BFS要判节点是否访问，以及记录有效路径，在BFS结束更新。可以考虑单独写个更新函数。

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

const int MAXN = 100 + 10;
int d[MAXN][MAXN],p[MAXN][MAXN],pre[MAXN];
bool vis[MAXN];
int n,m;

bool find()
{
    queue<int> q;
    while(!q.empty())
        q.pop();
    memset(vis,0,sizeof(vis));
    memset(pre,0,sizeof(pre));
    vis[0] = 1;
    q.push(0);

    while(!q.empty())
    {
        int now;
        now = q.front();
        q.pop();

        for(int i=1; i<=n+1; ++i)
        {
            if(!vis[i] && p[now][i] > 0)
            {
                pre[i] = now;
                vis[i] = 1;
                q.push(i);

                if(i == n+1)
                {
                    int maxflow = 0;
                    for(int j=n+1; j!=0; j=pre[j])
                        if(p[ pre[j] ][j] > maxflow)
                            maxflow = p[ pre[j] ][j];
                    for(int j=n+1; j!=0; j=pre[j])
                    {
                        p[ pre[j] ][j] -= maxflow;
                        p[j][ pre[j] ] += maxflow;
                        d[ pre[j] ][j] += maxflow;
                        d[j][ pre[j] ] -= maxflow;
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
    scanf("%d %d",&m,&n);
    memset(d,0,sizeof(d));
    memset(p,0,sizeof(p));
    int a,b;
    while(scanf("%d %d",&a,&b),a != -1 && b != -1)
    {
        p[a][b] = 1;
        p[0][a] = 1;
        p[b][n+1] = 1;
    }

    while(find());

    int ans=0;
    for(int i=1; i<=m; ++i)
        ans += d[0][i];
    printf("%d\n",ans);
    for(int i=1; i<=m; ++i)
    {
        if(!d[0][i])
            continue;
        for(int j=m+1; j<=n; ++j)
            if(d[i][j])
            {
                printf("%d %d\n",i,j);
                break;
            }
    }

    return 0;
}


```
