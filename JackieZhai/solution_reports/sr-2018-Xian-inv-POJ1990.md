# LETTers Solution Report

- Date: 10 April 2018
- Author: JackieZhai
- Problem ID: [POJ1990](http://poj.org/problem?id=1990)

## Description modeling

- 直线上有很多牛，两个牛的传播是max(v[i], v[j])*dis
- 求得两两牛的传播的总和
- 树状数组学习教材选~

## Points in solving

- 将牛按聋的程度从小到大排，保证最后取的牛能对其他所有牛进行“距离和”运算
- 使用树状数组维护求和运算，降低时间复杂度
	1. 第一个BIT存放牛的数量，下标是坐标，方便查找左右牛数
	2. 第二个BIT存放牛的距离，下标是坐标，方便计算距离和用
	3. 综合1和2，利用公式`v*((left*x-sum2(x-1)) + ((sum2(20000)-sum2(x))-right*x))`可以轻松计算距离和 

## Warnings

- 注意下标都是从1开始的，坐标是从1~20000
- 注意区间的sum要用sum(y)-sum(x)表示sum(x+1, y)

```c++
#include <cstdio>
#include <cmath>
#include <cstring>
#include <algorithm>
#include <iostream>
using namespace std;

typedef long long ll;

//BIT均是index-1
ll bit[20007]; //下标是坐标，统计牛的个数
int n;
ll sum(int i)
{
    ll s=0;
    while(i>0)
    {
        s+=bit[i];
        i-=i&-i;
    }
    return s;
}
void add(int i, ll x)
{
    while(i<=n)
    {
        bit[i]+=x;
        i+=i&-i;
    }
}

ll bit2[20007]; //下标是坐标，统计牛的距离
int n2;
ll sum2(int i)
{
    ll s=0;
    while(i>0)
    {
        s+=bit2[i];
        i-=i&-i;
    }
    return s;
}
void add2(int i, ll x)
{
    while(i<=n2)
    {
        bit2[i]+=x;
        i+=i&-i;
    }
}

int m;
struct Node{
    ll v, x;
    friend bool operator < (const Node &a, const Node &b)
    {
        return a.v<b.v;
    }
}a[20007];


int main()
{
    while(scanf("%d", &m)!=EOF)
    {
        for(int i=1; i<=m; i++)
            scanf("%d%d", &a[i].v, &a[i].x);

        sort(a+1, a+m+1);

        memset(bit, 0, sizeof(bit));
        memset(bit2, 0, sizeof(bit2));
        n=20000;
        n2=20000;
        ll ans=0;
        for(int i=1; i<=m; i++)
        {
            //从小牛开始
            int v=a[i].v;
            int x=a[i].x;
            ll left=sum(x-1);
            ll right=sum(20000)-sum(x);
            ans+=v*((left*x-sum2(x-1)) + ((sum2(20000)-sum2(x))-right*x));
            //添加此牛的信息
            add(x, 1);
            add2(x, x);
        }
        printf("%lld\n", ans);
    }

    return 0;
}
```