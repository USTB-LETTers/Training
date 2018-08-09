
# LETTers Solution Report

- Date: 9 August 2018
- Author: WGM
- Problem ID: [nowcoder - 145C](https://www.nowcoder.com/acm/contest/145/C)

## Description modeling

暴力，双向搜索(BFS+DFS)

## Points in solving

- 用二叉树存储，方便访问下标。
- 根据输入的字符串从上往下DFS，可以剪枝删掉全0的状态，因为全0经过任何操作都变不成1。
- 根据根节点为1从下往上BFS枚举所有合法条件。

## Warnings

只用DFS+剪枝+scanf读入，居然过了= =，所以以后遇到几亿复杂度的题可以试试暴力

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

const int MAXN = 2 << 20;

int tree[MAXN],ans;

void dfs(int n)
{
    if(n == 0)
    {
        if(tree[1] == 1)
            ++ans;
        return;
    }
    bool flag;

    flag = 0;
    for(int i=(1 << (n-1)); i<=(1 << n)-1; ++i)
    {
        tree[i] = tree[i*2] & tree[i*2+1];
        if(tree[i] == 1)
            flag = 1; 
    }
    if(flag)
        dfs(n-1);

    flag = 0;
    for(int i=(1 << (n-1)); i<=(1 << n)-1; ++i)
    {
        tree[i] = tree[i*2] | tree[i*2+1];
        if(tree[i] == 1)
            flag = 1; 
    }
    if(flag)
        dfs(n-1);

    flag = 0;
    for(int i=(1 << (n-1)); i<=(1 << n)-1; ++i)
    {
        tree[i] = tree[i*2] ^ tree[i*2+1];
        if(tree[i] == 1)
            flag = 1; 
    }
    if(flag)
        dfs(n-1);
}

int main()
{
    ans = 0;
    int n;
    char s[MAXN];
    scanf("%d%s",&n,s);
    
    for(int i=0; i<=(1 << n)-1; ++i)
        tree[i + (1 << n)] = s[i] - '0';

    dfs(n);

    printf("%d\n",ans);

    return 0;
}


```
