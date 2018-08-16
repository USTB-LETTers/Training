
# LETTers Solution Report

- Date: 15 August 2018
- Author: WGM
- Problem ID: [nowcoder - 145J](https://www.nowcoder.com/acm/contest/145/J)

## Description modeling

- 因为只有52种字母，所以每次最大只需要考虑52*52的方格，暴力的复杂度为O(52*52*n*m)，考虑常数优化。
- 往右下遍历，每个格子往左上延展，所以只需要记录横向和纵向的最大可延展长度。

## Points in solving

可延展长度可以直接暴力O(52*n*m),没必要前缀和优化，而且容易写错= =

## Warnings

对于“每行每列”和“任意行列”题意有点模糊，样例也体现不出来

## Codes

```c++

#include<bits/stdc++.h>
#include<ext/rope>
using namespace std;
using namespace __gnu_cxx;

const int MAXN = 1000 + 10;

map<char,int> mm;
int lenn[MAXN][MAXN],lenm[MAXN][MAXN];
int main()
{
    memset(lenn,0,sizeof(lenn));
    memset(lenm,0,sizeof(lenm));

    int n,m;
    string s[MAXN];
    scanf("%d %d",&n,&m);
    for(int i=0; i<n; ++i)
        cin >> s[i];

    for(int i=0; i<n; ++i)
        for(int j=0; j<m; ++j)
        {
            char c = s[i][j];
            mm.clear();
            mm[c] = 1;
            for(int k=1; k<=52; ++k)
            {
                if(i-k >= 0 && !mm.count(s[i-k][j]))
                    mm[ s[i-k][j] ] = 1;
                else
                {
                    lenn[i][j] = k-1;
                    break;
                }
            }
            mm.clear();
            mm[c] = 1;
            for(int k=1; k<=52; ++k)
            {
                if(j-k >= 0 && !mm.count(s[i][j-k]))
                    mm[ s[i][j-k] ] = 1;
                else
                {
                    lenm[i][j] = k-1;
                    break;
                }
            }
        }

    int ans = 0;
    for(int i=0; i<n; ++i)
    {
        for(int j=0; j<m; ++j)
        {
            int now = ans;
            int nown = 52,nowm = 52;
            for(int k=0; k<=52; ++k)
            {
                if(i-k < 0 || j-k < 0 || lenn[i][j-k] < k || lenm[i-k][j] < k)
                    break;
                nown = nown < lenn[i][j-k] ? nown : lenn[i][j-k];
                nowm = nowm < lenm[i-k][j] ? nowm : lenm[i-k][j];
                ans += (nown-k) + (nowm-k) + 1;
                if(nown == 0 || nowm == 0)
                    break;
            }
            //printf(" %d ",ans-now);
        }
        //printf("\n");
    }

    printf("%d",ans);

    return 0;
}


```
