
# LETTers Solution Report

- Date: 25th July 2018
- Author: Mirrorera
- Problem ID: [TA](https://www.nowcoder.com/acm/contest/140/A)

## Description modeling
二分 or dp

## Points in solving
前提：
对于任一个位置，若最终将物品挪到此位置，应优先考虑较近的物品<br>

设dp[i][0]表示最终挪到i位置时i位置之前位置所贡献物品数，dp[i][1]表示最终挪到i位置时i位置之后位置所贡献的物品数
则首先令<br>
dp[i][0] = dp[i - 1][0] + num[i - 1]<br>
dp[i][1] = dp[i - 1][1] - num[i]<br>
此时cost[i] = cost[i - 1] + (dp[i - 1][0] + num[i - 1] - dp[i - 1][1] + num[i]) * dis(i,i - 1)<br>
此时，若cost[i] > T，则从已选区间头部逐渐减少物品<br>
若cost[i] < T，则从已选区间尾部逐渐增加物品<br>
这样增减的原因：
若cost[i] > T，则如果目前需要减少物品，而显然转移之前i - 1位置不必减少，<br>
导致当前cost过大的因素必然是递增项，也就是dp[i][0] = dp[i - 1][0] + num[i - 1]部分<br>
cost[i] < T 时同理可得
最终时间复杂度为O(N)
## Warnings
None.
