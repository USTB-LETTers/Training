
# LETTers Solution Report

- Date: 6 April 2018
- Author: WGM
- Problem ID: [HDU - 5237](http://acm.hdu.edu.cn/showproblem.php?pid=5237)

## Description modeling

对字符串s，逐位取ascii码，如果长度不能被6整除，就在末尾补0，即ascii乘2的幂；是二进制的6位是十进制64，就对ascii码的十进制数对64取余，转换成64进制，再用64整除，用于下一位的计算；如果当前位数小于6，就要再取s中的下一个字符转ascii，再调整位数，最后同样是%64、64；全部转换完，如果长度不能被4整除，就在末尾补‘=’号；

将以上过程写成函数，对全局变量字符串s进行操作，执行k次函数即可；

## Points in solving

二进制位右补n个0，对应十进制的操作是乘2的n次幂；
可以数一下位数，初步判断答案有没有错误；
‘=’号的ascii码是61；

## Warnings

每执行一次，都要判断要不要补‘=’号，而不是只在最终结果处；
对于右边补位的情况，习惯性从右边开始操作，实际上这题从左从右都可以；
使用strcpy时，最好先把被赋值的字符串清零；

