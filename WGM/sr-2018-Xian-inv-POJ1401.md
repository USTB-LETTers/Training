
# LETTers Solution Report

- Date: 14 April 2018
- Author: WGM
- Problem ID: [POJ - 1401](http://poj.org/problem?id=1401)

## Description modeling

末尾多少个0 也就是前面的因数有多少个2和5；
很重要的一点是 2的个数一定比5的个数要多 所以只要求5的个数

含因数5的数字有5 10 15 20 25 30 35 ……
很明显这些数有n/5个
但是25 50 75……中有两个因数5 所以还要求含因数25的数有多少个
根据上面的思路 有n/25个 正好就把25倍数里多出来的5算上了
以此类推 可以想到n/125 n/725……

## Points in solving

预先记一下5的次幂 12次幂就够了 估计不准多取几个也行
然后各次幂整除n求和即可

## Warnings

无
