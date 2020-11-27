---
title: SCAU程序设计在线实训平台_实验_高级语言程序设计_实验7.数组的应用
author: YelloooBlue
date: 2020-11-27 15:40:00 +0800
categories: [博客, 编程题]
tags: [SCAU, OJ, 高级语言程序设计, C语言]
math: true
image: 
---


# 实验7.数组的应用

## 单元测试：

### 1、打印杨辉三角：

#### 描述：

	由键盘输入正数n（n<30），要求输出具有n行的杨辉三角。

#### 输入样例：

	5

#### 输出样例：

	1
	1,1
	1,2,1
	1,3,3,1

#### 代码实现（参考）：

```c
#include <stdio.h>

int main()
{
    int n, sz[30][30];
    scanf("%d", &n);
    for (int i = 0; i < n; i++){
        if(i == 0){
            sz[0][0] = 1;
            printf("1\n");
            continue;
        }
        if(i <= 1){
            sz[1][0] = 1;
            sz[1][1] = 1;
            printf("1,1\n");
            continue;
        }

        for(int j = 1;j < i; j++){
            sz[i][j] = sz[i-1][j] + sz[i-1][j-1];
            sz[i][0]=1;
            sz[i][i]=1;
        }

        for(int k = 0; k <= i; k++){
            printf("%d,", sz[i][k]);
        }
        printf("\n");
    }

}
```
