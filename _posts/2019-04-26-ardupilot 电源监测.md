---
layout:     post
title:      ardupilot 电源监测
subtitle:   看懂这些，有助于给飞机做好低电保护
date:       2019-04-26
author:     Sugar
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - ardupilot
    - ArduPilotLog
    - 少儿编程
    - 初中物理
---

电源监测理论基础
---
1. 分压电路
![分压电路](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/voltage_dividing_circuit_1.jpg)
2. 串联电路与欧姆定律
![串联电路与欧姆定律](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/voltage_dividing_circuit_2.jpg)

ardupilot 中的模拟量电源监测
---
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/volt_current_1.png)
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/volt_current_2.png)
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/volt_current_3.png)
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/volt_current_4.png)
> 1. 下图中的**分压比**就是`电源监测理论基础`部分的`(R1+R2)/R2`<br>
> 2. 参数`BATT_VOLT_MULT`表示**分压比**，其值与硬件相关。

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/volt_current_5.png)
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/volt_current_6.png)

[ArduPilotLog](https://github.com/SuWeipeng/ArduPilotLog)出场
---
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/volt_current_13.png)

[ArduPilotLog](https://github.com/SuWeipeng/ArduPilotLog)退场，[MATLAB](https://github.com/SuWeipeng/ArduPilotLog/tree/master/matlab)登场
---
* MATLAB 登场方法
> 详见[ArduPilotLog开源说明](https://github.com/SuWeipeng/ArduPilotLog)
> [下载链接]https://pan.baidu.com/s/1hwnQ6RL8s9tQwfO6Shs_Xw 
> 提取码：x0iv 

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/ardupilotlog_1.png)
* 一些简单的分析
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/volt_current_14.png)
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/volt_current_15.png)
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/volt_current_16.png)
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/lowpass_filter_4.png)

分析过后，我们知道
---
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/volt_current_17.png)

篇末总结
---
1. 新时代的学习方法
![](https://github.com/SuWeipeng/img/raw/master/9_mind/mind_1.png)
2. 通过简单的示例介绍了 [ArduPilotLog](https://github.com/SuWeipeng/ArduPilotLog) 将数据导入 [MATLAB](https://github.com/SuWeipeng/ArduPilotLog/tree/master/matlab) 进一步分析的方法。
3. 展示了编程有什么用。

一点点感慨
---
作者高中时学的知识，现在都降到初中了。对于孩子们来讲，小脑袋里要装更多的东西才有可能跟上当下的发展。<br>
孩子上了初中的家长，如何把当初自己高中的知识装到当下自己孩子只有初中年龄的小脑袋里？这是个必须马上解决的问题。<br>
孩子还小的家长，不得不说要考虑的更多，未来可能面对的是“如何将自己当初高中学的知识装到只有小学年龄的小脑袋里”的问题。<br>

请我喝杯咖啡如何？
---
微信
![weixinfukuan](https://github.com/SuWeipeng/img/raw/master/weixinfukuan.jpg)
支付宝
![zhifubaofukuan](https://github.com/SuWeipeng/img/raw/master/zhifubaofukuan.jpg)

微信好友
---
![weixinhaoyou](https://github.com/SuWeipeng/img/raw/master/weixinhaoyou.png)
