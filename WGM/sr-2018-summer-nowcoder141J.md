
# LETTers Solution Report

- Date: 30 July 2018
- Author: WGM
- Problem ID: [nowcoder - 141J](https://www.nowcoder.com/acm/contest/141/J)

## Description modeling

面积表示期望，就是求半径r，使圆在多边形内的面积为多边形总面积的1-P/Q倍。显然半径越大相交面积越大，所以可以二分答案。本题关键是求面积。

## Points in solving

- 处理多边形的通用思路是，分成多个三角形。本题就是把三角形与圆结合，取圆心和每一条边，讨论边和圆的关系。
- 三种情况
  - 线段（边）在圆形外部，如果线段和圆不相交，面积就是圆周角对应的扇形；如果相交，则是大的扇形面积减去两交点对应的扇形面积，再加上两交点的三角形面积
  - 线段在圆形内部，面积就是两端点和圆心围成的三角形
  - 线段两端点一个在圆心内，一个在圆心外。原理与第一种类似，也是两个扇形相减再加上三角形。
- 考虑方向，所求的面积贡献（正负）可以通过叉乘的正负判断。
- 输入的点可能是逆时针也可能是顺时针，根据面积正负转换一下即可，也可以不变，但是后面所有求的面积都要带正负。

## Warnings

- 实际实现时，还要考虑钝角和锐角对应关系的不同、三点共线等情况，改公式和分类非常麻烦。
- 参考题解思路，对于计算几何题，要尽量减少情况分类和公式的复杂度，要找到基础情况并把各种情况转换。比如只考虑一个点在圆上一个点在内部和外部这两种基础情况。那么相交就可以以交点分隔，转换成多个基础情况，方向再额外考虑即可。根据

## Codes

```c++
#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

const double e = 1e-8;
const double pi = acos(-1);
struct Point
{
    double x,y;
}p0,p[210];

double mc(Point a,Point b,Point c,Point d)//叉乘
{
    return (b.x-a.x)*(d.y-c.y)-(b.y-a.y)*(d.x-c.x);
}

double dis(Point a,Point b)//两点距离
{
    return sqrt( pow(a.x-b.x,2) + pow(a.y-b.y,2) );
}

double mind(Point a,Point b,double r)//线段到圆心最短距离 相离则为-1
{
    double h=0;
    h = mc(p0,a,p0,b) / dis(a,b);
    if(h < 0)
        h = -h;
    if(h >= r)
        return -1;
    return h;
}

double theta(Point pp,Point a,Point b)//ppa和ppb的夹角
{
    double ans;
    a.x -= pp.x;
    a.y -= pp.y;
    b.x -= pp.x;
    b.y -= pp.y;
    ans = (a.x*b.x + a.y*b.y) / sqrt(a.x*a.x + a.y*a.y) / sqrt(b.x*b.x + b.y*b.y);
    return acos(ans);
}

double area(Point a,Point b,double r)//折线与圆围成的面积 化成三角形
{
    if((a.x == p0.x && a.y == p0.y) || (b.x == p0.x && b.y == p0.y))
        return 0;
    
    int flag = 1;
    if(mc(p0,a,p0,b) < 0)   //面积贡献为正还是负
        flag = -1;

    if( (dis(p0,a) <= r) && (dis(p0,b) <= r) )   //内部
        return mc(p0,a,p0,b) / 2.0;
    else if( (dis(p0,a) > r) && (dis(p0,b) > r) )  //外部
    {
        if(mind(a,b,r) == -1 || theta(a,p0,b) > pi/2.0 || theta(b,p0,a) > pi/2.0)               //相离                       
            return theta(p0,a,b) / 2 * r * r * flag;
        else            //相交
        {
            double h=mind(a,b,r),sinth,d,s1,s2,s3;
            d = sqrt(r*r - h*h) * 2;
            sinth = h * d / r / r;
            s1 = theta(p0,a,b) / 2 * r * r;
            if(theta(p0,a,b) > pi/2.0)//三角形顶角为钝角
                s2 = (pi - asin(sinth)) / 2 * r * r;
            else
                s2 = asin(sinth) / 2 * r * r;
            s3 = d * h / 2;
            //printf("    %.6lf %.6lf s1=%.6lf s2=%.6lf s3=%.6lf\n",h,d,s1,s2,s3);
            return (s1 - s2 + s3)*flag;
        }
    }
    else    //一个点在圆内，另一个在外
    {
        if(dis(p0,b) > r)  //保证a在圆外
        {
            Point c;
            c=a,a=b,b=c;
        }
        double h=mind(a,b,r),sinth,d1,d2,lb,s1,s2,s3;
        lb = dis(b,p0);
        d1 = sqrt(r*r - h*h);
        d2 = sqrt(lb*lb - h*h);
        s1 = theta(p0,a,b) / 2 * r * r;
        if(theta(b,p0,a) > pi/2.0) //高在两端点一侧
        {
            sinth = (d1 - d2) * h / r / lb;
            s2 = asin(sinth) / 2 * r * r;
            s3 = (d1 - d2) * h / 2;
        }
        else//高在两端点中间
        {
            sinth = (d1 + d2) * h / r / lb;
            if(theta(p0,a,b) > pi/2.0)  //三角形顶角为钝角
                s2 = (pi - asin(sinth)) / 2 * r * r;
            else
                s2 = asin(sinth) / 2 * r * r;
            s3 = (d1 + d2) * h / 2;
        }
        //printf("   %.6lf %.6lf %.6lf s1=%.6lf s2=%.6lf s3=%.6lf\n",h,d1,d2,s1,s2,s3);
            
        return (s1 - s2 + s3)*flag;
    }
}

double P,Q,ans,arean;
int n;

void find(double l,double r)
{
    double aream=0,mid=(l+r)/2;
    //printf("===%.6lf %.6lf %.6lf===\n",l,r,mid);
    if( fabs(l-r) < e )
    {
        ans = mid;
        return;
    }
    
    for(int i=1; i<=n-1; i++)
    {
        aream += area(p[i],p[i+1],mid);
        //printf("r=%.6lf %.6lf,%.6lf %.6lf,%.6lf    %.6lf %.6lf\n",mid,p[i].x,p[i].y,p[i+1].x,p[i+1].y,area(p[i],p[i+1],mid),aream);
    }
    aream += area(p[n],p[1],mid);
        //printf("r=%.6lf %.6lf,%.6lf %.6lf,%.6lf    %.6lf %.6lf\n\n",mid,p[n].x,p[n].y,p[1].x,p[1].y,area(p[n],p[n+1],mid),aream);

    if( aream/arean == 1.0-P/Q )
        ans = mid;
    else if( aream/arean > 1.0-P/Q )
        find(l,mid);
    else 
        find(mid,r);

    return;
}

int main()
{
    int m;
    scanf("%d",&n);
    for(int i=1; i<=n; i++)
        scanf("%lf %lf",&p[i].x,&p[i].y);
    
    arean=0;
    for(int i=2; i<=n-1; i++)
        arean += mc(p[1],p[i],p[1],p[i+1]) / 2;

    //printf("arean=%.6lf\n",arean);
    if(arean < 0)
    {
        for(int i=1; i<=n/2; i++)
        {
            Point t;
            t = p[i];
            p[i] = p[n+1-i];
            p[n+1-i] = t;
        }
        arean = -arean;
    }

    scanf("%d",&m);
    while(m--)
    {
        scanf("%lf %lf %lf %lf",&p0.x,&p0.y,&P,&Q);
        find(sqrt((1.0-P/Q)*arean/pi),2000);
        printf("%.8lf\n",ans);
    }

    return 0;
}


```
