# LETTers Solution Report

- Date: 31 August 2018
- Author: WGM
- Problem ID: [HDU - 5878](http://acm.hdu.edu.cn/showproblem.php?pid=5878)

## Description modeling

- 乍一看，似乎没有多少种情况。 <a href="https://www.codecogs.com/eqnedit.php?latex=2^{30}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?2^{30}" title="2^{30}" /></a> 或者 <a href="https://www.codecogs.com/eqnedit.php?latex=7^{11}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?7^{11}" title="7^{11}" /></a> 就已经够了，完全可以暴搜。
- 注意一下每层循环变量不同，否则后面会爆long long。

## Points in solving

- 仔细一想，并不需要存下所有会用到的$a^b$，甚至连快速幂都不用，直接循环乘法，边乘边判断是否越界。

## Warnings

- 这种暴力水题尽量写粗暴点，越快越好。
