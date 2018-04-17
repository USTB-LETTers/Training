# LETTers Training Report

- Date: 17 April 2018
- Author: JackieZhai
- ID and Title of Contest: [LETTers 2018 Shannxi Invitational Training Round 11'](https://vjudge.net/contest/223068)

## Part I - 练习赛总结

### 题目总体结构分析：

- A: 水题
- B: 贪心题，有些水、有些坑
- C: 贪心+模拟题，比较水
- D: 置换群？
- E: 概率dp
- F: 矩阵快速幂运算
- G: 水题，有坑
- H: 最小费用+负圈+消圈(spfa)
- I: 二分图判定(染色法)+二分图最大匹配(最大流或者匈牙利)

### 练习赛中的个人状态（包括整体节奏的把握）：

1. 前两道题进展不错，虽然B水题掉进了坑里，但还是很快爬出来了
2. 之后看榜发现G题很快就有人AC了，就从此题开始做了，顺便把F题也AC了
3. E题本以为概率dp可以做，没想到很复杂，占用了很长时间还是WA了，就立马跳向其他题了
4. 发现I题是二分图的两种模板的组合，很快就AC了

### 与队友的协作情况：

- 无

### 其他建议：

1. 把那道概率题死磕出来
2. 顺便再以后的比赛中，注意概率这类数学性比较强的题需要放在最后慢慢钻研

## Part II - AC情况(只包含赛时)

| ProblemID | Tags | 解题要点 | 
| :-: | :-: | :-: | 
| [CodeForces441A](http://codeforces.com/problemset/problem/469/A) | 水题 | 直接实现即可 | 
| [CodeForces441B](http://codeforces.com/problemset/problem/469/B) | 贪心 | 注意可能出现重复的问题 | 
| [CodeForces441C](http://codeforces.com/problemset/problem/469/C) | 贪心+模拟 | 只需每次取最短的长度为2的管道就行，蛇形走位 | 
| [POJ3233](http://poj.org/problem?id=3233) | 矩阵快速幂 | 直接套模板即可 | 
| [POJ2499](http://poj.org/problem?id=2499) | 水题 | 注意细节，直接实现即可 | 
| [HDU2444](http://acm.hdu.edu.cn/showproblem.php?pid=2444) | 二分图 | 染色判图+二分图最大匹配算法 |