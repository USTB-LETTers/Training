# LETTers Training Report

- Date: 14 April 2018
- Author: JackieZhai
- ID and Title of Contest: [LETTers 2018 Shannxi Invitational Training Round 09'](https://vjudge.net/contest/222504)

## Part I - 练习赛总结

### 题目总体结构分析：

- A: 遍历，很水
- B: 暴力区间判断，比较水
- C: 数学题，有技巧
- D: 并查集
- E: 数学+大数
- F: 二分法或者搜索优化
- G: 最大流模板题
- H: 线段树
- I: 欧拉回路
- J: 线段树

### 练习赛中的个人状态（包括整体节奏的把握）：

1. 一开始卡在C题卡了很久，一开始以为是dp，想了半天；想从小数往大数递推的时候发现n=4和n=5就可以解决24点，之后只要*1就行了，这才发现是一道技巧题
2. 之后一直没什么思路，直到发现G题是模板题，渐渐找到了一些做题的节奏
3. 最后死磕D题，想了很多种解法，最后发现用map把数组下标和数组值倒转的方法很好用，就AC了

### 与队友的协作情况：

- 无

### 其他建议：

1. 把线段树的题补一补
2. 开始学习计算几何相关内容

## Part II - AC情况(只包含赛时)

| ProblemID | Tags | 解题要点 | 
| :-: | :-: | :-: | 
| [CodeForces469A](http://codeforces.com/problemset/problem/469/A) | 水题 | 直接实现即可 | 
| [CodeForces469B](http://codeforces.com/problemset/problem/469/B) | 暴力题 | 直接三重循环实现即可 | 
| [CodeForces469C](http://codeforces.com/problemset/problem/469/C) | 数学 | 从小数开始尝试即可发现规律 | 
| [CodeForces469D](http://codeforces.com/problemset/problem/469/D) | 并查集 | 将数组下标构成并查集，分情况讨论 | 
| [POJ1273](http://poj.org/problem?id=1273) | 最大流模板题 | 直接套模板即可 | 