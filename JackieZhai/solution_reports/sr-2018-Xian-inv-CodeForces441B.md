# LETTers Solution Report

- Date: 17 April 2018
- Author: JackieZhai
- Problem ID: [CodeForces441B](http://codeforces.com/problemset/problem/441/B)

## Description modeling

- 贪心题，每天只能收v个果实，每棵树只能在ai和ai+1天采摘

## Points in solving

- 建立两个数组即可，每天优先采摘之前一天没采摘完的就行

## Warnings

- 注意：没说不能在同一天成熟，所以数组应该是`coun[a]+=b;`，而决不能是`coun[a]=b;`