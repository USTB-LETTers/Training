# LETTers Solution Report

- Date: 6 April 2018
- Author: JackieZhai
- Problem ID: [HDU5241](http://acm.hdu.edu.cn/showproblem.php?pid=5241)

## Description modeling

- 由于最长关系链是有5个成员，所以情况数是2<sup>5<sup>n</sup></sup>
- 学会一些技巧，看题意是集合相关（保证是2的幂），可以看样例想答案

## Points in solving

- 大数问题，学会用Java代码实现

```java
import java.math.*;
import java.util.Scanner;

public class Main {
	public static void main(String[] args) {
		
		Scanner sca = new Scanner(System.in);
		
		int T;
		T = sca.nextInt();
		for(int kase=1; kase<=T; kase++) {
			System.out.printf("Case #%d: ", kase);
			
			BigInteger b =  new BigInteger("1");
			BigInteger c = new BigInteger("32");
			
			int n = sca.nextInt();
			if(n==0) {
				System.out.println("1");
			} else {
				for(int i=0; i<n; i++)
					b=b.multiply(c);
				System.out.println(b);
			}
		}
	}		
}
```

## Warnings

- 无
