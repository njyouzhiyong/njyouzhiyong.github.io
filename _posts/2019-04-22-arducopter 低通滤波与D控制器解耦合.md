---
layout:     post
title:      arducopter 低通滤波与D控制器解耦合
subtitle:   解决 arducopter 的一个陈年老 BUG
date:       2019-04-22
author:     Sugar
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - arducopter
    - ardupilot
    - 低通滤波
---

> 这是一篇多图文章，简单易懂不烧脑

调试 arducopter 参数的时候，是否遇到过这样的问题：D值已经调很大了，怎么不起作用？<br>
原因：`“低通滤波”与“D控制器”耦合了！`

怎么耦合的？该怎么解耦合？
---
![set_input_filter_all_1](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/set_input_filter_all_1.png)

看不懂代码就看图示
---
![lowpass_filter_3](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/lowpass_filter_3.png)

耦合了会怎么样
---
1. 先看下低通滤波的表达式<br>
![lowpass_filter_1](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/lowpass_filter_1.png)
2. 关键在于阿尔法（alpha）<br>
![lowpass_filter_2](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/lowpass_filter_2.png)
> 由此可见，在arducopter默认参数下的耦合效果是：
> 1. ATC_RAT_YAW_D 被削减为原值的 3.78%
> 2. 调低通滤波参数“XXX_FILT”会影响到D控制器的输出

修改后是什么效果
---
> 图用跨平台绘图软件 [ArduPilotLog](https://github.com/SuWeipeng/ArduPilotLog) 绘出

![set_input_filter_all_2](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/set_input_filter_all_2.png)<br>
![set_input_filter_all_3](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/set_input_filter_all_3.png)<br>

请我喝杯咖啡如何？
---
![weixinfukuan](https://github.com/SuWeipeng/img/raw/master/weixinfukuan.jpg)
![zhifubaofukuan](https://github.com/SuWeipeng/img/raw/master/zhifubaofukuan.jpg)

微信好友
---
![weixinhaoyou](https://github.com/SuWeipeng/img/raw/master/weixinhaoyou.png)<br>
