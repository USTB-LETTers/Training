
# LETTers Solution Report

- Date: 25 July 2018
- Author: WGM
- Problem ID: [nowcoder - 141H](https://www.nowcoder.com/acm/contest/141/H)

## Description modeling

- 先粗略估计。i不等于j，否则最后结果是(1,1)。其次，i或j不能为1，否则数对中也会有1。
- 逆推，找当前素数对及其倍数可能属于哪个n。假设n=20，其中必定有个答案是(2,3)，同时再考虑，把(2,3)倍增，只要两个数都小于20，就是合法的答案。结论是，所有的答案都是通过素数对倍增得到的。也就是说，需要求比n小的素数并两两组合。再考虑倍增次数，只要倍增后小于或等于n就行，就是n除以这两个数中较大的一个。
- sum[i]表示小于i的素数个数和,注意不包括i本身，因为(i,i)不符合。ans=sum[i] * n/i，i从2取到n。

## Points in solving

素数筛并记录素数个数。

## Warnings

素数筛记录个数时，本题要求不包括i本身，所以结果要减1。但是不能在过程中减1，因为会影响到后面的计数，所以要在全部处理完后再减1。(其实i是非素数时的sum[i]不需要减1，所以可以都减，不影响结果)

## Codes

```c++

#include<bits/stdc++.h>

using namespace std;

const int MAXN = 1e7 + 233;

int N;

int prime[MAXN];
long long sum[MAXN];

long long ANS(0);

int main()
{
    cin>>N;
    for(int i=2;i<=N;++i)
        prime[i] = 1;
    for(int i=2;i<=N;++i)
    {
        if(!prime[i])
            continue;
        for(int j=i;i <= N / j;++j)
            prime[i * j] = 0;
    }
    for(int i=2;i<=N;++i)
        sum[i] = sum[i - 1] + prime[i];
    for(int i=2;i<=N;++i)
        --sum[i];
    for(int i=2;i<=N;++i)
        if(prime[i])
            ANS += N / i * sum[i];
    cout<<ANS * 2<<endl;
    return 0;
}

```
