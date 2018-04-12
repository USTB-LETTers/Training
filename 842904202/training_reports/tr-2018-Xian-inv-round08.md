# LETTers Training Report

- Date: 12 April 2018
- Author: Alice_Margatroid
- ID and Title of Contest: [LETTers 2018 Shannxi Invitational Training Round 08](https://vjudge.net/contest/221927)

## Part I - 练习赛总结

### 题目总体结构分析：

- A: 水
- B：字符串，stl
- C: 计算几何
- D: 概率dp
- E: 最短路
- F: 线段树+数学
- G: 最大流
- H: 树状数组，例题
- I: 二分
- J: 线段树


### 练习赛中的个人状态（包括整体节奏的把握）：

今天的比赛感觉还可以。一开始看见了A题发现似水非水，然后仔细一看就是水。做完提交发现WA了，在第20多个点。找不到bug就先搁着了。接着看见H题，刚好是大白上一模一样的题。
最后写了一下发现全是细节错误。数组的下标似乎很模糊。最后对着书上的改了一下下标的细节过了。这种卡数组下标不是第一次了，要找办法解决。
之后国铭出了个数据发现了A题的bug。改了之后a了。然后做I题。做了一部分之后发现二分的结束不好确定。这时国铭过来做D题。

过了一阵子看书发现二分的结束可以是精确范围也可以直接来100次。于是来了100次，wa了，改了longlong过了。

还有最后半小时的时候决定清掉B题。一看就是map的应用但是我们俩都不太会map。对着c++primer现敲了一阵子，弄了半天字符串的长度，才发现有个函数叫s.size()。
最后的两分钟a了。


### 其他建议：

暂无

## Part II - AC情况
| ProblemID | Tags | 解题要点 | 
| :-: | :-: | :-: | 
| [CodeForces - 499A](https://vjudge.net/contest/221927#problem/A) | 水题 | 直接实现即可 | 
| [CodeForces - 499B](https://vjudge.net/contest/221927#problem/B) | 水题 | 直接实现即可 | 
| [POJ - 3468](https://vjudge.net/contest/221927#problem/H) | 例题，区间和 | 树状数组+区间修改优化 | 
| [POJ - 3104](https://vjudge.net/contest/221927#problem/I) | 二分 | 二分贪心 | 

