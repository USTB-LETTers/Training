
# LETTers Solution Report

- Date: 25th July 2018
- Author: Mirrorera
- Problem ID: [TA](https://www.nowcoder.com/acm/contest/140/A)

## Description modeling
linear dp

## Points in solving

\begin{cases}
dp[i][0] = dp[i - 1][0] + dp[i - 1][1]<br>
dp[i][1] = dp[i - k][0]
\end{cases}

## Warnings
None.
