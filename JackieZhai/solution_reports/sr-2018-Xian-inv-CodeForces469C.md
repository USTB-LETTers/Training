# LETTers Solution Report

- Date: 14 April 2018
- Author: JackieZhai
- Problem ID: [CodeForces469C](http://codeforces.com/problemset/problem/469/C)

## Description modeling

- 题目玩的是一个24点游戏
- 只不过有点不同的是会将“a+b”、“a-b”、“a*b”中的一个加入数组
- 问什么时候可以组成24点

## Points in solving

- 从小数枚举，很快就可以找到规律：
    1. 发现n小于4的时候死也组不成24
    2. n=4的时候可以组成24，且只要是偶数，4以后两两组成一组相减为1，全都在24的基础上乘1就行了
    3. n=5的时候可以组成24，且只要是奇数都可以，跟上面同理

## Warnings

- 无