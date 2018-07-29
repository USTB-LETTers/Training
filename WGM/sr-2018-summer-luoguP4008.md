
# LETTers Solution Report

- Date: 29 July 2018
- Author: WGM
- Problem ID: [luogu - P4008](https://www.luogu.org/problemnew/show/P4008)

## Description modeling

- 平衡树模版题，练习熟悉一下stl里的rope（块状链表实现可持久化平衡树）
- 支持插入、删除、读取、替换操作，且繁杂度都是O(logn)，有链表的优点方便修改，且能像数组一样访问下标。

## Points in solving

题目本身不难，关键是Insert操作的字符串内可能含其它字符。本来只考虑到\n，然后根据linux评测还要忽略\r，但转念一想，既然题目给了合法的ascii码区间，就应该根据区间判断。

## Warnings

getchar读字符限定最好用题目中给定限制的ascii码，以及，多用string。

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

rope<char> s;

char str[2000000];
int main()
{
    int t,now=0,x;
    scanf("%d",&t);
    while(t--)
    {
        scanf("%s",str);
        switch(str[0])
        {
            case 'M' : scanf("%d",&now);break;
            case 'I' :
            {
                scanf("%d",&x);
                for(int i=0; i<x; i++) 
                {
                    str[i]=getchar();
                    while(str[i] < 32 || str[i] > 126) 
                        str[i]=getchar();
                }
                str[x]=0;
                s.insert(now,str);
                break;
            }
            case 'D' :
            {
                scanf("%d",&x);
                s.erase(now,x);
                break;
            }
            case 'G' :
            {
                scanf("%d",&x);
                s.copy(now,x,str);
                str[x] = 0; 
                printf("%s\n",str);
                break;
            } 
            case 'P' : now--;break;
            case 'N' : now++;break;  
        }
        //s.copy(0,100,str);
        //printf("  %d==%s\n",t,str);
    }

    return 0;
}

```
