
# LETTers Solution Report

- Date: 6 April 2018
- Author: WGM
- Problem ID: [HDU - 5240](http://acm.hdu.edu.cn/showproblem.php?pid=5240)

## Description modeling

贪心 排序后，每次选择还未准备的考试中最先开始的考试，并记录可用于后面考试复习的时间，一旦这个时间小于0，就说明前面的时间都不够复习这场考试，即可得出答案，跳出循环

## Points in solving

结构体排序，手写cmp

## Warnings

无
