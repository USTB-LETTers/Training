
# LETTers Solution Report

- Date: 24 July 2018
- Author: WGM
- Problem ID: [nowcoder - 139D](https://www.nowcoder.com/acm/contest/139/D)

## Description modeling

G2子图中与G1同构的数量，重复的部分为G1自身同构的数量

有点类似于除序的思想："排列=组合\*顺序  ->  组合=排列/顺序", 因为自同构就是在确认已选出节点下的内部排序，而题目要求的不重复则只是节点的“组合”。

## Points in solving

- 同构算法：G1作为目标，cast数组作为映射函数，尝试所有的映射函数（next_permutation），要在G2内可以通过映射函数找到所以G1内的边。
- 对于m1≠m2，可能会考虑到映射集合的选择，但实际上可以想象成补空节点使两图节点数相同，不影响结果。

## Warnings

不是要求G2内所有边通过映射函数都在G1内，只需要G2的**子图**，大小关系应该是G2>=G1，所以判断条件是!G2[cast[i]][cast[j]] && G1[i][j]，而不是G2[cast[i]][cast[j]] == G1[i][j]

## Codes

```c++

#include <bits/stdc++.h>
using namespace std;

const int MAXN = 15;

int cast[MAXN] = {0, 1, 2, 3, 4, 5, 6, 7, 8};

int TongGou(int n,int G1[MAXN][MAXN],int G2[MAXN][MAXN])
{
    int ANS = 0;
    do
    {
        bool flag = true;
        for (int i = 0; i < n; ++i)
        {
            for (int j = 0; j < n; ++j)
            {
                if (!G2[cast[i]][cast[j]] && G1[i][j])
                {
                    flag = false;
                    break;
                }
            }
            if (!flag)
                break;
        }

        if (flag)
            ++ANS;
    } while (next_permutation(cast, cast + n));
    
    return ANS;
}

int M1,M2,N;
int gragh1[MAXN][MAXN], gragh2[MAXN][MAXN];
int vis[MAXN],now;
int main()
{
    while (cin >> N >> M1 >> M2)
    {
        memset(gragh1,0,sizeof(gragh1));
        memset(gragh2,0,sizeof(gragh2));

        for (int i = 0; i < M1; ++i)
        {
            int a, b;
            cin >> a >> b;
            --a;--b;
            gragh1[a][b] = gragh1[b][a] = 1;
        }
        for (int i = 0; i < M2; ++i)
        {
            int a, b;
            cin >> a >> b;
            --a;--b;
            gragh2[a][b] = gragh2[b][a] = 1;
        }
        
        cout << TongGou(N,gragh1,gragh2) / TongGou(N,gragh1,gragh1) << endl;
    }
    return 0;
}

```
