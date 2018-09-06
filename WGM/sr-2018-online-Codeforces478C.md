# LETTers Solution Report

- Date: 6 September 2018
- Author: WGM
- Problem ID: [CodeForces - 478C](http://codeforces.com/problemset/problem/478/C)

## Description modeling

- 给出三种颜色的气球个数，往桌子上贴气球，每个桌子贴3个，且这三个气球颜色不能完全一样，求最多贴多少个桌子。
- 贪心的想，肯定是把最少的那种气球放满，然后补第二少的。再仔细一想，“第二少”肯定不会过多(不会有哪个桌子不得不贴3个第二少的)。所以理想情况是n=sum/3，如果最少+第二少≥n，就能铺满，否则就是把最多的和前两种按2：1放置。

## Points in solving

直接实现

## Warnings

无
