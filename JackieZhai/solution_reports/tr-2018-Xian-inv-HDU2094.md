# LETTers Solution Report

- Date: 7 April 2018
- Author: JackieZhai
- Problem ID: [HDU2094](http://acm.hdu.edu.cn/showproblem.php?pid=2094)

## Description modeling

- 题意之中对冠军的理解，简单来说就是赢过而从没输过
- 考虑使用两个set进行实现，把los的人从win的中删除
- 如果当且仅当win中只有一个人，那么就可以说冠军确定

## Points in solving

- 注意set的查找算法、删除算法中iterator的运用

## Warnings

- 在find()方法中，找不到的时候ite==set.end()，要加判断，如果直接做*ite操作会下标越界