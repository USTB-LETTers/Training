
# LETTers Solution Report

- Date: 8 April 2018
- Author: Mirrorera
- Problem ID: [POJ3233](https://vjudge.net/contest/222750#problem/F)

## Description modeling

矩阵快速幂

## Points in solving

为了计算$f(K) = \sum_i^K A^i$，可以计算f(k) = f(k / 2) + A^{k / 2} f(k / 2)，就可以二分法解决，矩阵的幂可以使用快速幂

## Warnings

[PlaceHolder]
