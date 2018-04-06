# LETTers Solution Report

- Date: 6 April 2018
- Author: JackieZhai
- Problem ID: [HDU4847](http://acm.hdu.edu.cn/showproblem.php?pid=4847)

## Description modeling

- 用string进行读入
- 从头开始遍历，每四个做一次检测即可

## Points in solving

- 无

## Warnings

- 少于四个的时候会溢出！！！以后交之前要测一下边界！

```c++
#include <bits/stdc++.h>
using namespace std;

string a;

int main()
{
    int coun=0;
    while(getline(cin, a))
    {
        if(a.size()<4) //!!!
            continue;  //!!!
        for(int i=0; i<a.size()-3; i++)
        {
            if(a[i]=='D'||a[i]=='d')
                if(a[i+1]=='O'||a[i+1]=='o')
                    if(a[i+2]=='G'||a[i+2]=='g')
                        if(a[i+3]=='E'||a[i+3]=='e')
                            coun++;
        }
    }

    printf("%d\n", coun);


    return 0;
}
```