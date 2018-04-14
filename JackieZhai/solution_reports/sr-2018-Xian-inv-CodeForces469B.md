# LETTers Solution Report

- Date: 14 April 2018
- Author: JackieZhai
- Problem ID: [CodeForces469B](http://codeforces.com/problemset/problem/469/B)

## Description modeling

- 题目问的是当t变化时，两组区间[ai, bi]和[ci+t, di+t]什么时候有重合
- 判断重合只需满足`x1<=y2 && y1>=x2`

## Points in solving

- 由于题目给的条件是`1 ≤ p, q ≤ 50; 0 ≤ l ≤ r ≤ 1000`，所以不要想得太复杂，直接暴力即可

## Warnings

- 无