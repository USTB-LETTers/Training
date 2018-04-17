
# LETTers Solution Report

- Date: 17 April 2018
- Author: WGM
- Problem ID: [CodeForces - 441B](http://codeforces.com/problemset/problem/441/B)

## Description modeling

很浅显的贪心
每次选择以当天结束的水果 
不满足每天最大值的情况下再选择以当天开始的水果 并把下一天结束的水果减去(因为当天选择了的 后一天就不能选了)

## Points in solving

不用区分水果树 直接两个数组分别记录以这天开始和结束的水果树
跑一边即可

## Warnings

记录最后一棵水果树什么时候可以收获(最大时间)
