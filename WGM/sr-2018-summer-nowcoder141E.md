
# LETTers Solution Report

- Date: 27 July 2018
- Author: WGM
- Problem ID: [nowcoder - 141E](https://www.nowcoder.com/acm/contest/141/E)

## Description modeling

- 便于理解先倍增处理，S_i就是S[i]~S[i+N]。假设S_i=S_j就有S[i] S[i+1] S[i+2] …… S[j-1]与S[j] S[j+1] S[j+2] …… S[2] * j-1-i]相等，那将相等的这两部分去掉 就有S_{j}=S_{2 * j-i}。同理，多次处理即可得出每个部分相同。故存在S_i=S_j的充要条件是原字符串中存在长度为i-j整数倍的循环节。判断循环节即可
- 举例
    长度为6的字符串倍增后：0 1 2 3 4 5 6 7 8 9 10 11 
    如果S_2=S_5，首先有S[2]、S[3]、S[4]=S[5]、S[6]、S[7]，同时又有S[5]、S[6]、S[7]=S[8]、S[9]、S[10]，最终可以得到存在长度为3的循环节。

## Points in solving

题目要求是字典序，其实答案中没有重复值，并且只要从左到右遍历就已经是字典序了。

## Warnings

- 优化：字符串长度一定可以被循环节长度整除。
- 循环节长度最长为len/2,可以取到；但是判断是否是循环节遍历应该是到len/2-1,取不到len/2，否则判断时下标会溢出。

## Codes

```c++
 #include<bits/stdc++.h>
using namespace std;

char s[1000007];
int main()
{
	int i,j,flag=0,flag2=0,ans=0;
	scanf("%s",&s);
	int len=strlen(s);
	for(i=1;i<=len/2;i++)
	{
		if(len%i!=0)
			continue;	
		flag=1;
		for(j=0;j<len/2;j++)
		{
			if(s[j]!=s[j+i])
			{
				flag=0;
				break;
			}
		}
		if(flag==1)
		{	
			flag2=1;
			break;
		}
	}
	ans=i;
	if(flag2)
	{
		printf("%d\n",ans);
		for(i=0;i<ans;i++)
		{
			printf("%d ",len/ans);
			for(j=i;j<len;j+=ans)
				printf("%d ",j);
			printf("\n");
		}
	}
	else
	{
		printf("%d\n",len);
		for(i=0;i<len;i++)
		{
			printf("1 %d\n",i);
		}
	}
	return 0;
}

```
