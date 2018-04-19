# LETTers Solution Report

- Date: 19 April 2018
- Author: JackieZhai
- Problem ID: [CodeForces552D](http://codeforces.com/problemset/problem/552/D)

## Description modeling

- 给定一些点，问能围成的三角形的数量

## Points in solving

- 由于点不是很多，可以三重循环
- 再判断是否共线即可

## Warnings

- 注意此题的所有点都是整数点，所以判断共线的时候直接用乘法判断即可，不用考虑精度问题
- 注意三重循环的写法，不要有交叉重复的情况出现

```c++
#include <bits/stdc++.h>
using namespace std;

pair<int, int> P[2007];
int n;

int main()
{
    scanf("%d", &n);
    for(int i=1; i<=n; i++)
        scanf("%d%d", &P[i].first, &P[i].second);

    int ans=0;
    for(int i=1; i<=n-1; i++)
    {
        for(int j=i+1; j<=n-1; j++)
        {
            for(int k=j+1; k<=n; k++)
            {
                if((P[j].first-P[i].first)*(P[k].second-P[i].second)-(P[k].first-P[i].first)*(P[j].second-P[i].second)!=0)
                    ans++;
            }
        }
    }
    printf("%d\n", ans);

    return 0;
}
```