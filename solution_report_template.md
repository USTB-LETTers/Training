# LETTers Solution Report

- Date: 7 April 2018
- Author: WGM
- Problem ID: [HDU2736](http://acm.hdu.edu.cn/showproblem.php?pid=2736)

## Description modeling

遍历点对的距离，用map记录两点，并判断是否重复；
入map时若遇到已经重复的，就break，直接出答案

## Points in solving

每次改变点对距离，清空map；

## Warnings

点对用结构体表示，由于map用红黑树实现，结构体作下标时需要手写<操作符
