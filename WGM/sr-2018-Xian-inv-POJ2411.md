
# LETTers Solution Report

- Date: 14 April 2018
- Author: WGM
- Problem ID: [POJ2411](http://poj.org/problem?id=2411)

## Description modeling

对于第j行的每个格子：
  如果上一行位子的格子是空 那么这个格子必须竖放一块
  其余情况：
    如果不是最后一行 就可以选择不放(等下一行放竖直的)；
    如果能放得下横的 就可以选择放横的；

显然还需要状态压缩
对于已经放了方块的格子 不用管已经放的方块是什么状态(不用管是横的还是竖的)
只需要关心放了还是没放足矣 所以用二进制存每一行的状态

## Points in solving

因为最后一行的情况特殊(不能留空)
所以没法预处理打表 对每组输入单独计算

## Warnings

虽然最大是11 X 11  但情况总数是会爆int的
以及 除了程序前定义的变量 不要忘了在程序中间定义的变量也要换long long

