
# LETTers Solution Report

- Date: 7 April 2018
- Author: WGM
- Problem ID: [Codeforces - 499C](http://codeforces.com/problemset/problem/499/C)

## Description modeling

第一反应是扫描线：
扫到多少条线就要跨越几个blocks
仔细一想，并不会有绕远的路线符合，也就是说不需要扫描，
因为都是直线，长度无限的，所以最近的路一定是跨blocks最少的；
只要观察起点终点中有多少条路就行了

## Points in solving

要判断线段和多少条直线相交不容易，不如对每一条直线判断其是否在两点之间；
最先想到的就是把两点投影在直线上，纵坐标值一大一小就说明在两边，再单独讨论b=0，也就是垂直y轴的情况；

再仔细一想，可以把除法变成乘法来提高精度(这应该成为一个好习惯)，再移项就会发现这个式子很熟悉
——其实就是把点带到直线方程里，一个大于0一个小于0
恍然发现，这是数学里可以直接用的结论
并且正好包括了b=0的情况，不用单独讨论了。

## Warnings

计算几何要冷静，要有大局观。
