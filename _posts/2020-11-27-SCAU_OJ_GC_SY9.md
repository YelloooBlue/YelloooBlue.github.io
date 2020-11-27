---
title: SCAU程序设计在线实训平台_实验_高级语言程序设计_实验9.函数的应用
author: YelloooBlue
date: 2020-11-27 15:40:00 +0800
categories: [博客, 编程题]
tags: [SCAU, OJ, 高级语言程序设计, C语言]
math: true
image: 
---


# 实验7.数组的应用
## 单元测试：
### 1、求函数值：
#### 描述：
	输入x(x为整数)，求函数值
	函数定义如下：
	F(x)=x          	         x小于3
	F(x)=F(x/3)*2   	         x大于等于3且x为3的倍数
	F(x)=F((x-1)/3)+1   	x大于等于3且x除3余1
	F(x)=F((x-2)/3)+2   	x大于等于3且x除3余2
#### 输入格式：
	一个整数
#### 输出格式：
	结果
#### 输入样例：
	20
#### 输出样例：
	6
#### 代码实现（参考）：
```c
#include <stdio.h>

int x;
int F(int x)
{
    if( x < 3 ) return x;
    else{
        int r=x%3;
        switch(r)
            {
            case 0:
                return F(x/3)*2;
            case 1:
                return F((x-1)/3)+1;
            case 2:
                return F((x-2)/3)+2;
            default:
                break;
        }
    }
}
int main()
{
    scanf("%d",&x);
    printf("%d",F(x));
}
```