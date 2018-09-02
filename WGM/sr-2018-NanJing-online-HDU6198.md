# LETTers Solution Report

- Date: 1 September 2018
- Author: WGM
- Problem ID: [HDU - 6198](http://acm.hdu.edu.cn/showproblem.php?pid=6198)

## Description modeling

- 定义了一种m-d数，即不能被拆成k项斐波那契数的和，可重复可包括0。输入k，输出最小的m-d数。
- 最小的不能拆成k项，也就是要求至少拆成k+1项的数。
- 很明显，所有斐波那契数都能拆成自己和许多项0，因此不用考虑。如果是斐波那契数+1，也只是多出来1，所以应该反过来考虑减法。枚举了几个斐波那契数-1的情况，发现正好可以拆成前几项隔开的斐波那契数，即n/2个。而如果再减1，因为前一种拆法的第一项一定是1，这样减去的1就会把这个1抵消掉，对应的k比之前要小。因此可以肯定k最大的数是斐波那契数-1。

## Points in solving

- 第2*k+3项斐波那契数-1，直接矩阵快速幂板子。

## Warnings

- 矩阵快速幂斐波那契从0开始，不影响
