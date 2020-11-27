---
title: SCAU程序设计在线实训平台_实验_高级语言程序设计_教材习题_第三章
author: YelloooBlue
date: 2020-11-27 15:40:00 +0800
categories: [博客, 编程题]
tags: [SCAU, OJ, 高级语言程序设计, C语言]
math: true
image: 
---


### 1、分期还款（第三章第4题）：

#### 描述：
	从银行贷款金额为d，准备每月还款额为p，月利率为r。
	请编写程序输入这三个数值，算并输出多少个月能够还清贷款，
	输出时保留1位小数。如果无法还清，请输出“God”计算公式如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201126172937548.png#pic_center)


#### 输入格式：
	三个数，分别为货款金额、每月还款和月利率，以空格分隔，均为非负数，其中d，p，r>=0

#### 输出格式：
	需要还款的月份

#### 输入样例：
	50 50 0.01

#### 输出样例：
	1.0

#### 代码实现（参考）：
```c
#include <stdio.h>
#include <math.h>
double p,d,r,m;
int main()
{
    scanf("%lf %lf %lf",&d,&p,&r);

    if(d==0)
        printf("0.0\n");
    else if(d*(1+r)-p>d)
        printf("God\n");
    else
    {
    m=log10(p/(p-d*r))/log10(1+r);
    printf("%.1lf",m);
    }
    return 0;
}
```

