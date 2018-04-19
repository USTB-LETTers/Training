
# LETTers Solution Report

- Date: 19 April 2018
- Author: WGM
- Problem ID: [HDU - 3018](http://acm.hdu.edu.cn/showproblem.php?pid=3018)

## Description modeling

欧拉通路问题
如果只有出度和入度和为奇数的点只有两个及以下 就可以一遍不重复遍历
否则的话 可以推一下 每多出两个度数为奇数的点 就要多分一组
(有一个显然的规律是 度数为奇数的点只会有偶数个 所以一定能整除2)

## Points in solving

还要注意到 题目没有说是连通图
所以用并查集转化成子图 再对每个子图求欧拉通路

## Warnings

规律只知道个大概 细节不清楚的话 可以多编几个样例找规律
