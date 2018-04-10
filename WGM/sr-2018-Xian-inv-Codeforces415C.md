
# LETTers Solution Report

- Date: 10 April 2018
- Author: WGM
- Problem ID: [CodeForces - 415C](http://codeforces.com/problemset/problem/415/C)

## Description modeling

令第二对及之后数的gcd都是1，如果第一对是1即是最小总和，如果大于k就输出-1；否则就取第一对使总和为k；
对于n为1的情况要独立讨论，因为n1且k=0的情况是可以实现的。

## Points in solving

如果要求第一对的gcd是x，前两个数是x和2*x，后面的数依此加1即可保证gcd为1；
注意行末空格在哪个输出考虑；

## Warnings

distinct是“不同的”意思，所以要求数列中不能有重复的数
(因为这个吃了两次罚时)

