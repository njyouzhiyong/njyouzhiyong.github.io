---
layout:     post
title:      跟着 ardupilot 学 C++ 系列之类和对象
subtitle:   C++ 基础系列推文
date:       2019-10-14
author:     Sugar
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - ardupilot
    - arducopter
    - C++
    - 类
    - 对象
---

> 背景介绍：     
> 买了 Sugar 做的麦轮车的朋友表示自己飞飞机是美国手，用 Sugar 配的遥控不习惯。      
> 是的呢，因为 Sugar 玩飞机是日本手。     
> 下面说说美国手、日本手在玩麦轮车上的什么差别，以及要换手的话该怎样改程序。     
> 重点说一说怎样从生活的角度理解 C++ 最基本的概念“类和对象”。

摇杆通道
---
> x 控前后平移     
> y 控左右平移
> z 控平面旋转

![](https://github.com/SuWeipeng/img/raw/master/13_car/rc_chan_1.jpg)     
上图中的 ADC 通道缓冲区，是 Sugar 写的遥控器代码里的，如下图：     
![](https://github.com/SuWeipeng/img/raw/master/13_car/fire_rc_1.jpg)     
不难看出，因为麦轮车能够横向平移的特点，其控制与多旋翼飞机比，仅少了一个油门通道（图中标“空”的在多旋翼飞机里就是油门）。所以，相比于其他种类的模型车，美国手、日本手的差别就比较明显（主要体现在前后左右的控制上）。     
怎样改成美国手：注释掉 RC_Channel.h 的第 6 行“#define RC_MODE_1”就行了。因为：
![](https://github.com/SuWeipeng/img/raw/master/13_car/rc_chan_2.jpg)     

白话讲“类和对象”
---
> 面向对象的编程离不开类和对象，这里 Sugar 不讲编程，尝试从生活的角度说一说啥是类、啥是对象。     
    
Sugar 上学时当过理综（理、化、生）课代表，就以物理课代表来说，最常做的两件事是：从老师那里得到作业内容并布置给同学们、从老师那里取练习卷发给同学们。不妨按下面的格式写一下这两件事：
![](https://github.com/SuWeipeng/img/raw/master/13_car/cpp_oop_1.jpg)     
这样写出来不难发现，要完成课代表的工作只需要明确两件事就行了：一是，要干什么事；二是，用什么来做要干的事。     
这样不难发现，当课代表要做的事和做事用的资源都明确后，只要找一个人来担任课代表就能把这些事情做起来了。事实上我们生活中的任何一个职位都是这样发挥作用的。       
说了这么多，与“类和对象”有啥关系呢？其实，“类”就相当于上面图片的作用：明确任务以及用什么做这些任务。“对象”就是来做这些任务的人。不难发现：只有类没有对象是不能把事情做起来的。（会C++的同学在这里不要起高调说“类的静态函数是可以不通过对象调用的”，这跟目前要表达的不是一个问题。）

ardupilot 里的类和对象
---
> 下面以 ardupilot 为例从宏观角度说一下：什么东西可以写成一个类。     

1、某一领域的算法或某种软件功能写成一个类     
比如：算法类 AC_AttitudeControl、AC_Avoidance、AP_NavEKF2 等；功能类 AP_Logger、AP_Math 等。     
2、某一类硬件写成一个类     
比如：AP_GPS、AP_Baro、AP_Beacon等。     
3、不同平台写成一个类     
比如：AP_HAL_ChibiOS、AP_HAL_Linux、AP_HAL_SITL等。     

上面是 Sugar 理解的 ardupilot C++ 类的划分方法。说到类的划分，我们日常生活中耳熟能详的一个词是“分类整理”，提到“分类”就联想到“整理”。提到整理，就要有“整理的方法”和“整理的东西”。回看 ardupilot 支持的设备：ArtennaTracker 追踪天线、APMrover2 各种车、ArduCopter 各种旋翼飞机、ArduPlane 各种固定翼、ArduSub 水下设备。Sugar 统称这些为“设备层”，设备层代码就是对 libraries 里的各个类按设备所需的方法进行整理而做出的。libraries 就是负责给出整理的东西（上面那三种分类的代码）。

这里把 OOP 类和对象的“类”与生活中分类整理的“类”混说了一下，有没有发现生活其实跟编程很接近，爱生活的人对编程更容易接受就是这个原因。

ardupilot 的传承
---
Sugar 很喜欢 ardupilot 的代码，但因为 ardupilot 代码非常庞大，容易引起初学者的畏难心理，所以 Sugar 决定发扬 ardupilot 代码的优秀思想做一套简单的开源程序。      
Sugar 传承 ardupilot 的想法很早就有了，一直没下手是因为没有找到合适的载体。直到今年给宝宝做生日礼物，然后发朋友圈有人购买，才促成了 Sugar 现在开源的麦克纳姆轮车代码。     
在[《ardupilot 利箭离弦式飞速起步方略》](https://mp.weixin.qq.com/s/flCiLMEFJfbnPHUPX1kvZw)中 Sugar 让麦轮车的代码目录亮了个相。      
在[《一起来做遥控车（软件架构训练三终篇）》](https://mp.weixin.qq.com/s/ASKcCaGkyCwLIaf57nVj-w)中提到了是大家的支持促成了这个传承。      
Sugar 希望大家能用更短的时间学到精华的东西，不仅仅是那些行固定的 ardupilot 代码。所以 Sugar 有想法把这个体积小、组织精、入门简单的麦轮车代码继续维护下去，希望能得到各位伙伴的支持。

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