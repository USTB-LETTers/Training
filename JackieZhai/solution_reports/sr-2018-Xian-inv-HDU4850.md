# LETTers Solution Report

- Date: 9 April 2018
- Author: JackieZhai
- Problem ID: [HDU4850](http://acm.hdu.edu.cn/showproblem.php?pid=4850)

## Description modeling

- 给定一个n，要求输出一个长度为n的字符串，并且不会有长度大于等于4的重复的子串，不能得到输出Impossible
- 此题要先判断最长是多长，应该是26<sup>4</sup>+3长度的串，超过的就不可能了

## Points in solving

### Method 1
- 运用欧拉回路，以长度为3的串为节点，一共有26<sup>3</sup>个节点，每个节点出度为26，入度为26，最后构造出的串起始就是走过边的权值，要求每个节点刚好经过26次。
- 可以考虑用贪心的方法，每次移动的下一个节点，一定是当前能移动到节点的中经过最少次数的节点，这样做去保证每个节点都能刚好走26次。

### Method 2
- 运用哈希的思想，构造一个四维的标记数组，从第四个开始逐个判重即可
- 真的比想象简单！详见下面代码

## Warnings

- 若用string的s=s+char拼接，速度很慢；而用char s[]，然后s[size++]=char，就快得多啦

### Method 2
```c++
#include <bits/stdc++.h>
using namespace std;

const int maxn=26*26*26*26;

int a[500005];
int vis[26][26][26][26];

int main()
{
    memset(vis,0,sizeof vis);
    a[1]=0, a[2]=0, a[3]=0;

    for(int i=4; i<=maxn+3; i++)
    {
        for(int j=25; j>=0; j--)
        {
            if(vis[a[i-3]][a[i-2]][a[i-1]][j]==0)
            {
                a[i]=j;
                vis[a[i-3]][a[i-2]][a[i-1]][j]=1;
                break;
            }
        }
    }

    int n;
    while(scanf("%d",&n)!=EOF)
    {
        if(n>maxn+3)
        {
            printf("Impossible\n");
        }
        else
        {
            for(int i=1; i<=n; i++)
                printf("%c", a[i]+97);
            printf("\n");
        }
    }

    return 0;
}
```

### Method 1
```c++
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;
const int maxn = 26*26*26;
const int mod = 26 * 26;
const int maxl = 500005;

int maxlen;
int v[maxn+5][30], c[maxn+5];
char s[maxl];

inline int get_next (int u, int k)
{
    return (u % mod) * 26 + k;
}

int find_next (int u)
{
    int x = 0, ans = -1;
    for (int i = 1; i < 26; i++)
    {
        if (v[u][i])
            continue;

        int tmp = get_next(u, i);
        if (ans == -1 || c[tmp] < c[ans])
        {
            ans = tmp;
            x = i;
        }
    }
    return x;
}

void init ()
{
    maxlen = maxn * 26 + 3;

    int mv, u = 0;
    memset(v, 0, sizeof(v));
    for (mv = 0; mv < 3; mv++)
        s[mv] = 'a';

    while (true)
    {
        int x = find_next(u);
        int next = get_next(u, x);
        if (c[next] == 26)
            break;

        c[next]++;
        s[mv++] = x + 'a';
        v[u][x] = 1;
        u = next;
    }
}

int main ()
{
    int n;
    init();
    while (scanf("%d", &n) == 1)
    {
        if (n <= maxlen)
        {
            for (int i = 0; i < n; i++)
                printf("%c", s[i]);
            printf("\n");
        }
        else
            printf("Impossible\n");
    }
    return 0;
}
```
