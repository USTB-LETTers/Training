# LETTers Solution Report

- Date: 5 April 2018
- Author: Alice_Margatroid
- Problem ID: [HDU - 1722 ](https://vjudge.net/contest/220479#problem/A)

## Description modeling

题意：给一块蛋糕，有可能有p或q个人来吃，问最少要把蛋糕分成几块

样例：
input
2 3

output
4

也就是说，首先要把蛋糕分成至少q块（p>q）,然后再考虑p的情况。

首先，题目的要求是以圆心为中心将蛋糕切成若干个扇形。

经过分析，可以得出结论：如果已经分成了q块，而p,q互质，那么p块蛋糕的每一条边（除了第一条）一定不会和q块蛋糕的任何一条边重叠。

而每一条边对应着一块蛋糕。

此时，应该分成的块数，为p+q-1。

而再考虑p,q不互质的情况：那么此时，必定每过GCD（p,q）块，就会有一条边重合。

于是，总的块数就是p和q除以最大公约数之后，计算p'+q'-1再乘回去。

## Points in solving

要注意最大公约数的求法。本题数据不大，所以一般的方法就足够了。


## Warnings

暂无。
