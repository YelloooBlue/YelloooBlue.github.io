---
title: 如何让小爱同学控制一颗LED_基于ESP8266_NodeMCU
author: YelloooBlue
date: 2020-11-27 14:33:00 +0800
categories: [博客, 小实验]
tags: [ESP8266, IOT, NodeMCU, 小爱同学]
math: true
image: /assets/img/Blog/2020-11-27/NodeMCU.jpg
---



# 一、准备：

1.一块刷好 NodeMCU 固件的ESP8266
<br>2.一台装好 Arduino IDE 的电脑
<br>3.给 Arduino IDE 配置 NodeMCU 支持
<br>4.良好的 2.4G WIFI 网络（无需登录） 
<i><br>（以上内容具体教程留意后续博客哦）</i>

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

