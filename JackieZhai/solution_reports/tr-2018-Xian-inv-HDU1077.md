# LETTers Solution Report

- Date: 8 April 2018
- Author: JackieZhai
- Problem ID: [HDU1077](http://acm.hdu.edu.cn/showproblem.php?pid=1077)

## Description modeling

- 为了找能包含最多点的圆，直接枚举所有可能的圆心
- 根据贪心原理，每两个点可以确定两个“边界圆心”，这两个圆心到这两个点的距离都是1
- 然后分别计算各个圆心所包含的点数量，取最大值即可

## Points in solving

- 求两点+半径确定的圆心
- 求已知圆包络的点集数

## Warnings

- 注意题目中说`smaller 1.0001...also caught`所以选取eps为1e-4

```c++
#include <bits/stdc++.h>
using namespace std;

const int MAXN=330;
const double eps=1e-4;

double p[MAXN][2];
double xx1, yy1, xx2, yy2;

double dis(int i, int j)
{
    return sqrt((p[i][0]-p[j][0])*(p[i][0]-p[j][0]) + (p[i][1]-p[j][1])*(p[i][1]-p[j][1]));
}

void get_center_point(int a,int b)
{
    double x0=(p[a][0]+p[b][0])/2;
    double y0=(p[a][1]+p[b][1])/2;
    double d=sqrt(1-((p[a][0]-p[b][0])*(p[a][0]-p[b][0]) + (p[a][1]-p[b][1])*(p[a][1]-p[b][1]))/4);
    if(fabs(p[a][1]-p[b][1])<1e-6)
    {
        xx1=x0;
        yy1=y0+d;
        xx2=x0;
        yy2=y0-d;
    }
    else
    {
        double tmp=atan(-(p[a][0]-p[b][0])/(p[a][1]-p[b][1]));
        double dx=d*cos(tmp);
        double dy=d*sin(tmp);
        xx1=x0+dx;
        yy1=y0+dy;
        xx2=x0-dx;
        yy2=y0-dy;
    }
}

int main()
{
    int T;
    int n;
    scanf("%d",&T);
    while(T--)
    {
        scanf("%d", &n);
        for(int i=0; i<n; i++)
           scanf("%lf%lf", &p[i][0], &p[i][1]);

        int ans=1;
        for(int i=0; i<n; i++)
            for(int j=i+1; j<n; j++)
            {
                if(dis(i,j)>2.0)continue;
                get_center_point(i,j);
                int cnt=0;
                for(int i=0; i<n; i++)
                if(sqrt((p[i][0]-xx1)*(p[i][0]-xx1)+(p[i][1]-yy1)*(p[i][1]-yy1))<1+eps)
                    cnt++;
                if(cnt>ans)ans=cnt;
                cnt=0;
                for(int i=0; i<n; i++)
                    if(sqrt((p[i][0]-xx2)*(p[i][0]-xx2)+(p[i][1]-yy2)*(p[i][1]-yy2))<1+eps)
                        cnt++;
                if(cnt>ans)ans=cnt;
            }

        printf("%d\n",ans);
    }

    return 0;
}
```