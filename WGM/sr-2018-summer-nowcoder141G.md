
# LETTers Solution Report

- Date: 1 August 2018
- Author: WGM
- Problem ID: [nowcoder - 141G](https://www.nowcoder.com/acm/contest/141/G)

## Description modeling

- 价值为d的方案数 = 价值大于等于d的方案数 - 价值大于等于d+1的方案数;
- 价值大于等于d，需要保证与当前节点距离小于d的点没有相同颜色。当前节点会使所有距离小于d的节点的方案数少1，总方案数为所有节点方案数相乘。
- 重复问题，通过方向解决，只要保证始终往后算，即i使i后面的节点减1，而不影响i前面的节点，就能保证没有重复——bfs层次遍历

## Points in solving

难点是多叉树，有些地方的处理和二叉树不一样。
- 建树用vector数组，方便处理一个节点的多个孩子。根节点随意选，关键是如何判断众多孩子中哪个实际是父亲，不向这个方向搜索。
- 距离通过dfs求。虽然是无向的，应该要记录dis[i][j]和dis[j][i]，但由于搜索是从上往下的，所以可以只跑父亲到孩子的距离，为了区分父亲，把当前节点中的父亲节点记为递归参数。
- bfs用vis数组判断是否访问，保证向下求值。

## Warnings

- 优化1：二维数组dis的初始化，其实只需要在起点时初始化d[i][i]为0即可，后面节点为父亲加1.可以优化一个二维数组memset的时间。
- 优化2：其实bfs是边搜索边求值的，也就是说已经遍历过的点不用再考虑，所以不需要vis数组，前面的节点已经被运算了，即使更改了前面节点的值，也不会对总方案数产生影响。

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

const int MAXN = 5000 + 10;
const int MOD = 1e9 + 7;
vector<int> p[MAXN];
int vis[MAXN],dis[MAXN][MAXN],c[MAXN],n,K,D;

void dfs(int now,int son,int fa)
{
    for(int i=0; i<p[son].size(); ++i)
        if(p[son][i] != fa)
        {
            dis[now][ p[son][i] ] = dis[now][son] + 1;
            dfs(now,p[son][i],son);
        }

    return;
}

long long bfs(int d)
{
    long long ans=1;
    queue<int> Q;
    Q.push(1);
    for(int i=1; i<=n; ++i)
        c[i] = K;
    memset(vis,0,sizeof(vis));

    while(!Q.empty())
    {
        int now = Q.front();
        Q.pop();
        ans *= c[now];
        ans %= MOD;
        vis[now] = 1;
        //printf("now=%d c=%d ans=%d \n",now,c[now],ans);

        for(int i=1; i<=n; ++i)
        {
            if(dis[now][i] >= d || i == now || vis[i] == 1)
                continue;
            c[i]--;
            if(c[i] == 0)    //剪枝
                return 0;
        }

        for(int i=0; i<p[now].size(); ++i)
            if(vis[ p[now][i] ] == 0)
                Q.push(p[now][i]);
    }

    return ans;
}

int main()
{
    int a,b;
    scanf("%d %d %d",&n,&K,&D);
    for(int i=1; i<=n-1; ++i)
    {
        scanf("%d %d",&a,&b);
        p[a].push_back(b);
        p[b].push_back(a);
    }

    for(int i=1; i<=n; ++i)
    {
        dis[i][i] = 0;
        vis[i] = 1;
        dfs(i,i,0);
    }

    long long ans1,ans2; 
    ans1 = bfs(D);
    ans2 = bfs(D+1);
    printf("%lld\n",(ans1 - ans2 + MOD) % MOD);

    return 0;
}


```
