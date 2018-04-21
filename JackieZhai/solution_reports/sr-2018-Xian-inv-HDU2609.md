# LETTers Solution Report

- Date: 21 April 2018
- Author: JackieZhai
- Problem ID: [HDU2609](http://acm.hdu.edu.cn/showproblem.php?pid=2609)

## Description modeling

- 判断给定序列中，共有多少种序列
- 没种序列内，可以循环滚动

## Points in solving

- 最小表示法的应用
- 将所有输入字符串转化为最小表示，存在set中，再进行比对

## Warnings

- 关注一切STL的清零操作！

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <string>
#include <set>
#include <algorithm>
using namespace std;

int coun;
char str[10007];
set<string> se;

int minRepre()
{
    int n = strlen(str);
    int i = 0,j = 1, k = 0;
    while(i<n && j<n && k<n)
    {
        int t = str[(i+k)%n] - str[(j+k)%n] ;
        if(t == 0)
            k++;
        else
        {
            if(t>0)
                i+=k+1;
            else
                j+=k+1;
            if(i==j)
                j++;
            k = 0;
        }
    }
    return i < j ? i : j;
}


int main()
{
    while(scanf("%d", &coun)!=EOF)
    {
        se.clear();
        int ans=0;
        getchar();
        while(coun--)
        {
            scanf("%s", str);
            int len=strlen(str);
            int les=minRepre();
            string s;
            for(int i=les; i<len; i++)
                s.push_back(str[i]);
            for(int i=0; i<les; i++)
                s.push_back(str[i]);
            if(!se.count(s))
            {
                ans++;
                se.insert(s);
            }
        }
        printf("%d\n", ans);
    }


    return 0;
}
```