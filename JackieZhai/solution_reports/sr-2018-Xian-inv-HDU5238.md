# LETTers Solution Report

- Date: 9 April 2018
- Author: JackieZhai
- Problem ID: [HDU5238](http://acm.hdu.edu.cn/showproblem.php?pid=5238)

## Description modeling

- 此题要模拟一个计算器，有+、*、^三种操作
- 给定两种查询，1是给输入求输出、2是修改某一个运算
- 线段树学习教材选~

## Points in solving

- 题目的模数比较奇怪：<br>
    1. 模数不奇怪的情况：10007、1000...00007什么的……
    2. 而模数奇怪的情况：一个不是非常大的乱七八糟的数，需要有嗅觉把它质因数分解一下，此题的29393 = 7 * 13 * 17 * 19，从此有了中国剩余定理的灵感；<br>或者在[HDU5239](http://acm.hdu.edu.cn/showproblem.php?pid=5239)里面，模数是9223372034707292160，一看就超级奇怪，试一试就发现有玄机，不论什么数，平方取模至多29次以后就不变了<br>

    **所以此题考虑用中国剩余定理，先把四个余数的情况分别算出来，存在数组里**

- 题目的复杂度很高，n和m都达到了5000，所以必须找到更快的数据结构进行维护
    
    **所以此题考虑用线段树，维护每一个模数下，各个操作的余数；叶子结点是各个操作**

## Warnings

- 请一定要进行复杂度的估计！神TM 50000<sup>2</sup> 的暴力算法做了四十多分钟 =_=

```c++
#include <bits/stdc++.h>
using namespace std;

const int MAX_N=50007;
const int MOD=29393;

int mod[4]={7, 13, 17, 19};
int p[4][20][MOD];
int f[MAX_N<<2][4][20];
int n, m;

void init()
{
    for(int i=0; i<4; i++)
    {
        int m=mod[i];
        for(int j=0; j<m; j++)
        {
            p[i][j][0]=1;
            for(int k=1; k<MOD; k++)
            {
                p[i][j][k]=p[i][j][k-1]*j%m;
            }
        }
    }
}

void cal(int k, char op, int x)
{
    for(int i=0; i<4; i++)
    {
        int m=mod[i];
        for(int j=0; j<m; j++)
        {
            if(op=='+')
                f[k][i][j]=(j+x)%m;
            else if(op=='*')
                f[k][i][j]=(j*x)%m;
            else
                f[k][i][j]=p[i][j][x];
        }
    }
}

void build(int k, int l, int r)
{
    if(l==r)
    {
        char c;
        int x;
        scanf(" %c%d", &c, &x);
        cal(k, c, x);
        return ;
    }
    int mid=(l+r)>>1;
    int ls=k<<1;
    int rs=k<<1|1;
    build(ls, l, mid);
    build(rs, mid+1, r);
    for(int i=0; i<4; i++)
    {
        int m=mod[i];
        for(int j=0; j<m; j++)
        {
            f[k][i][j]=f[rs][i][f[ls][i][j]];
        }
    }
}

void modify(int x, char c, int v, int k, int l, int r)
{
    if(l==r)
    {
        cal(k, c, v);
        return ;
    }
    int mid=(l+r)>>1;
    int ls=k<<1;
    int rs=k<<1|1;
    if(x<=mid)
        modify(x, c, v, ls, l, mid);
    else
        modify(x, c, v, rs, mid+1, r);
    for(int i=0; i<4; i++)
    {
        int m=mod[i];
        for(int j=0; j<m; j++)
        {
            f[k][i][j]=f[rs][i][f[ls][i][j]];
        }
    }
}

int exgcd(int a, int b, int &x, int &y)
{
    if(!b)
    {
        x=1, y=0 ;
        return a ;
    }
    int ans=exgcd(b ,a%b ,y ,x);
    y-=a/b*x;
    return ans;
}

int crt(int v)
{
    int ans=0;
    for(int i=0; i<4; i++)
    {
        int t=MOD/mod[i] ,x ,y;
        exgcd(t, mod[i], x, y);
        ans=(ans + f[1][i][v%mod[i]]*t*(x%mod[i])) % MOD;
    }
    return (ans+MOD)%MOD;
}

int main()
{
    int T;
    scanf("%d", &T);

    init();

    for(int kase=1; kase<=T; kase++)
    {
        printf("Case #%d:\n", kase);
        scanf("%d%d", &n, &m);

        build(1, 1, n);

        while(m--)
        {
            int type, x, v;
            char c;
            scanf("%d%d", &type, &x);
            if(type==1)
            {
                printf("%d\n", crt(x));
            }
            else
            {
                scanf(" %c%d", &c, &v);
                modify(x, c, v, 1, 1, n);
            }
        }
    }

    return 0;
}
```
