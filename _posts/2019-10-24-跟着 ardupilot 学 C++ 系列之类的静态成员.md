---
layout:     post
title:      跟着 ardupilot 学 C++ 系列之友元
subtitle:   C++ 基础系列推文
date:       2019-10-11
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
> “跟着 ardupilot 学 C++ 系列”推文已经连载三篇了，分别是：      
> [《跟着 ardupilot 学 C++ 系列之多态》](https://mp.weixin.qq.com/s/ixhfR7zmlFlsUV7m6zy0Yg)      
> [《跟着 ardupilot 学 C++ 系列之友元》](https://mp.weixin.qq.com/s/g52zaKy8vcVGxstmwfSb-A)
> [《跟着 ardupilot 学 C++ 系列之类和对象》](https://mp.weixin.qq.com/s/g52zaKy8vcVGxstmwfSb-A)      
> Sugar 做这些推推文的想法源于对模友付费辅导的经历。     
> 因为找 Sugar 辅导的绝大多数模友 C++ 基础比较薄弱，所以 Sugar 会以免费推文的形式让模友有个复习参考，同时也能惠及更多没有付费但关注了 Sugar 公众号的朋友们。

白话讲“C++类内的静态成员”
---
如果你是自己创业做公司的读者或做团队领导的读者，那么你一定知晓“统一思想”对团队有多重要。      
团队成员的共识程度是影响团队凝聚力的重要因素之一。如果把一个团体比作一个“类”，那么这个共识就相当于“类内的静态成员”。统一思想的目的就是推动团队成员达成共识，为同一个目标努力奋斗。这个“共识”存在于每个团队成员的头脑里，相当于“类的静态成员被类的所有对象共享”。      
一个公司的共识会渐渐沉淀成这个公司的文化，当我们谈到“公司文化”的时候是将“公司”和“文化”联系起来了。同样的，类内的静态成员一般都直接通过类名访问。

ardupilot 静态成员的典型用法
---
> 这里 Sugar 为了方便以自己封装的 AP_Logger2 类为例。     
> 在 ardupilot 里直接搜 "get_singleton" 可以看到很多地方都有类似的应用。     

![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/FSM_Code_2.jpg)      
最新的 ardupilot 代码都是通过“命名空间”里定义接口函数来调用静态函数成员的，如下图：     
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/FSM_Code_3.jpg)       
有关“命名空间”的使用，本篇推文不会展开，有需要的读者要自己查一下相关知识。     
通过上面的截图，我们发现：     
静态函数成员 get_singleton() 是通过类名 AP_Logger2 访问的。      
下面我们看下静态成员变量 _singleton 的使用，如下图：      
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/FSM_Code_4.jpg)       
通过上面的截图，要知道：     
静态成员变量必须按上图的方式进行初始化。     
经过上面一翻折腾，我们就可以非常爽地到处记录状态机了，如下图：      
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/FSM_Code_5.jpg)       
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/FSM_Code_6.jpg)        

状态机
---
> ardupilot 代码里很多地方使用了“状态机”。      
> 状态机不仅是一种代码的写法，也是一种编程思路。      
> 下面以模式代码为例，看下该怎么通过“状态机”来看代码。

第一种情况：以 Alt_Hold 模式解锁起飞，低电触发降落。那么定高的状态机和马达的状态机是的切换顺序是这样的，如下图：      
（绿色的 id1 是定高模式的状态机，蓝色的 id0 是马达的状态机）     
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/FSM_1.jpg)      
第二种情况：以 Alt_Hold 模式解锁起飞，在 Alt_Hold 模式下落地上锁。那么状态机如下图：     
（红色的 id1 是定高模式的状态机，蓝紫色的 id0 是马达的状态机）      
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/FSM_2.jpg)       

状态机的代码形式，以及知道状态迁移顺序对看代码有什么好处？     
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/FSM_Code_7.jpg)        
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/FSM_Code_8.jpg)        
很显然，知道状态迁移顺序有助于我们理清代码的运行过程，是不是？     

PS
---
本来 Sugar 今天想写定高模式的控制过程（偏算法一点），但一看代码，还是决定再补一篇基础。因为讲控制的推文 Sugar 不写也有别人写，而且已经很多了，而通过具体应用来补代码基础的文章还很少。       
定高这里涉及的两个其余的基础知识是：“命名空间的使用”和“状态机程序设计方法”，这两个就不在这篇推文展开讲了，有必要的话以后再说。      
本文的状态迁移顺序图是通过 ArduPilotLog 导出数据库文件后，将数据库文件加载到 Matlab 里用 FSMAnalysis.m 脚本绘出的。因为设计上考虑到节省空间，所以不能直接在 ArduPilotLog 里直接显示状态迁移图。有需要的读者可以在 ArduPilotLog 的开源地址里找到这个脚本，或者在公众号回复 FSM。

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