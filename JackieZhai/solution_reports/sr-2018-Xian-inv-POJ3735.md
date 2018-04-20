# LETTers Solution Report

- Date: 20 April 2018
- Author: JackieZhai
- Problem ID: [POJ3735](http://poj.org/problem?id=3735)

## Description modeling

- 题目初始都是零
- 题目给了三种操作，这些操作要进行k次
- 而这k次操作还要重复m次

## Points in solving

- 很明显属于矩阵递推的问题，把每k次操作构成一个矩阵，在做m次方的快速幂运算就可以了
- 关键在于如何推出此种递推式，突破口在于：
    1. 是从一串数变换到长度相等的一串数，所以用方阵作为转换矩阵
    2. 因为g操作需要统计增加的数量，所以需要在多保存一维的数据，来处理加法运算
    3. 而e就直接把所在列清零，s就是两列的交换，都比较好想<br>
    *详细可以参考代码或者[此链接](http://www.hankcs.com/program/algorithm/poj-3735-training-little-cats-time.html)*

## Warnings

- 注意：由于矩阵非常大而且稀疏，所以直接进行幂运算就会TLE，需要先判断一下(详见代码中的注释)

```c++
#include <cstdio>
#include <vector>
#include <algorithm>
#include <iostream>
using namespace std;

typedef long long ll;

typedef vector<ll> vec;
typedef vector<vec> mat;

mat mul(mat &A, mat &B)
{
    mat C(A.size(), vec(B[0].size()));
    for(int i=0; i<A.size(); i++)
        for(int k=0; k<B.size(); k++)
            if(A[i][k])//此处作一个判断，应对稀疏矩阵问题
                for(int j=0; j<B[0].size(); j++)
                    C[i][j]=(C[i][j]+A[i][k]*B[k][j]);
    return C;
}

mat pow(mat A, ll n)
{
    mat B(A.size(), vec(A.size()));
    for(int i=0; i<A.size(); i++)
        B[i][i]=1;
    while(n>0)
    {
        if(n&1)
            B=mul(B, A);
        A=mul(A, A);
        n>>=1;
    }
    return B;
}

int n, m, k;

int main()
{
    while(scanf("%d%d%d", &n, &m, &k)!=EOF)
    {
        if(n==0 && m==0 && k==0)
            break;

        mat a(1, vec(n+1));
        a[0][0]=1;

        mat b(n+1, vec(n+1));
        for(int i=0; i<n+1; i++)
            b[i][i]=1;
        while(k--)
        {
            getchar();
            char type=getchar();
            if(type=='g')
            {
                int in;
                scanf("%d", &in);
                b[0][in]++;
            }
            else if(type=='e')
            {
                int in;
                scanf("%d", &in);
                for(int i=0; i<n+1; i++)
                    b[i][in]=0;
            }
            else
            {
                int in1, in2;
                scanf("%d%d", &in1, &in2);
                for(int i=0; i<n+1; i++)
                    swap(b[i][in1], b[i][in2]);
            }
        }

        b=pow(b, m);

        a=mul(a, b);

        for(int i=1; i<=n; i++)
        {
            if(i!=1)
                printf(" ");
            printf("%lld", a[0][i]);
        }
        printf("\n");

    }


    return 0;
}
```