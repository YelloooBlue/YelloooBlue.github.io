---
<<<<<<< HEAD
title: 如何让小爱同学控制一颗LED_基于ESP8266_NodeMCU
author: YelloooBlue
date: 2020-11-27 14:33:00 +0800
categories: [博客, 小实验]
tags: [ESP8266, IOT, NodeMCU, 小爱同学]
=======
title: 第一篇博客
author: YelloooBlue
date: 2020-11-22 11:33:00 +0800
categories: [Blogging, Demo]
tags: [感想]
>>>>>>> 1d8b6a1ad5819cc3de4a993548b4223ed21a9c2b
math: true
image: /assets/img/Blog/2020-11-27/NodeMCU.jpg
---



<<<<<<< HEAD
# 一、准备：

1.一块刷好 NodeMCU 固件的ESP8266
<br>2.一台装好 Arduino IDE 的电脑
<br>3.给 Arduino IDE 配置 NodeMCU 支持
<br>4.良好的 2.4G WIFI 网络（无需登录） 
<i><br>（以上内容具体教程留意后续博客哦）</i>
=======

## 标题

---

# 一级标题

<h2 data-toc-skip>学习markdown中</h2>

<h3 data-toc-skip>H3</h3>

<h4>H4</h4>

---

##段落

I wandered lonely as a cloud

That floats on high o'er vales and hills,

When all at once I saw a crowd,

A host, of golden daffodils;

Beside the lake, beneath the trees,

Fluttering and dancing in the breeze.

## 列表

### 排序列表

1. first item
2. second item
3. third item

###不排序列表

- item 1
	- sub item 1
	- sub item 2

- item 2

## 引用

> This line to shows the Block Quote.

## 表格

| Company                      | contact          | Country |
|:-----------------------------|:-----------------|--------:|
| Alfreds Futterkiste          | Maria Anders     | Germany |
| Island Trading               | Helen Bennett    | UK      |
| Magazzini Alimentari Riuniti | Giovanni Rovelli | Italy   |

## 超链接

<http://acm.scau.edu.cn:8000>


## Footnote

Click the hook will locate the footnote[^footnote].


## 图像

By default, the image is centered and the image caption can be displayed at the 按钮:

![Desktop View](/assets/img/sample/mockup.png)
_Full screen width and center alignment_

You can change the size of the picture:
>>>>>>> 1d8b6a1ad5819cc3de4a993548b4223ed21a9c2b

# 二、开整：
## 1. 下载点灯科技Blinker APP：
<https://www.diandeng.tech/>
## 2. 注册点灯科技Blinker账号：
## 3. 添加设备：
<image src="../assets/img/Blog/2020-11-27/Blinker_APP1.jpg">
独立设备-->WIFI接入-->阿里云-->获取Secret Key

## 4. 编写硬件程序：

```
#define BLINKER_WIFI  //点灯科技
#define BLINKER_MIOT_LIGHT  //小爱同学支持  
#define LED_BUILTIN 16  //LED引脚
#include <Blinker.h>  //点灯科技

char auth[] = "这里改成刚刚获取的Secret Key（保留双引号)";
char ssid[] = "这里改成你的wifi名称（保留双引号）";
char pswd[] = "这里改成你的wifi密码（保留双引号）";

// 新建组件对象
BlinkerButton Button1("btn-LED");   //新建一个按钮，数据键名为btn-LED，这个可以自定义



// 按下btn-LED按键即会执行该函数

void button1_callback(const String & state) {
    BLINKER_LOG("get button state: ", state);
    digitalWrite(LED_BUILTIN, !digitalRead(LED_BUILTIN));   //LED状态取反
    Blinker.vibrate();
}



void miotPowerState(const String & state)   //小爱同学状态返回函数
{  
    BLINKER_LOG("need set power state: ", state);

    if (state == BLINKER_CMD_ON) {
        digitalWrite(LED_BUILTIN, LOW);
        BlinkerMIOT.powerState("on");
        BlinkerMIOT.print();
    }
    else if (state == BLINKER_CMD_OFF) {
        digitalWrite(LED_BUILTIN, HIGH);
        BlinkerMIOT.powerState("off");
        BlinkerMIOT.print();
    }
}

void setup() {
   // 初始化串口
    Serial.begin(9600);
    BLINKER_DEBUG.stream(Serial);
    BLINKER_DEBUG.debugAll();
    pinMode(LED_BUILTIN, OUTPUT);   // 初始化LED的IO
    digitalWrite(LED_BUILTIN, HIGH);
    Blinker.begin(auth, ssid, pswd);    // 初始化blinker
    Button1.attach(button1_callback);       //绑定按钮回调函数
    BlinkerMIOT.attachPowerState(miotPowerState);     //绑定小爱同学状态回调函数
}

void loop() {
    Blinker.run();    //运行
}
```


## 5. APP添加控制组件
<image src="../assets/img/Blog/2020-11-27/Blinker_APP2.jpg">
<image src="../assets/img/Blog/2020-11-27/Blinker_APP3.jpg">
<b>注意这里的数据键名要与程序中一致</b>

