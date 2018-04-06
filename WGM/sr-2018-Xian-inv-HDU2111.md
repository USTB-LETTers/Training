# LETTers Solution Report

- Date: 5 April 2018
- Author: WGM
- Problem ID: [HDU - 2111](http://acm.hdu.edu.cn/showproblem.php?pid=2111)

## Description modeling

贪心背包，对价值排序，每次选择最高价值的物品，如果全选不超过容量就全选，否则就装满并跳出循环

## Points in solving

p[i]是单位价值，不是总价值
用结构体存价值和体积，方便排序（sort中cmp的使用）

## Warnings

v为0的时候结束输入，所以应该先读入v，判断是不是0，再读入n
for循环中循环条件如果有多个，应该取且（&&），而不是用逗号表达式
