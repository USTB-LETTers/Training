# LETTers Solution Report

- Date: 17 April 2018
- Author: JackieZhai
- Problem ID: [CodeForces441C](http://codeforces.com/problemset/problem/441/C)

## Description modeling

- 给定一个网格，求要铺满k条“贪吃蛇”，要怎么铺

## Points in solving

- 其实由于给的数据一定是可以铺成的，所以只需要每次铺最短的长度为2的蛇就行
- 铺完k-1个之后，剩下的是一条蛇就OK
- 由于m可能是奇数、可能是偶数，所以蛇形走位最好

## Warnings

- 无

```c++
#include <bits/stdc++.h>
using namespace std;

int n, m, k;

int main()
{
    scanf("%d%d%d", &n, &m, &k);
    int px=1, py=0;
    int dir=0; //->:0,  <-:1
    for(int i=1; i<=k-1; i++)
    {
        printf("2");
        if(dir==0)
        {
            if(py+1>m)
            {
                dir=1;
                px++;
                printf(" %d %d", px, py);
            }
            else
            {
                py++;
                printf(" %d %d", px, py);
            }
        }
        else
        {
            if(py-1<1)
            {
                dir=0;
                px++;
                printf(" %d %d", px, py);
            }
            else
            {
                py--;
                printf(" %d %d", px, py);
            }
        }
        if(dir==0)
        {
            if(py+1>m)
            {
                dir=1;
                px++;
                printf(" %d %d", px, py);
            }
            else
            {
                py++;
                printf(" %d %d", px, py);
            }
        }
        else
        {
            if(py-1<1)
            {
                dir=0;
                px++;
                printf(" %d %d", px, py);
            }
            else
            {
                py--;
                printf(" %d %d", px, py);
            }
        }
        printf("\n");
    }

    int coun;
    if(dir==0)
    {
        coun=(n-px)*m+(m-py);
        printf("%d", coun);
        while(coun--)
        {
            if(dir==0)
            {
                if(py+1>m)
                {
                    dir=1;
                    px++;
                    printf(" %d %d", px, py);
                }
                else
                {
                    py++;
                    printf(" %d %d", px, py);
                }
            }
            else
            {
                if(py-1<1)
                {
                    dir=0;
                    px++;
                    printf(" %d %d", px, py);
                }
                else
                {
                    py--;
                    printf(" %d %d", px, py);
                }
            }
        }
    }
    else
    {
        coun=(n-px)*m+(py-1);
        printf("%d", coun);
        while(coun--)
        {
            if(dir==0)
            {
                if(py+1>m)
                {
                    dir=1;
                    px++;
                    printf(" %d %d", px, py);
                }
                else
                {
                    py++;
                    printf(" %d %d", px, py);
                }
            }
            else
            {
                if(py-1<1)
                {
                    dir=0;
                    px++;
                    printf(" %d %d", px, py);
                }
                else
                {
                    py--;
                    printf(" %d %d", px, py);
                }
            }
        }
    }


    return 0;
}
```