
# LETTers Solution Report

- Date: 19 April 2018
- Author: WGM
- Problem ID: [Codeforces - 469C](http://codeforces.com/problemset/problem/469/C)

## Description modeling

数列是1到n所有的数 很明显越大的数越难处理
那想办法前几个数凑出24 后面的数都两两相减变成1
比较好想到的是1 2 3 4凑出24 所以n是偶数情况有解了

## Points in solving

对于奇数情况 可以想到1 2 3 4中其实不需要1也能乘出24 想办法把1和后面想减剩下的数处理一下
既然大的数难处理 就把5拿出来 后面剩下的数就是偶数个了
但是1和5也不好处理 
仔细一想 其实是要处理1 2 3 4 5凑出24
显然 可以

## Warnings

检查格式
