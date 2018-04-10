# LETTers Solution Report

- Date: 10 April 2018
- Author: JackieZhai
- Problem ID: [POJ3320](http://poj.org/problem?id=3320) 

## Description modeling

- 经典尺取法模板题

## Points in solving

- 抓住尺取法的要点：为了解决`满足条件的最小区间`这类问题的方法
- 可以运用set和map这类STL提高处理能力

## Warnings

- 无

```c++
#include <cstdio>
#include <iostream>
#include <set>
#include <map>
#include <algorithm>
using namespace std;

const int MAX_P=1000007;

int P;
int a[MAX_P];

int main()
{
	scanf("%d", &P);
	for(int i=0; i<P; i++)
		scanf("%d", &a[i]);

	set<int> all; //所有知识点的集合
	for(int i=0; i<P; i++)
		all.insert(a[i]);
	int n=all.size();

	// 尺取法
	int s=0, t=0, num=0;
	map<int, int> coun; //每个知识点出现的次数
	int res=P;
	while(true)
	{
		while(t<P && num<n)
		{
			if(coun[a[t++]]++ == 0)
			{
				num++;
			}
		}
		if(num<n)
			break;
		res=min(res, t-s);
		if(--coun[a[s++]] == 0)
		{
			num--;
		}
	}
	printf("%d\n", res);

	return 0;
}
```
