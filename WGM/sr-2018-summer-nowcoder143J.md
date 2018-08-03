
# LETTers Solution Report

- Date: 3 August 2018
- Author: WGM
- Problem ID: [nowcoder - 143J](https://www.nowcoder.com/acm/contest/143/J)

## Description modeling

一定要列出所有情况：
- 首先，要尽量选性价比高的房间，然后用另一个房间去补
- 用来补的三人间只需要1个，否则2个三人间必然劣与3个双人间
- 用来补的双人间可能是1个或者2个，否则3个双人间必然劣于2个三人间

## Points in solving

比赛时不用考虑优化和压缩，简单题直接暴力列出所有情况反而不容易错

## Warnings

三人间性价比高时，双人间可能是2个

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

int main()
{
    long long n,ans1,ans2;
    long long p2,p3;
    scanf("%lld %lld %lld",&n,&p2,&p3);


    if(n == 1)
    {
        printf("%0.lf",p2>p3?p3:p2);
        return 0;
    }

    if(p2*3 <= p3*2)
    {
        if(n%2 == 0)
        {
            ans1 = n/2 * p2;
            ans2 = ans1;
        }
        else
        {
            ans1 = (n/2+1) * p2;
            ans2 = ((n-3)/2) * p2 + p3;
        }
    }
    else
    {
        if(n%3 == 0)
        {
            ans1 = n/3*p3;
            ans2 = ans1;
        }
        else
        {
            ans1 = (n/3+1)*p3;
            if(n%3 == 1)
            {
                ans2 = (n-4)/3*p3 + 2*p2;
                ans1 = ans1<ans2?ans1:ans2;
                ans2 = n/3*p3 + p2;
            }
            else
                ans2 = n/3*p3 + p2;
        }
    }

    printf("%lld",ans1>ans2?ans2:ans1);

    return 0;
}


```
