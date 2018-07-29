
# LETTers Solution Report

- Date: 25 July 2018
- Author: WGM
- Problem ID: [nowcoder - 139B](https://www.nowcoder.com/acm/contest/139/B)

## Description modeling

rope模板题，但是卡常数，所以要尝试不同实现方式。

## Points in solving

- rope类型支持同类型的赋值和加法。
- vector没开空间不能直接赋值，rope用的是rope.push_back();

## Warnings

卡常数有很多细节，比如输出遍历时先copy而不是依此访问。

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

rope<int> s;
int ans[100010];
int main()
{
    int n,m;
    scanf("%d %d",&n,&m);
    for(int i=0; i<n; i++)
        s.push_back(i+1);

    while(m--)
    {
        int l,len;
        scanf("%d %d",&l,&len);

        s = s.substr(l-1,len) 
            + s.substr(0,l-1) 
            + s.substr(l-1+len,n-len-l+1);
    }

    s.copy(0,n,ans);
    for(int i=0; i<n; i++)
        printf("%d ",ans[i]);

    return 0;
}


```
