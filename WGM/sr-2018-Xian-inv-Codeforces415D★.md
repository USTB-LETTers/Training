
# LETTers Solution Report

- Date: 7 April 2018
- Author: WGM
- Problem ID: [Codeforces - 415D](http://codeforces.com/problemset/problem/415/D)

## Description modeling

很容易想到dp：
d[i][j]表示长度为i，结尾数字为j的数列种类数
对t=1 to n 如果j整除t，则d[i][j] += d[i-1][t]

最终答案是d[k][1] + d[k][2]+d[k][3] + …… + d[k][n]

## Points in solving

以上算法复杂度为(k n²)，明显会超
这里关于能否整除的判断，我想到了筛法素数打表
不用逐个考虑能否整除，而是把除法换成乘法：
d[i+1][j*1] += d[i][j];
d[i+1][j*2] += d[i][j];
d[i+1][j*3] += d[i][j];
……
d[i+1][j*t] += d[i][j];
显然终止条件是j*t ≤ k；
复杂度近似为(k n logn)

## Warnings

DP的关键除了状态转移方程，还要考虑约束条件
