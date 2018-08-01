
# LETTers Solution Report

- Date: 1 August 2018
- Author: WGM
- Problem ID: [nowcoder - 142F](https://www.nowcoder.com/acm/contest/142/F)

## Description modeling

- 大矩形和方案的长宽都是偶数，且要求对称，所以必须放在正中间，结论是只要确认长宽，方案就唯一确定。
- 有缺陷时，要求水池必须覆盖缺陷位置，就可以确定水池最小的长和宽。

## Points in solving

- 只要记录最外侧的缺陷的长和宽。
- 暴力搜索缺陷时只需要四分之一。

## Warnings

最终结论算式可简化。（然而水题并没有什么用= =）

## Codes

```c++

#include<bits/stdc++.h>
using namespace std;

const int MAXN = 2010;
string a[MAXN];

int main()
{
    int n,m,t,minn,minm;
    scanf("%d",&t);
    while(t--)
    {
        scanf("%d %d",&n,&m);
        minn = n/2 - 1;
        minm = m/2 - 1;
        for(int i=0; i<n; i++)
            cin >> a[i];
        for(int i=0; i<n/2; i++)
            for(int j=0; j<m/2; j++)
            {
                if(j > minm)
                    break;
                if( a[i][j] == a[i][m-j-1] && a[i][j] == a[n-i-1][m-j-1] && a[i][j] == a[n-i-1][j] )
                    continue;
                else
                {
                    //printf("   %d %d\n",i,j);
                    if(minn > i)
                        minn = i;
                    if(minm > j)
                        minm = j;
                }
            }

        int ans = minn * minm;
        printf("%d\n",ans); 
                
    }


    return 0;
}


```
