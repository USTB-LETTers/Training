# LETTers Solution Report

- Date: 31 August 2018
- Author: WGM
- Problem ID: [HDU - 5879](http://acm.hdu.edu.cn/showproblem.php?pid=5879)

## Description modeling

- cout << pi*pi/6;（逃）
- 发散的，手动打个表，到第110292项往后似乎就没变化了，仔细想一下应该只可能卡到这。

## Points in solving

- 四舍五入注意比较的时候看，而不是相差0.00001。
- 由于输入没给范围，而n较大的时候答案通过打表已知，所以用double读，需要转下标再int。（又试了下，long long确实不行）

## Warnings

- 特别大而只需要简单计算的数，用double。
