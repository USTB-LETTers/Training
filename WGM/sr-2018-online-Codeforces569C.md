# LETTers Solution Report

- Date: 6 September 2018
- Author: WGM
- Problem ID: [CodeForces - 569C](http://codeforces.com/problemset/problem/569/C)

## Description modeling

- pi(n)表示小于等于n的数中质数的数量，rub(n)表示小于等于n的数中回文数的数量。输入p和q，输出满足pi(n)≤(p/q)*rub(n)。
- 先打个表看看数据规模，再判断要不要优化。质数明显比回文数多，42倍的话到1e7就够了，可以直接做。
- 关于回文数打表，比较容易想到的是把i翻转再拼上，可以得到偶数长度的回文数；再把i最后一位去掉的翻转拼上原本的i，可以得到奇数长度的回文数，并且没有重复。1e7的话i最多1e4也就够了。

## Points in solving

- 打表注意严格约束上限。
- 翻转不如直接用while读各位，用log/log10有些地方会出错。

## Warnings

- 虽然p/q只有42，但是最大q会有1e4，而q*pi(n)≤p*rub(n)中pi(n)最多大概会有6e5，不等式左边会爆int。
- cf的题总是会在奇怪的地方爆int
