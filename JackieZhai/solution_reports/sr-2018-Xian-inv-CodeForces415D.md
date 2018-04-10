# LETTers Solution Report

- Date: 10 April 2018
- Author: JackieZhai
- Problem ID: [CodeForces415D](http://codeforces.com/problemset/problem/415/D)

## Description modeling

- 从1~n中选长度为k的不下降序列(可重复选)
- 保证相邻两个数可以整除

## Points in solving

### Method 1 (TLE)
- 用dp[i][j]表示第一项是i，长度为k的好序列的个数
- 转移如下：<br>
dp[i][j] = 1 ( 1 <= j <= n && i == 1)<br>
dp[i][j] = i ( 1 <= i <= n && j == 1)<br>
dp[i][j] = dp[i][j] + dp[i/k][j-1] (由于i/k的数量与k的数量相等)<br>
答案就是dp[n][k]

### Method 2
- 用dp[i][j]表示最后一项是i，长度为k的好序列的个数
- 转移如下：<br>
dp[i][j] = 1 ( 1 <= i <= n && j == 1)<br>
dp[p][j+1] = sum(dp[i][j]) (其中 p%i == 0)<br>
答案就是sum(dp[i][k]) (1 <= i <= n)


## Warnings

- 优化dp以防超时，详见“背包九讲”

### Method 1 (TLE)
```c++
#include <bits/stdc++.h>
using namespace std;

const int MOD=1e9+7;

int dp[2007][2007];
int n, k;

int main()
{
    scanf("%d%d", &n, &k);

    for(int i=1; i<=k; i++)
        dp[1][i]=1;
    for(int i=1; i<=n; i++)
        dp[i][1]=i;

    for(int i=2; i<=n; i++)
        for(int j=2; j<=k; j++)
            for(int k=1; k<=i; k++)
            {
                dp[i][j]=(dp[i][j]+dp[i/k][j-1])%MOD;
            }

//    for(int i=1; i<=k; i++)
//    {
//        for(int j=1; j<=n; j++)
//            cout<<dp[j][i]<<" ";
//        cout<<endl;
//    }

    printf("%d\n", dp[n][k]);

    return 0;
}
```

### Method 2
```c++
#include <bits/stdc++.h>
using namespace std;

const int MOD=1e9+7;

int dp[2007][2007];
int n, k;

int main()
{
    scanf("%d%d", &n, &k);

    for(int i=1; i<=n; i++)
        dp[i][1]=1;

    for(int i=1; i<=n; i++)
        for(int j=1; j<=k; j++)
            for(int k=1; i*k<=n; k++)
            {
                dp[i*k][j]=(dp[i*k][j]+dp[i][j-1])%MOD;
            }

//    for(int i=1; i<=k; i++)
//    {
//        for(int j=1; j<=n; j++)
//            cout<<dp[j][i]<<" ";
//        cout<<endl;
//    }

    int ans=0;
    for(int i=1; i<=n;  i++)
    {
        ans=(ans+dp[i][k])%MOD;
    }
    printf("%d\n", ans);

    return 0;
}
```