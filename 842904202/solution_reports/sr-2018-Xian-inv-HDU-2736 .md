# LETTers Solution Report

- Date: 7 April 2018
- Author: Alice_Margatroid
- Problem ID: [HDU-2736](http://codeforces.com/problemset/problem/616/B)

## Description modeling

字符串处理，在j从0——n-1的所有情况中如果存在（s[i1]，s[i1+j]）和（s[i2]，s[i2+j]）完全相等那么这个字符串就不amazing。


## Points in solving

直接做就好

```c++
#include <bits/stdc++.h>
using namespace std;
char s[85]={0};
int via[800]={0};
int main() 
{
	int i,j,n,k,sum=0,max1=-100,pd;
	while(scanf("%s",&s)&&s[0]!='*')
	{
		memset(via,0,sizeof(via));
		pd=1;
		int len=strlen(s);
		for(i=0;i<len;i++)
		{
			for(j=0;j<len-i-1;j++)
			{
				if(via[(s[j]-'A')*26+s[j+i+1]-'A']==0)
					via[(s[j]-'A')*26+s[j+i+1]-'A']=1;
				else
					pd=0;		
			}
			for(j=0;j<800;j++)
				via[j]=0;
		}
		if(pd)
			printf("%s is surprising.\n",s);
		else
			printf("%s is NOT surprising.\n",s);
	}
	return 0;
}
```
## Warnings

暂无。
