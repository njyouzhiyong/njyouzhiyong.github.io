---
layout:     post
title:      arducopter 前馈分析
subtitle:   “代码截图”部分说明本文足够简单
date:       2019-05-11
author:     Sugar
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - ardupilot
    - ArduPilotLog
    - arducopter
    - feed forward
    - 前馈
---

> 本文对上一篇[ arducopter 定高算法梳理 ](https://suweipeng.github.io/2019/05/08/arducopter-%E5%AE%9A%E9%AB%98%E7%AE%97%E6%B3%95%E6%A2%B3%E7%90%86/)曾抛出的问题进行解答。

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_ff_v_1.png)

原理分析
---
* 目标位置的改变 `(常规算法)`

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_ff_v_5.png)

* 定高控制 `(常规算法)`

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_ff_v_4.png)

* 快速响应输入 `(前馈作用)`

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_ff_v_3.png)

数据佐证
---
> 数据表明前馈作用是非常明显的。通过数据可知：如果在目标速度上减去前馈，那输入的反应一定会慢很多。

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_ff_v_2.png)

代码截图
---
> 这里有点搞笑了，上面说的那么多，到代码上就三行。

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_ff_v_code.png)

篇末提示
---
* ArduPilotLog 开源地址[点此链接](https://github.com/SuWeipeng/ArduPilotLog)，[ v1.0.1](https://github.com/SuWeipeng/ArduPilotLog/releases)下载：[百度网盘链接](https://pan.baidu.com/s/1hwnQ6RL8s9tQwfO6Shs_Xw)，提取码：x0iv 

请我喝杯咖啡如何？
---
微信
![weixinfukuan](https://github.com/SuWeipeng/img/raw/master/weixinfukuan.jpg)
支付宝
![zhifubaofukuan](https://github.com/SuWeipeng/img/raw/master/zhifubaofukuan.jpg)

微信好友
---
![weixinhaoyou](https://github.com/SuWeipeng/img/raw/master/weixinhaoyou.png)



