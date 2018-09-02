
# LETTers Solution Report

- Date: 2nd Sep 2018
- Author: Mirrorera
- Problem ID:  **Nanjiing Online Contest** [E](https://nanti.jisuanke.com/t/30994)

## Description modeling

 - 给出一些点之间的依赖关系，每个点有权值 A 和 B ，定义收益为 A $\times$ T + B ，求最大收益

 - 保证点数 $N < 20$

## Points in solving

1. 若图中存在有向环，则其上的点全部不能被选，先进行一遍拓扑排序删除有向环

2. 删环之后，剩余图满足有向无环，可以考虑动态规划

3. 每次选点时依赖于已经被选的点集，所以考虑状态压缩，以被选点集作为状态

4. 得出方程,设 depend[i][j] 为点i所依赖的点,dep表示当前状态 1 的个数

    - $dp[state] = max\{\;dp[state | oper] + A[i] \cdot (dep + 1) + B[i])\;\} ,\; (1 << depend[i][j])\; \& \; state == true$

## Warnings

 - None.
