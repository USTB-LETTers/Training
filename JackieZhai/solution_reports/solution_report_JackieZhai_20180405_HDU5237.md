# LETTers Solution Report

- Date: 2 April 2018
- Author: JackieZhai
- Problem ID: [HDU5237](http://acm.hdu.edu.cn/showproblem.php?pid=5237)

## Description modeling

- 先将文字转换为ASCII的二进制
- 24个bit一个组，先把整组的转换了
- 有余的只有两种情况：8和16，分别进行特殊处理即可

```c++
//由二进制进行转换成秘钥的过程
    string ans;
    int anspoint=0;
    int group=tra.size()/24;
    int resor=tra.size()%24;
    for(int i=0; i<group; i++)
    {
        int code[4];
        for(int j=0; j<4; j++)
        {
            code[j]=0;
            for(int k=0; k<6; k++)
            {
                code[j]+=tra[i*24+j*6+k]*pow(2, (6-k-1));
            }
            ans.push_back(pic[code[j]]);
        }
    }
    if(resor==8)
    {
        int ad1=0, ad2=0;
        for(int i=0; i<6; i++)
        {
            ad1+=tra[group*24+i]*pow(2, (6-i-1));
        }
        ans.push_back(pic[ad1]);
        for(int i=0; i<2; i++)
        {
            ad2+=tra[group*24+6+i]*pow(2, (6-i-1));
        }
        ans.push_back(pic[ad2]);
        ans.push_back('=');
        ans.push_back('=');
    }
    else if(resor==16)
    {
        int ad1=0, ad2=0, ad3=0;
        for(int i=0; i<6; i++)
        {
            ad1+=tra[group*24+i]*pow(2, (6-i-1));
        }
        ans.push_back(pic[ad1]);
        for(int i=0; i<6; i++)
        {
            ad2+=tra[group*24+6+i]*pow(2, (6-i-1));
        }
        ans.push_back(pic[ad2]);
        for(int i=0; i<4; i++)
        {
            ad3+=tra[group*24+12+i]*pow(2, (6-i-1));
        }
        ans.push_back(pic[ad3]);
        ans.push_back('=');
    }
```

## Points in solving

- 做一个函数，输入输出都是string，这样就可以循环求解密码了（不过这样有TLE的隐患）

## Warnings

- 这种题真的很费时间，要Debug很多次
