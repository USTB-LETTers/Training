# LETTers Solution Report

- Date: 10 April 2018
- Author: JackieZhai
- Problem ID: [HDU4856](http://acm.hdu.edu.cn/showproblem.php?pid=4856)

## Description modeling

- 给你一张n*n的图，其中"."为可走，”#"为不可走，再给你m条通道的入口和出口（代表单向）
- 通道直接穿过不需要时间，点可到相邻的点，花费1个单位时间
- 问你以任意个通道入口为起点，走完所有通道而且每个通道只走一次，最少需要多少时间。

## Points in solving

- 这题相当于裸的**旅行商**问题，只需要bfs预处理每个通道的出口到其他通道的入口的最短距离，然后状压dp搞定

## Warnings

- 无

### Method 1
```c++
#include <bits/stdc++.h>
using namespace std;

const int inf=0x3f3f3f3f;
const int f[4][2]={1, 0, -1, 0, 0, 1, 0, -1};
char ma[20][20];
int n, m;
struct node
{
    int x1, y1;
    int x2, y2;
}a[20];//保存m个通道的入口和出口坐标
struct Node
{
    int x,y,dis;
};
int b[20][20][20][20];//存的是一个通道的出口到其他通道的入口的最短距离，前两维表示出口坐标，后两维表示入口坐标
int ex, ey;
bool vis[20][20];
int dp[33000][20];

int bfs(int sx,int sy)
{
    memset(vis, false, sizeof(vis));
    queue<Node> q;
    Node st,en;
    st.x=sx, st.y=sy, st.dis=0;
    q.push(st);
    vis[sx][sy]=true;
    while(q.size())
    {
        st=q.front();
        q.pop();
        if(st.x==ex && st.y==ey) return st.dis;
        for(int i=0; i<4; i++)
        {
            int mx=st.x+f[i][0];
            int my=st.y+f[i][1];
            if(mx<1||mx>n||my<1||my>n||vis[mx][my]||ma[mx][my]=='#') continue;
            vis[mx][my]=true;
            en.x=mx,en.y=my;
            en.dis=st.dis+1;
            q.push(en);
        }
    }
    return inf;
}

int main()
{
    while(scanf("%d%d",&n,&m)!=EOF)
    {
        for(int i=1; i<=n; i++)
            scanf("%s",ma[i]+1);
        for(int i=0; i<m; i++)
            scanf("%d%d%d%d",&a[i].x1,&a[i].y1,&a[i].x2,&a[i].y2);
        memset(b,inf,sizeof(b));
        for(int i=0; i<m; i++)//预处理出口到其他入口之间的最短距离
        {
            for(int j=0; j<m; j++)
            {
                if(i==j) continue;
                ex=a[j].x1,ey=a[j].y1;
                int d=bfs(a[i].x2,a[i].y2);
                b[a[i].x2][a[i].y2][a[j].x1][a[j].y1]=d;
            }
        }
        int N=1<<m;
        for(int i=0; i<N; i++)
            for(int j=0; j<m; j++)
            dp[i][j]=inf;
        for(int i=0; i<m; i++)
            dp[(1<<i)][i]=0;
        int ans=inf;
        for(int i=1; i<N; i++)
        {
            int flog=1;
            for(int j=0; j<m; j++)
            {
                if(!(i&(1<<j)))
                {
                    flog=0;
                    continue;
                }
                for(int k=0; k<m; k++)
                {
                    if(!(i&(1<<k))||j==k) continue;
                    dp[i][j]=min(dp[i][j],dp[i^(1<<j)][k]+b[a[k].x2][a[k].y2][a[j].x1][a[j].y1]);
                }
            }
            if(flog)
            {
                for(int j=0;j<m;j++)
                    ans=min(ans,dp[i][j]);
            }
        }
        if(ans==inf)
            puts("-1");
        else
            printf("%d\n",ans);
    }
    return 0;
}
```

### Method 2
*强行把每一个格点作为结点Dijkstra了一下，但是WA，不知道哪里错了……<br>
日后再研究研究吧*
```c++
#include <bits/stdc++.h>
using namespace std;

const int MAX_V=307, MAX_N=27, INF=0x3f3f3f3f;

char maze[MAX_N][MAX_N];
int x1[MAX_N], y1[MAX_N];
int x2[MAX_N], y2[MAX_N];
int N, M;
int V;
int cost[MAX_V][MAX_V];
int d[MAX_N][MAX_V];
int de[MAX_N][MAX_V];
bool used[MAX_V];
int ans=INF;

void dijkstra(int s, int m)
{
    fill(d[m], d[m]+V, INF);
    fill(used, used+V, false);
    d[m][s]=0;

    while(true)
    {
        int v=-1;
        for(int u=0; u<V; u++)
        {
            if(!used[u] && (v==-1 || d[m][u]<d[m][v]))
                v=u;
        }

        if(v==-1)
            break;
        used[v]=true;
        for(int u=0; u<V; u++)
        {
            d[m][u]=min(d[m][u], d[m][v]+cost[v][u]);
        }
    }
}

void dijkstra2(int s, int m)
{
    fill(de[m], de[m]+V, INF);
    fill(used, used+V, false);
    de[m][s]=0;

    while(true)
    {
        int v=-1;
        for(int u=0; u<V; u++)
        {
            if(!used[u] && (v==-1 || de[m][u]<de[m][v]))
                v=u;
        }

        if(v==-1)
            break;
        used[v]=true;
        for(int u=0; u<V; u++)
        {
            de[m][u]=min(de[m][u], de[m][v]+cost[v][u]);
        }
    }
}

bool vis[MAX_N];
void dfs(int m, int sum, int c)
{
    vis[m]=true;

//    for(int i=0; i<M; i++)
//            printf("%d ", vis[i]);
//        printf("\n");
//    printf("c = %d\n", c);
//    printf("$ %d\n", sum);
    if(c==M-1)
    {
//        printf("$$ %d\n", sum);

        ans=min(ans, sum);
        return ;
    }

    for(int i=0; i<M; i++)
    {
        if(i!=m && !vis[i])
        {
            sum+=de[m][x1[i]*N+y1[i]];
            dfs(i, sum, c+1);
            vis[i]=false;
            sum-=de[m][x1[i]*N+y1[i]];
        }
    }
}


int main()
{
    scanf("%d%d", &N, &M);
    V=N*N;
    getchar();
    for(int i=0; i<N; i++)
    {
        scanf("%s", &maze[i]);
        //reverse(maze[i], maze[i]+N);
    }
    reverse(maze, maze+N);


    for(int i=0; i<N*N; i++)
        for(int j=0; j<N*N; j++)
            cost[i][j]=INF;

    for(int i=0; i<N; i++)
        for(int j=0; j<N; j++)
        {
            if(maze[i][j]=='.')
            {
                if(!(i+1<N))
                {
                    if(j+1<N) if(maze[i][j+1]!='#')
                        cost[i*N+j][(i)*N+(j+1)]=1;
                    if(j-1>=0) if(maze[i][j-1]!='#')
                        cost[i*N+j][(i)*N+(j-1)]=1;
                    if(maze[i-1][j]!='#')
                    cost[i*N+j][(i-1)*N+(j)]=1;
                }
                else if(!(i-1>=0))
                {
                    if(j+1<N) if(maze[i][j+1]!='#')
                        cost[i*N+j][(i)*N+(j+1)]=1;
                    if(j-1>=0) if(maze[i][j-1]!='#')
                        cost[i*N+j][(i)*N+(j-1)]=1;
                    if(maze[i+1][j]!='#')
                    cost[i*N+j][(i+1)*N+(j)]=1;
                }
                else
                {
                    if(j+1<N) if(maze[i][j+1]!='#')
                        cost[i*N+j][(i)*N+(j+1)]=1;
                    if(j-1>=0) if(maze[i][j-1]!='#')
                        cost[i*N+j][(i)*N+(j-1)]=1;
                    if(maze[i+1][j]!='#')
                    cost[i*N+j][(i+1)*N+(j)]=1;
                    if(maze[i-1][j]!='#')
                    cost[i*N+j][(i-1)*N+(j)]=1;
                }
            }
        }
    for(int i=0; i<M; i++)
    {
        scanf("%d%d%d%d", &x1[i], &y1[i], &x2[i], &y2[i]);
        x1[i]--, x2[i]--, y1[i]--, y2[i]--;
        int buf=cost[x1[i]*N+y1[i]][x2[i]*N+y2[i]];
        cost[x1[i]*N+y1[i]][x2[i]*N+y2[i]]=0;

        dijkstra(x1[i]*N+y1[i], i);
        dijkstra2(x2[i]*N+y2[i], i);
        d[i][x1[i]*N+y1[i]]=de[i][x1[i]*N+y1[i]];

        cost[x1[i]*N+y1[i]][x2[i]*N+y2[i]]=buf;

//        //PRINT
//        printf("-d-\n");
//        for(int k=0; k<N; k++)
//        {
//            for(int j=0; j<N; j++)
//                printf("%d ", de[i][k*N+j]);
//            printf("\n");
//        }
//        printf("---\n");
//        //PRINT
    }

    for(int i=0; i<M;  i++)
    {
        fill(vis, vis+M, false);
        dfs(i, 0, 0);
    }
    printf("%d\n", ans);

    return 0;
}
```
