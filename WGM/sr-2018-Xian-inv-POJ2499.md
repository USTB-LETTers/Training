
# LETTers Solution Report

- Date: 17 April 2018
- Author: WGM
- Problem ID: [POJ - 2499](http://poj.org/problem?id=2499)

## Description modeling

如果目标点的上一个点是(a,b) 那么目标点要么是(a,a+b) 要么是(a+b,b)
可以比较两个值的大小来转移到上一个点 并得到(a,b)的值

## Points in solving

考虑时间优化 因为只有左右两个方向
所以考虑从(a+b+b+b+b+b,b)直接转移到(a,b)
也就是整除得到的数是步数 取余得到的是新的(a,b)

## Warnings

特别考虑余数为0的情况
因为不能从(b+b,b)转移到(0,b) 而是应该到(b,b)

