
# LETTers Solution Report

- Date: 14 April 2018
- Author: WGM
- Problem ID: [CodeForces - 552D](http://codeforces.com/problemset/problem/552/D)

## Description modeling

想不到有什么别的方法 因为判断三点是否共线没有可优化的地方 必须要遍历到所有点
即使用组合数 也是要全部遍历 和一边遍历一边计数复杂度一样
4s的题可以尝试下暴力
(可能这个限时也是暗示可以暴力吧)

## Points in solving

向量叉乘判断共线
或者用斜率 写成乘法的形式

## Warnings

不要用Clang 会超时(编译快 跑得慢)

