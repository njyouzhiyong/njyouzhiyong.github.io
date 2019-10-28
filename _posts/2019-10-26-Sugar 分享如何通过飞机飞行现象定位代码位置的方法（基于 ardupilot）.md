---
layout:     post
title:      跟着 ardupilot 学 C++ 系列之友元
subtitle:   C++ 基础系列推文
date:       2019-10-26
author:     Sugar
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - ardupilot
    - arducopter
    - C++
    - 静态成员
---

> 背景介绍：      
> Sugar 在调试带 VL53L1X 激光测距模块的小六轴时一直有一个现象觉得挺别扭：飞机在自动定高的模式下，飞到一定高度，再用遥控推油门飞机就不往上飞了。       
> 咋回事儿呢？Sugar 平时比较忙，没啥时间玩儿飞机。今天特意抽个时间把这个疑惑解开。      
> 关于定高，Sugar 之前写过 3 篇推文：     
> [《arducopter 定高算法梳理》](https://mp.weixin.qq.com/s/bVzmtRRUYL1meLVLLSd5tg)     
> [《arducopter 前馈分析》](https://mp.weixin.qq.com/s/lNj7KqciicuPRF8c7vaUIQ)
> [《arducopter 高度控制前馈处理》](https://mp.weixin.qq.com/s/h6WpcEmkOUpIwobqNDC3Vg)        
> 正好趁这个机会，把目前官方 master 分支最新（2019年10月23日）的定高代码完整的理一遍。     
> 本文 Sugar 着重表现如何依据现象锁定代码位置的方法。     

ArduPilotLog 呈现一下这个别扭的现象
---
公众号内回 ArduPilotLog 获得 Sugar 最近更新的 ArduPilotLog 软件下载地址和 github 开源地址。      
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/althold_q1.jpg)      

就这个现象，看代码该怎么下手啊？
---
通过上一篇[《跟着 ardupilot 学 C++ 系列之类的静态成员》](https://mp.weixin.qq.com/s/brPsgi6Bkn9FmoXG8M-ezQ)中有关“状态机”的介绍，再配合一点点经验，就可以马上锁定目标代码泛围。           
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/FSM_3.jpg)       

一点点经验都包括哪些呢？
---        
1、定高算法的完整控制框图     
（依据 run_z_controller() 函数绘制）
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/AltHold_p2v.jpg)        
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/AltHold_v2a.jpg)        
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/AltHold_a.jpg)       
2、set_alt_target_from_climb_rate_ff() 函数的 3 个作用：     
(1) 对遥控给出的目标速度做平滑处理；
(2) 平滑处理后的目标速度赋给 _vel_desired.z；       
(3) 用 _vel_desired.z 对 dt 的积分推进 _pos_target.z。       
3、用 ArduPilotLog 仔细看一下数据       
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/AltHold_q2.jpg)       

按上面线索，开始下手翻代码
---
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/AltHold_code1.jpg)        
通过上面分析，目前有两个结论：      
1、问题发生在 Flying 状态下；      
2、set_alt_target_from_climb_rate_ff()的速度形参收到的参数是零。     
按这两个结论，去看一下 mode_althold.cpp ，如下：       
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/AltHold_code2.jpg)          
至此，问题就被爆力解决了。

PS
---
Sugar 这次的做法其实是爆力干掉了最新代码里高度上的 surface_tracking 和 avoidance 功能。      
ardupilot 代码一直很灵活，一直在变动，一直在加功能改功能。这两个被 Sugar 干掉的功能应该可以用参数配置停掉（基于经验判断），Sugar 不想细推这部分相关代码，在了解架构的前提下直接注释掉了。       
如果读者也跟 Sugar 一样对某些新加的功能觉得不对胃口，在看得懂代码的前提下就可以放心大胆的干掉这些用不上的功能。     
Sugar 这篇推文着重体现了如何锁定目标代码的方法，希望能对读者有一定帮助和启发。
为了写这篇有关定高模式的文章，前面 Sugar 有做四篇基础铺垫，分别是：     
[《跟着 ardupilot 学 C++ 系列之多态》](https://mp.weixin.qq.com/s/ixhfR7zmlFlsUV7m6zy0Yg)           
[《跟着 ardupilot 学 C++ 系列之友元》](https://mp.weixin.qq.com/s/g52zaKy8vcVGxstmwfSb-A)      
[《跟着 ardupilot 学 C++ 系列之类和对象》](https://mp.weixin.qq.com/s/g52zaKy8vcVGxstmwfSb-A)        
[《跟着 ardupilot 学 C++ 系列之类的静态成员》](https://mp.weixin.qq.com/s/brPsgi6Bkn9FmoXG8M-ezQ)

关注作者
---
欢迎扫码关注我的公众号`MultiMCU EDU`。     
![](https://github.com/SuWeipeng/img/raw/master/gongzonghao.jpg)      
### `提示：在公众号“关于我”页面可加作者微信好友。`
### `喜欢本文求点赞，有打赏我会更有动力。`



请我喝杯咖啡如何？
---
微信
![weixinfukuan](https://github.com/SuWeipeng/img/raw/master/weixinfukuan.jpg)
支付宝
![zhifubaofukuan](https://github.com/SuWeipeng/img/raw/master/zhifubaofukuan.jpg)