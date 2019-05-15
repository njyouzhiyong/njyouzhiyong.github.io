---
layout:     post
title:      arducopter 高度控制前馈处理
subtitle:   跟 ArduPilot 学习，为 ArduPilot 奉献。
date:       2019-05-15
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

> 在上一篇推文 [arducopter 前馈分析](https://suweipeng.github.io/2019/05/11/arducopter-%E5%89%8D%E9%A6%88%E5%88%86%E6%9E%90/) 中我以速度环为例说了前馈的作用。<br>
> 本文继续关注一下加速度环的前馈。

两个病证
---
* 病证一：前馈太疯狂

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_ff_a_1.png)<br>
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_ff_a_2.png)

* 病证二：低通效果跑偏
> 在 [arducopter 定高算法梳理](https://suweipeng.github.io/2019/05/08/arducopter-%E5%AE%9A%E9%AB%98%E7%AE%97%E6%B3%95%E6%A2%B3%E7%90%86/) 一文中我们知道高度控制在加速度环上有两个低通滤波器。

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_a_d_lowpass_1.png)<br>
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_a_e_lowpass_1.png)

对证下药
---
* 第一服良药：`速效止疯丸`。
> 关于数据如何导入 MATLAB 请看 [ArduPilot 开源说明](https://github.com/SuWeipeng/ArduPilotLog)。<br>
> 这里展示一下 MATLAB 的强大助力。

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_ff_a_3.png)<br>
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_ff_a_4.png)<br>
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_ff_a_5.png)<br>
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_ff_a_6.png)

* 第二服良药：`醒脑明目汤`。
> 理论基础请读者自行搜索关键词：`香农采样定理`。<br>
> 这个错误就像是一名大夫抓着 A 病人的脉，看着 B 病人的脸，一脑子问号：这脉象跟面象对不上啊。。。<br>
> 大夫太累了，赶紧服一剂“醒脑明目汤”定定神就好了。<br>
> `充分展现“实时采样”的重要性。`

* 翠花，上汤
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_a_d_lowpass_code_6.png)<br>
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_a_d_lowpass_code_3.png)

* 药效立杆见影

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_a_d_lowpass_2.png)<br>
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_a_e_lowpass_2.png)

本文代码修正截图
---
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_a_d_lowpass_code_4.png)<br>
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_a_d_lowpass_code_5.png)<br>
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_a_d_lowpass_code_1.png)<br>
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/arducopter_alt_control_a_d_lowpass_code_2.png)

请我喝杯咖啡如何？
---
微信
![weixinfukuan](https://github.com/SuWeipeng/img/raw/master/weixinfukuan.jpg)
支付宝
![zhifubaofukuan](https://github.com/SuWeipeng/img/raw/master/zhifubaofukuan.jpg)

微信好友
---
![weixinhaoyou](https://github.com/SuWeipeng/img/raw/master/weixinhaoyou.png)