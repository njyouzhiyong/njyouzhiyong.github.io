---
layout:     post
title:      arducopter 定高算法梳理
subtitle:   文中展现的研究方法比内容本身更宝贵
date:       2019-05-08
author:     Sugar
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - ardupilot
    - ArduPilotLog
    - arducopter
    - MALAB
    - 研究方法
---

> 本文并主旨不在算法，意在表现一些研究方法：<br>
> 1. 跟着控制框图理代码的方法<br>
> 2. 用数据佐证判断的方法<br>
> 3. 用 MATLAB 快速成现简单算法效果的方法<br>
> 4. 展示数据时实采样与非时实采样的差别<br>
> 5. 了解 arducopter 定高相关有哪些参数，各是什么作用。

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/copter_alt_control_1.png)

控制过程梳理
---
* 从高度开始（位置环）

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_P.png)

> 代码截图<br>
> ![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_P_code.png)


* 速度控制过程（速度环）

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_V_1.png)

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_V_2.png)

> 代码截图<br>
> ![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_V_code.png)

* 终到加速度控制（加速度环）
> 这里用到`set_input_filter_all`控制器，有关这个控制器以前在[arducopter 低通滤波与D控制器解耦合](https://suweipeng.github.io/2019/04/22/arducopter-%E4%BD%8E%E9%80%9A%E6%BB%A4%E6%B3%A2%E4%B8%8ED%E6%8E%A7%E5%88%B6%E5%99%A8%E8%A7%A3%E8%80%A6%E5%90%88/)中介绍过。

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_A_PID.png)

1. 时实采样看跟踪效果

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_A_1.png)

2. 非实时采样看跟踪效果

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_A_2.png)

3. 评价参数效果
> 想要调好参数，首先要对当前的参数效果有个主观评价。<br>
> 这有利于接下来寻找参数的调整方向。

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_A_4.png)

> 代码截图<br>
> ![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_A_code.png)

* 时实采样数据与非时实采样数据对比

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_A_3.png)

* 用好 MATLAB 的便利

> 上面提到一个 `sqrt_controller` 译成普通话是`开方控制器`<br>
> 有关开方控制器的更多信息，请点击[ ZingHD 的博文链接](https://zinghd.gitee.io/sqrt_controller-lean_angles_to_accel/)

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_to_matlab_method.png)

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_to_matlab_method_1.png)

篇末提示
---
1. 数据怎样进入 MATLAB 的，请看[ArduPilotLog开源说明](https://github.com/SuWeipeng/ArduPilotLog)。
2. 支持 MATLAB 的版本是[ v1.01](https://github.com/SuWeipeng/ArduPilotLog/releases)，[百度网盘链接](https://pan.baidu.com/s/1hwnQ6RL8s9tQwfO6Shs_Xw)，提取码：x0iv 

请我喝杯咖啡如何？
---
微信
![weixinfukuan](https://github.com/SuWeipeng/img/raw/master/weixinfukuan.jpg)
支付宝
![zhifubaofukuan](https://github.com/SuWeipeng/img/raw/master/zhifubaofukuan.jpg)

微信好友
---
![weixinhaoyou](https://github.com/SuWeipeng/img/raw/master/weixinhaoyou.png)
