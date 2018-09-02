# LETTers Solution Report

- Date: 1 September 2018
- Author: WGM
- Problem ID: [HDU - 6195](http://acm.hdu.edu.cn/showproblem.php?pid=6195)

## Description modeling

- m个屏幕，k个信号源，用电缆连接信号源和屏幕就是可以使屏幕上显示信号。从m个屏幕中选择k个屏幕，要求 *无论如何选择* 都可以显示出这k个信号源，问最少需要多少电缆可以满足。
- 鸽巢原理，为使m中任意选k个都会选到a，a至少需要连接n-k+1个屏幕，一共k*(n-k+1)

## Points in solving

检查样例，观察是否有特例。直接实现即可

## Warnings

无
