
# LETTers Solution Report

---
- Date: 10 April 2018
- Author: Mirrorera
- Problem ID: [POJ1990](https://vjudge.net/contest/221157#problem/I)

## Description modeling

美国人的题就是骚）
**题意:**  
给定N个二元组，两个数分别表示其在数轴上的位置和一个题设vol，
求$\sum_{(i,j)}^{i < j <= N} max(vol_i,vol_j)*|pos_i - pos_j| $

## Points in solving

如果暴力枚举所有点对，时间复杂度为$O(n^2)$，显然会t，所以我们需要更优的算法
首先，考虑$max(vol_i,vol_j)$部分，事实上，这部分运算可以通过改变处理顺序来解决。如果我们按照vol递减的顺序进行计算，那么每次就可以省略max的运算，直接用当前的vol乘以该点与其他所有点的距离之和。等等，所有点的距离之和？区间求和可以采用前缀和，这需要预处理，而$D_k = \sum_i d_i = \sum_i |x_i - x_k| \\
= -\sum_{i = 0}^{k - 1} x_i + \sum_{i = k + 1}^N x_i - (N - k)x_k +(k - 1)x_k$
经过前缀和优化之后
## Warnings

[PlaceHolder]

写题解的思路崩溃，先附代码为敬
```c++

#include <queue>
#include <vector>
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cstdio>

using namespace std;

typedef long long LL;

struct Bull
{
    int vol;
    int pos;
    bool operator<(const Bull &rhs) const
    {
        return pos < rhs.pos;
    }
};

struct Index
{
    int lab;
    int vol;
    Index() = default;
    Index(int a, int b) : lab(a), vol(b){};
    bool operator<(const Index &rhs) const
    {
        if (vol == rhs.vol)
            return lab < rhs.lab;
        return vol < rhs.vol;
    }
};

const int MAXN = 20000 + 233;

int N;

Bull data[MAXN];

priority_queue<Index, vector<Index> > Order;

int BitTree[MAXN];
int BitCount[MAXN];

LL ANS(0);

inline int lowbit(int n)
{
    return n & (-n);
}

inline void modify(int *d, int n, int inc)
{
    ++n;
    while (n <= N)
    {
        d[n - 1] += inc;
        n += lowbit(n);
    }
}

inline int query(int *d, int n)
{
    int ans(0);
    ++n;
    while (n)
    {
        ans += d[n - 1];
        n -= lowbit(n);
    }
    return ans;
}

int main()
{
    cin >> N;
    for (int i = 0; i < N; ++i)
        cin >> data[i].vol >> data[i].pos;
    sort(data, data + N);
    for (int i = 0; i < N; ++i)
        Order.push(Index(i, data[i].vol));
    for (int i = 0; i < N; ++i)
    {
        modify(BitTree, i, data[i].pos);
        modify(BitCount, i, 1);
    }
    while (!Order.empty())
    {
        Index oper = Order.top();
        Order.pop();
        LL possum(0);
        possum += query(BitTree, N - 1) - query(BitTree, oper.lab);
        possum -= query(BitTree, oper.lab - 1);
        modify(BitTree, oper.lab, -data[oper.lab].pos);
        possum += (query(BitCount, oper.lab - 1) - query(BitCount, N - 1) + query(BitCount, oper.lab)) * data[oper.lab].pos;
        modify(BitCount, oper.lab, -1);
        ANS += possum * data[oper.lab].vol;
    }
    cout << ANS << endl;
    return 0;
}
```
