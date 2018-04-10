# LETTers Solution Report

- Date: 7 April 2018
- Author: JackieZhai
- Problem ID: [CodeForces741A](http://codeforces.com/problemset/problem/741/A)

## Description modeling

- 判断有向图的最小环，用暴力搜索就可以
- 当环节点数大于n，说明有重复走的路，不可达，直接-1输出
- 最后把每个最小环的t求最小公倍数就是所求

## Points in solving

- 注意偶数t的时候，正反都可以走，在中间汇合，所以要除以2

## Warnings

- 无

```c++
#include <bits/stdc++.h>
using namespace std;

bool used[107];
int a[107];

int gcd(int a, int b)
{
    if(b==0)
        return a;
    else
        return gcd(b, a%b);
}

int main()
{
    int n;
	scanf("%d", &n);
    fill(used, used+n+1, false);

    for(int i=1; i<=n; i++)
        scanf("%d", &a[i]);

    int ans=1;
    for(int i=1; i<=n; i++)
    {
        if(used[i])
            continue;
        used[i]=true;
        int aa=a[i];

        int coun=1;
        while(aa!=i)
        {
            used[aa]=true;
            aa=a[aa];
            coun++;
            if(coun>n)
            {
                printf("-1\n");
                return 0;
            }
        }
        if(coun%2==0)
            coun/=2;
        ans=ans*coun/gcd(ans,coun);
    }
    printf("%d\n",ans);

	return 0;
}
```
