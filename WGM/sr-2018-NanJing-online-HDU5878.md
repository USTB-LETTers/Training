# LETTers Solution Report

- Date: 31 August 2018
- Author: WGM
- Problem ID: [HDU - 5878](http://acm.hdu.edu.cn/showproblem.php?pid=5878)

## Description modeling

- 乍一看，似乎没有多少种情况。$2^30$或者$7^11$就已经够了，完全可以暴搜。
- 注意一下每层循环变量不同，否则后面会爆long long。

## Points in solving

- 仔细一想，并不需要存下所有会用到的$a^b$，甚至连快速幂都不用。

## Warnings

- 这种暴力水题尽量写粗暴点，越快越好。
