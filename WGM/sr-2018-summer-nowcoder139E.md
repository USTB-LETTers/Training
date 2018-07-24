
# LETTers Solution Report

- Date: 24 July 2018
- Author: WGM
- Problem ID: [nowcoder - 139E](https://www.nowcoder.com/acm/contest/139/E)

## Description modeling

- 与简单DP相比，不好处理的是删了不同位置的相同元素，导致子序列重复。
    
    值得注意的是，本题中k≤10，也就是说元素的种类很少，必然会有很多重复的。那么对于当前位置后面的多个x，只需要转移到最近的一个即可。
- 预处理，记录第i个元素后面第一个0的位置next[i][0]、后面第一个1的位置next[i][1]等等。而转移的过程就是删除中间所有元素。
- d[i][j]表示当前位置i，已经删除j个，转移到d[next[i][k]][j+next[i][k]-i]（k取遍所有种类元素）

## Points in solving



## Warnings



## Codes

```c++

```
