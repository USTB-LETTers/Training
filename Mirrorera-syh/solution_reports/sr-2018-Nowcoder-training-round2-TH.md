
# LETTers Solution Report

- Date: 25th July 2018
- Author: Mirrorera
- Problem ID: [TH](https://www.nowcoder.com/acm/contest/140/H)

## Description modeling
树型dp

## Points in solving
以dp[i][j]表示以节点i为根节点的子树含有j / 2个链，且当j % 2 == 1时有向上链条，<br>
此时的最大值
则dp[i][j] = mmax{dp[son[i][a]][k] + dp[son[i][b]][j - k]}

## Warnings
None.
