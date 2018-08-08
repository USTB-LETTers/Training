
# LETTers Solution Report

- Date: 8 August 2018
- Author: WGM
- Problem ID: [luogu - P4015](https://www.luogu.org/problemnew/show/P4015)

## Description modeling

- 网络流经典二十四题之一
- 最小费用最大流练手题，主要思路就是在最大流的过程中，考虑增广路时选择费用最小的一条。
- 最短路算法，最好不要用dijkstra，因为可能有负权。本题中的最大费用就是用相反数处理。

## Points in solving

练了下板子，主要是熟悉邻接表。本题中也要注意初始化和记录输入数据的细节。

## Warnings

初始化函数要做到完全清空，对二次运行不产生影响。

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

const int MAXN = 200 + 10;
const int MAXM = 40000 + 10;
const int INF = 0x3f3f3f3f;

struct Edge
{
    int to,next,cap,flow,cost;
}edge[MAXM];
int head[MAXN],tol;
int pre[MAXN],dis[MAXN];
bool vis[MAXN];
int N;

void init(int n)
{
    N = n;
    tol = 0;
    memset(head,-1,sizeof(head));
}

void addedge(int u,int v,int cap,int cost)
{
    edge[tol].to = v;
    edge[tol].cap = cap;
    edge[tol].cost = cost;
    edge[tol].flow = 0;
    edge[tol].next = head[u];
    head[u] = tol++;
    edge[tol].to = u;
    edge[tol].cap = 0;
    edge[tol].cost = -cost;
    edge[tol].flow = 0;
    edge[tol].next = head[v];
    head[v] = tol++;
}

bool spfa(int s,int t)
{
    queue<int> q;
    for(int i = 0; i < N; i++)
    {
        dis[i] = INF;
        vis[i] = false;
        pre[i] = -1;
    }
    dis[s] = 0;
    vis[s] = true;
    q.push(s);
    while(!q.empty())
    {
        int u = q.front();
        q.pop();
        vis[u] = false;
        for(int i = head[u]; i != -1; i = edge[i].next)
        {
            int v = edge[i].to;
            if(edge[i].cap > edge[i].flow &&
                    dis[v] > dis[u] + edge[i].cost)
            {
                dis[v] = dis[u] + edge[i].cost;
                pre[v] = i;
                if(!vis[v])
                {
                    vis[v] = true;
                    q.push(v);
                }
            }
        }
    }
    
    if(pre[t] == -1)
        return false;
    else 
        return true;
}

int minCostMaxflow(int s,int t,int &cost)
{
    int flow = 0;
    cost = 0;
    while(spfa(s,t))
    {
        int Min = INF;
        for(int i = pre[t]; i != -1; i = pre[edge[i^1].to])
        {
            if(Min > edge[i].cap - edge[i].flow)
                Min = edge[i].cap - edge[i].flow;
        }
        for(int i = pre[t]; i != -1; i = pre[edge[i^1].to])
        {
            edge[i].flow += Min;
            edge[i^1].flow -= Min;
            cost += edge[i].cost * Min;
        }
        flow += Min;
    }
    return flow;
}

int main()
{
    int m,n;
    scanf("%d %d",&m,&n);
    int a[m+n+1],b[n*m+1];
    
    init(m+n+2);
    for(int i=1; i<=m; ++i)
    {
        scanf("%d",&a[i]);
        addedge(0,i,a[i],0);
    }
    for(int i=m+1; i<=m+n; ++i)
    {
        scanf("%d",&a[i]);
        addedge(i,n+m+1,a[i],0);
    }
    for(int i=1; i<=m; ++i)
        for(int j=1; j<=n; ++j)
        {
            scanf("%d",&b[(i-1)*n+j]);
            addedge(i,m+j,INF,b[(i-1)*n+j]);
        }
    
    int ans1;
    minCostMaxflow(0,n+m+1,ans1);
    printf("%d\n",ans1);
    
    init(m+n+2);
    for(int i=1; i<=m; ++i)
        addedge(0,i,a[i],0);
    for(int i=m+1; i<=m+n; ++i)
        addedge(i,n+m+1,a[i],0);
    for(int i=1; i<=m; ++i)
        for(int j=1; j<=n; ++j)
            addedge(i,m+j,INF,-b[(i-1)*n+j]);
    
    int ans2;
    minCostMaxflow(0,n+m+1,ans2);
    printf("%d\n",-ans2);

    return 0;
}


```
