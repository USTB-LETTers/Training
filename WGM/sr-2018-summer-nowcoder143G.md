
# LETTers Solution Report

- Date: 3 August 2018
- Author: WGM
- Problem ID: [nowcoder - 143G](https://www.nowcoder.com/acm/contest/143/AG)

## Description modeling

- a和b一定是c的倍数
- a和b不能成倍数，否则gcd(a,b)=a或b
- a最大值为kc，k=n/c，那么b应该为(k-1)c

## Points in solving

相邻的两个数必然互质，互质的两个数乘c，gcd就为c

## Warnings

- c=1时，不影响
- c比n大时，不存在a和b
- k=1时，取a=b=c

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

int main()
{
    long long a,b,c,n,ans;
    scanf("%lld %lld",&c,&n);
    if(c > n)
        ans = -1;
    else
    {
        a = n/c * c;
        b = (n/c - 1) * c;
        if(b == 0)
            b = c;
        ans = a * b;
    }

    printf("%lld",ans);

    return 0;
}

```
