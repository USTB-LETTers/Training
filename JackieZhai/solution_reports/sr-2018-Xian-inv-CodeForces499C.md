# LETTers Solution Report

- Date: 12 April 2018
- Author: JackieZhai
- Problem ID: [CodeForces499C](http://codeforces.com/problemset/problem/499/C)

## Description modeling

- 用一些直线把平面分成一些区域
- 有两点，两点之间的路程一次只能走两个区域之间的边，问一共要走多少步

## Points in solving

- 转化步数为两点之间有多少条直线
- 直线在两点之间说明吧两点的坐标分别带入直线，一个大于零、一个小于零（因为直线上的点是等于零的）

## Warnings

- 注意计算`Ax+By+C`的时候可能会爆int！需要用ll存