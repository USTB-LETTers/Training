
# LETTers Solution Report

- Date: 12 April 2018
- Author: Alice_Margatroid
- Problem ID: [POJ - 3368](https://vjudge.net/contest/221535#problem/I)

## Description modeling

大白的课后练习题。

给定N头奶牛和它们的位置以及各自的吼声大小，计算所有N（N-1）/2对奶牛之间，两两距离乘以二者之中吼声较大的那个值的和。

1<=N<=50000。

朴素的算法要N^3，肯定不行。所以这里要用到树状数组。

我理解中的树状数组是一种可以进行修改的前缀和。数组的每i位代表从第2^[log(i)]+1位到第i位之和。面对任意求和，有一个sum函数进行计算：

```c++
int sum (int *b,int i)
{
	
	int s=0;
	while(i>0)
	{
		s+=b[i];
		i-=i&-i;
	}
	return s;
}
```
乍一看好像很难懂对吧。其实就是利用了位运算巧妙计算了从第一位到第i位的值。这个函数也不需要做什么修改，直接用就行。

而修改值用的函数是add函数：


```c++
void add(int *b,int i,int v)
{
	
	while(i<=maxN)
	{
		b[i]+=v;
		i+=i&-i;
	}
}
```
同样是位运算，add函数的意思说白了就是为所有包括你所要操作的值的区间进行一次加和。

相比于前缀和或后缀和的简单实现，树状数组可以很方便的在nlogn的时间内进行单点修改和查询。

区间修改也可以，只不过要添加另一个bit数组。这里不再赘述。


算法的思路描述如下：

先对所有奶牛的位置和吼声分别升序和降序排序。建立树状数组，分别设置bit1,bit2,bit3,bit4，前两个用来存奶牛距离的前缀和后缀和，后两个用来存区间内剩余奶牛的个数。之后，每次利用已经排好的吼声序列，读取下一个吼声最大的奶牛，计算它的位置i和它前后各自有多少头奶牛，利用bit1和bit2得到的两个和快速的算出它到剩余所有奶牛的距离。之后在bit中减去它的位置和吼声，并修改数组相应的值。


## Points in solving
代码如下：

```c++
#include<stdio.h>
#include<stdlib.h>
#include<algorithm>
using namespace std;
int bit1[40005]={0};
int bit2[40005]={0};
int bit3[40005]={0};
int bit4[40005]={0};
int n,maxh=-100,minh=2147483647;
long long sum2=0;
struct node
{
	int h;
	int p;
}a[20005]={0},b[20005]={0},c[20005]={0};
bool cmp(node q,node p)
{
	return q.h>p.h;
}
bool cmp2(node q,node p)
{
	return q.h<p.h;
}
void add2(int *b,int i,int v)
{
	
	while(i<=maxh)
	{
		b[i]+=v;
		i+=i&-i;
	}
}
int sum (int *b,int i)
{
	
	int s=0;
	while(i>0)
	{
		s+=b[i];
		i-=i&-i;
	}
	return s;
}
int main()
{	
	int i,j;
	scanf("%d",&n);
	for(i = 1;i <= n;i++)
	{
		scanf("%d",&a[i].p);
		scanf("%d",&a[i].h);	
		if(maxh<a[i].h)
			maxh=a[i].h;
		if(minh>a[i].h)
			minh=a[i].h;
		b[i].h=a[i].p;
		b[i].p=i;//b.p:编号，a.h：距离
		c[i].h=a[i].h;
		c[i].p=a[i].p; 
	}
	sort(b+1,b+n+1,cmp);
	sort(c+1,c+n+1,cmp2);	
	for(i=1;i<=n;i++)
	{
		add2(bit1,c[i].h,c[i].h);
		add2(bit2,maxh-c[n-i+1].h+1,maxh-c[n-i+1].h);//bit1:前缀和 bit2:后缀和 
		add2(bit3,c[i].h,1);	
		add2(bit4,maxh-c[i].h+1,1);
	}
	for(i=1;i<n;i++)
	{
		int before=sum(bit3,a[b[i].p].h)-1;
		int after=sum(bit4,maxh-a[b[i].p].h+1)-1;
		int val1=a[b[i].p].h;
		int val2=maxh-a[b[i].p].h;
		long long sum3=(before*val1+after*val2-sum(bit1,a[b[i].p].h-1)-sum(bit2,maxh-a[b[i].p].h));
		sum2+=sum3*(a[b[i].p].p);
		add2(bit3,a[b[i].p].h,-1);	
		add2(bit4,maxh-a[b[i].p].h+1,-1);	
		add2(bit1,a[b[i].p].h,a[b[i].p].h*(-1));
		add2(bit2,maxh-a[b[i].p].h+1,(maxh-a[b[i].p].h)*(-1));
	}
	printf("%I64d",sum2);
	return 0;
}
```

## Warnings

这个题数据比较大，求和要用long long，另外$一定$要注意树状数组的下标从1开始，因为位运算设置使然，不然的话会死循环。
