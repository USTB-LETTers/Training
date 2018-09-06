# LETTers Solution Report

- Date: 6 September 2018
- Author: WGM
- Problem ID: [CodeForces - 569B](http://codeforces.com/problemset/problem/569/B)

## Description modeling

- 输入n和n个数，要把这些数重新编号，使新编号为1到n（也就是没有重复的编号），输出改变编号个数最短的方案。
- 拿个数组记哪个数没用过，因为不用考虑顺序，直接模拟一下就行。

## Points in solving

WA在了原来编号可能大于n的情况，虽然样例里有，但是不应该只记录这个数有没有出现，也要判断是不是大于n。

## Warnings

无
