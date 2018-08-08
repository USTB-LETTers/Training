
# LETTers Solution Report

- Date: 8 August 2018
- Author: WGM
- Problem ID: [nowcoder - 143J](https://www.nowcoder.com/acm/contest/143/E)

## Description modeling

- 网络流。每个去年宿舍从所有今年宿舍中选择一个，并且每个今年宿舍只有一个能被选择，即源点到去年、今年到汇点都是1。
- 最小费用，每条路径费用就是两个宿舍不同人数的个数，map记录再搜一下即可，数据规模很小。

## Points in solving

网络流抄板子，舒服=v=

## Warnings

关键还是建图思路。

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
} edge[MAXM];
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
    int n,a,b[5],count;
    map<int,int> m[MAXN];
    scanf("%d",&n);
    init(2*n+2);

    for(int i=1; i<=n; ++i)
    {
        m[i].clear();
        for(int j=1; j<=4; ++j)
        {
            scanf("%d",&a);
            ++m[i][a];
        }
        addedge(0,i,1,0);
    }
    for(int i=1; i<=n; ++i)
    {
        addedge(n+i,2*n+1,1,0);
        for(int j=1; j<=4; ++j)
            scanf("%d",&b[j]);
        for(int j=1; j<=n; ++j)
        {
            count = 0;
            for(int k=1; k<=4; ++k)
                if(!m[j].count(b[k]))
                    ++count;
            addedge(j,n+i,1,count);
        }
    }

    int ans;
    minCostMaxflow(0,2*n+1,ans);
    printf("%d\n",ans);

    return 0;
}


```
