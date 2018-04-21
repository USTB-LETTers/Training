# LETTers Solution Report

- Date: 21 April 2018
- Author: JackieZhai
- Problem ID: [CodeForces701D](http://codeforces.com/problemset/problem/701/D)

## Description modeling

- 给出了bus和walk两种方法，共有n个人，车辆k个座位
- 车辆需要来回接送，这点要考虑进去

## Points in solving

- 关键是需要n个人都到终点，所以每个人bus的距离是一样的为最优
- 注意，bus送最后一波人的时候不需要掉头了
- 计算公式：
    1. 计算kase，注意有余数的情况
    2. 计算busl，即每人做车的路程`l*(v1+v2)/(2*v1*(kase-1)+v1+v2)`
    3. 计算t，详见代码

## Warnings

- 无

```c++
#include <bits/stdc++.h>
using namespace std;

int n, k;
double l, v1, v2;
double d, t;

int main()
{
    scanf("%d%lf%lf%lf%d", &n, &l, &v1, &v2, &k);

    int kase=n/k;
    if(n%k!=0)
        kase++;
    if(kase-1==0)
    {
        printf("%.10lf\n", l/v2);
        return 0;
    }

    double busl=l*(v1+v2)/(2*v1*(kase-1)+v1+v2);
    double walkl=l-busl;
    double ans=(double)(kase-1)*(busl-walkl/(kase-1))+busl*kase;
    ans/=v2;

    printf("%.10lf\n", ans);

    return 0;
}
```