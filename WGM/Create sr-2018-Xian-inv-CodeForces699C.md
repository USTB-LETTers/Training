
# LETTers Solution Report

- Date: 21 April 2018
- Author: WGM
- Problem ID: [CodeForces - 699C](http://codeforces.com/problemset/problem/699/C)

## Description modeling

很明显的无后效性 当前的选择只与上一次选择有关

## Points in solving

状态转移比较复杂 因为要根据a的情况调整
怕细节出错可以把所有情况都写上
从前一天状态为k转移到这一天状态为j 其中k非零时k！=j 且j要受输入的控制
对所有的k 选择合法且使状态j值最大的转移方式

## Warnings

最后输出是n减去最后一天的最大值
