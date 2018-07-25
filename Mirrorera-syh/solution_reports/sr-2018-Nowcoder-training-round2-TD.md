
# LETTers Solution Report

- Date: 25th July 2018
- Author: Mirrorera
- Problem ID: [TD](https://www.nowcoder.com/acm/contest/140/D)

## Description modeling
Greedy

## Points in solving
设最大收益为ANS，将数列划分为数个极大连续不下降子序列，设第i个子序列最大值-最小值为v[i]<br>
则ANS = \sum{v[i]}<br>

证明：
反证，假设[l_1,r_1]和[l_2,r_2]为两个相邻极大连续不下降区间，易知有l_2 < r_1,<br>
则若在l_1处和l_2处买入，在r_1和r_2处卖出，收益为v[r_1] - v[l_1] + v[r_2] - v[l_2] > v[r_2] - v[l_1],<br>
且[l_1,r_1]和[l_2,r_2]为极大连续不下降区间，所以对于[l_1,r_2]，max{v[l_1,r_2]} = v[r_1] - v[l_1] + v[r_2] - v[l_2],<br>
算法得证

## Warnings
None.
