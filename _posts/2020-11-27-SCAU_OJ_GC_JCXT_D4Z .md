---
title: SCAU程序设计在线实训平台_实验_高级语言程序设计_教材习题_第四章
author: YelloooBlue
date: 2020-11-27 15:40:00 +0800
categories: [博客, 编程题]
tags: [SCAU, OJ, 高级语言程序设计, C语言]
math: true
image: 
---


### 1、计算分段函数值（题目编号：18042）：

#### 描述：
	根据如下数学公式，编写程序输入x，计算并输出y的值，保留两位小数

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201126174017158.png#pic_center)


#### 输入格式：
	输入一个实数x

#### 输出格式：
	输出函数值

#### 输入样例：
	0

#### 输出样例：
	0.00
    
#### 代码实现（参考）：
```c
#include <stdio.h>
double x;
double F(double x)
{
    if(x<1)
        return x;
    else if(1<=x&&x<10)
        return 2*x-1;
    else if(x>=10)
        return 3*x-11;
}
int main(){
    scanf("%lf",&x);
    printf("%.2lf",F(x));
    return 0;
}
```



### 2、找出3个数中最大的数（题目编号：18043）：

#### 描述：
	编写程序，由键盘输入3个整数，输出其中最大的数。

#### 输入格式：
	三个整数，空格分隔

#### 输出格式：
	最大的数

#### 输入样例：
	3 6 4

#### 输出样例：
	6

#### 代码实现（参考）：
```c
#include <stdio.h>
int a,b,c,m;

int main(){
    scanf("%d%d%d",&a,&b,&c);
    if(a>b)m=a;
    if(c>a)m=c;
    if(b>c&&b>a)m=b;
    printf("%d",m);
    return 0;
}
```



### 3、成绩等级评分（题目编号：18044）：

#### 描述：
	编写程序，由键盘输入一个百分制的整数成绩，要求输出对应的成绩等级。90分以上为		A，80到89分为B，70到79分为C，60到69分为D，60分以下为E。成绩不在0到100之间时输出“error”

#### 输入格式：
	一个整数成绩

#### 输出格式：
	输出对应的等级或error

#### 输入样例：
	99

#### 输出样例：
	A

#### 代码实现（参考）：
```c
#include <stdio.h>
int a;
int main(){
    scanf("%d",&a);
    if(a>=90&&a<=100)printf("A");
    else if(a>=80&&a<90)printf("B");
    else if(a>=70&&a<80)printf("C");
    else if(a>=60&&a<70)printf("D");
    else if(a>=0&&a<60)printf("E");
    else printf("error");
    return 0;
}
```



### 4、前一个和后一个字符（题目编号：18045）：

#### 描述：
	编写程序，输入一个数字字符，输出其前一个和后一个的数字字符，如果输入的是0前一个输出“first”，9后一个则输出“last”，输入的不是数学字符，输出“error”

#### 输入格式：
	一个字符

#### 输出格式：
	输出结果

#### 输入样例：
	0

#### 输出样例：
	first 1

#### 代码实现（参考）：
```c
#include <stdio.h>
char a;
int main(){
    scanf("%c",&a);
    if(a>=48&&a<=57){
        if(a==48){
            printf("first ");
            printf("1");
        }
        else if(a==57){
            printf("8 ");
            printf("last");
        }
        else{
            printf("%c ",a-1);
            printf("%c",a+1);
        }

    }
    else printf("error");
    return 0;
}
