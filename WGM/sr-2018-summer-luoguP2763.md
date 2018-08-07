
# LETTers Solution Report

- Date: 7 August 2018
- Author: WGM
- Problem ID: [luogu - P2763](https://www.luogu.org/problemnew/show/P2763)

## Description modeling

- 网络流经典二十四题之一
- 也是个可以用二分图构造的题。当成最大流练手。但是思考过程更复杂一点。

## Points in solving

把试卷对题型的要求转换成路径容量，最大流一定要使这几个路径全满，否则无解。

## Warnings

记录过程用vector数组，实现长度可变

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

const int MAXN = 1020 + 10;
const int INF = 0x3f3f;
int d[MAXN][MAXN],p[MAXN][MAXN],pre[MAXN];
bool vis[MAXN];
int n,k,t;

bool find()
{
    queue<int> q;
    while(!q.empty())
        q.pop();
    memset(vis,0,sizeof(vis));
    memset(pre,0,sizeof(pre));

    q.push(0);
    vis[0] = 1;
    while(!q.empty())
    {
        int now;
        now = q.front();
        q.pop();
        vis[now] = 1;
        for(int i=1; i<=t; ++i)
            if(!vis[i] && p[now][i] > 0)
            {
                vis[i] = 1;
                pre[i] = now;
                if(i != t)
                    q.push(i);
                else
                {
                    int minflow = INF;
                    for(int i=t; i!=0; i=pre[i])
                        if(minflow > p[ pre[i] ][i])
                            minflow = p[ pre[i] ][i];
                    for(int i=t; i!=0; i=pre[i])
                    {
                        p[ pre[i] ][i] -= minflow;
                        p[i][ pre[i] ] += minflow;
                        d[ pre[i] ][i] += minflow;
                        d[i][ pre[i] ] -= minflow;
                    }
                    return true;
                }
            }
    }
    return false;
}

int main()
{
    memset(p,0,sizeof(p));
    memset(d,0,sizeof(d));

    scanf("%d %d",&k,&n);
    t = n+k+1;
    int sum1 = 0;
    for(int i=n+1; i<=n+k; ++i)
    {
        scanf("%d",&p[i][t]);
        sum1 += p[i][t];
    }

    for(int i=1; i<=n; ++i)
    {
        p[0][i] = 1;
        int sp,a;
        scanf("%d",&sp);
        while(sp--)
        {
            scanf("%d",&a);
            p[i][n+a] = 1; 
        }
    }

    while(find());

    int sum2 = 0;
    for(int i=n+1; i<t; ++i)
        sum2 += d[i][t];
    if(sum1 != sum2)
        printf("No Solution!\n");
    else
    {
        vector<int> ans[50];
        for(int i=1; i<=k; ++i)
            ans[i].clear();

        for(int i=1; i<=n; ++i)
            for(int j=n+1; j<t; ++j)
                if(d[i][j] > 0)
                {
                    ans[j-n].push_back(i);
                    break;
                }

        for(int i=1; i<=k; ++i)
        {
            printf("%d:",i);
            for(unsigned int j=0; j<ans[i].size(); ++j)
                printf(" %d",ans[i][j]);
            printf("\n");
        }
    }

    return 0;
}

```
