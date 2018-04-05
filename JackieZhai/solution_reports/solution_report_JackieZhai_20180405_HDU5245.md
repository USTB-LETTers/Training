# LETTers Solution Report

- Date: 2 April 2018
- Author: JackieZhai
- Problem ID: [HDU5245](http://acm.hdu.edu.cn/showproblem.php?pid=5245)

## Description modeling

我们单独考虑每个格子对答案的贡献，就是K次染色后被染中的概率。
但是从反面计算更简单，对于格子(r,c)计算它一次不被染中的概率p，那么K次被染中的概率就是1−p<sup>K</sup>。

总的情况数为N2M2，
要计算不被选中的情况数，就是格子(r,c)在所选的矩形外面的各种情况：

1. 所选的两个点都在(r,c)的——<br>
    上面：有(r−1)<sup>2</sup>N<sup>2</sup>种情况<br>
    左面：有M<sup>2</sup>(c−1)<sup>2</sup>种情况<br>
    下面：有(M−r)<sup>2</sup>N<sup>2</sup>种情况<br>
    右面：有M<sup>2</sup>(N−c)<sup>2</sup>种情况<br>
2. 其中四个角被计重了，要再减去——<br>
    左上角：计重了(r−1)<sup>2</sup>(c−1)<sup>2</sup><br>
    左下角：计重了(M−r)<sup>2</sup>(c−1)<sup>2</sup><br>
    右下角：计重了(M−r)<sup>2</sup>(N−c)<sup>2</sup><br>
    右上角：计重了(r−1)<sup>2</sup>(N−c)<sup>2</sup><br>

## Points in solving

- 容斥原理的运用

## Warnings

- 注意输出要double，遍历的时候要long long不然会四次方会爆
