# LETTers Solution Report

- Date: 19 April 2018
- Author: JackieZhai
- Problem ID: [CodeForces552C](http://codeforces.com/problemset/problem/552/C)

## Description modeling

- 现有物品m和砝码w<sup>0</sup>, w<sup>1</sup>, w<sup>2</sup>...w<sup>100</sup>这101个砝码
- 问可不可以使得天平平衡

## Points in solving

- 由于每个砝码只有一个，所以可以对每一个w的次方数进行讨论
- 讨论的时候，允许m+1或者m-1，即为使用下一级别的砝码
- 每次讨论完，令m/=w，知道m==0为止

## Warnings

- 无

```c++
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

ll m, w;

int main()
{
    scanf("%I64d%I64d", &w, &m);

    while(m!=0)
    {
        ll l=m-1;
        ll r=m+1;

        if(l%w==0)
        {
            m--;
            m/=w;
        }
        else if(r%w==0)
        {
            m++;
            m/=w;
        }
        else if(m%w==0)
        {
            m/=w;
        }
        else
        {
            printf("NO\n");
            return 0;
        }
    }
    printf("YES\n");


    return 0;
}
```