---
layout:     post
title:      RT-Thread 使用 CubeMX 的 VCP（虚拟串口）
subtitle:   19分钟视频展示
date:       2019-06-29
author:     Sugar
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - RTT
    - rtthread
    - RTOS
    - RT-Thread
    - 操作系统
    - VCP
    - VPC
    - STM32
    - 虚拟串口
---

> 以前在推文[《我精简的 RT-Thread 内核开源啦》](https://suweipeng.github.io/2019/06/25/%E6%88%91%E7%B2%BE%E7%AE%80%E7%9A%84-RT-Thread-%E5%86%85%E6%A0%B8%E5%BC%80%E6%BA%90%E5%95%A6/)中提到过 RT-Thread 可以用 CubeMX 的 VCP，<br>
> 下面将展示 RT-Thread 的过程，文末有视频地址。

先搞定 CubeMX 的 VCP
---
> 这里只提示要点，详细过程**见演示视频**。

* STM32F407 使用 VCP 要调大 heap

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-1.png)

* 按架构修改代码，可以保证工作量最少。

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-2.png)

* 下面是很少量的修改，十分简单。

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-3.png)

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-4.png)

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-5.png)

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-6.png)

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-7.png)

* 看下效果吧

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-8.png)

RT-Thread 使用 VCPSend 
---
> RT-Thread 使用的是**我精简过的内核**。<br>
> 推荐使用 git 的 **submodule** 方式引用我的精简内核。

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-9.png)

* git submodule 引用内核 

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-10.png)

* 少量代码修改过程如下：

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-11.png)

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-12.png)

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-13.png)

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-14.png)

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-15.png)

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-16.png)

* 效果展示

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-17.png)

OK啦!
---
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/VCP-18.png)

PS
---

* 视频中的工作流包含的内容：
> 从 0 起点开始很详细的步骤。<br>
> 除了本文所述内容外，还包括以下内容。

1. 如何使用 git 做版本管理；
`如何把代码托管给 git`<br>
`如何提交`<br>
`如何让 git 忽略不关心的内容`<br>
`如何使用 git submodule`

2. 如何使用 project-generator 减小软件维护成本；
`怎样修改配置文件`<br>
`怎样用命令生成目标工程`<br>

* 在从前的推文中不只一次提到**代码架构**，通过本便也看到了：弄懂架构，可以使代码修改量最小。

* 实际上功能这么简单的代码，多改几行也没什么。**从初学时就养成规范架构的习惯，对以后接触大工程有很大好处**。

* 我们常说的：`代码模块化`，`代码文件管理`这些都与好的架构思想非常相关。

* 视频地址

[点此 B站 链接](https://www.bilibili.com/video/av57167077/)

[点此 Youtube 链接](https://youtu.be/Hr1ijva-VJY)


关注作者
---
欢迎扫码关注我的公众号`MultiMCU EDU`。
![](https://github.com/SuWeipeng/img/raw/master/gongzonghao.jpg)
### `提示：在公众号“关于我”页面可加作者微信好友。`

请我喝杯咖啡如何？
---
微信
![weixinfukuan](https://github.com/SuWeipeng/img/raw/master/weixinfukuan.jpg)
支付宝
![zhifubaofukuan](https://github.com/SuWeipeng/img/raw/master/zhifubaofukuan.jpg)