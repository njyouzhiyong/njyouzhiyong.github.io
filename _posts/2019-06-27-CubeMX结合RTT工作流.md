---
layout:     post
title:      CubeMX结合RTT工作流
subtitle:   13分钟内学会如何使用 git 和我精简的 RTT 内核
date:       2019-06-27
author:     Sugar
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - RTT
    - rtthread
    - RTOS
    - RT-Thread
    - 操作系统
---

> [上一篇推文](https://suweipeng.github.io/2019/06/25/%E6%88%91%E7%B2%BE%E7%AE%80%E7%9A%84-RT-Thread-%E5%86%85%E6%A0%B8%E5%BC%80%E6%BA%90%E5%95%A6/)介绍了我精简的 [RT-Thread 内核](https://github.com/SuWeipeng/rt-thread)，很多朋友反应不知道怎么用。<br>
> 本篇推文以视频形式展现一下`如何使用我的精简内核`，同时展示一下`CubeMX与RT-Thread接合的工作流`。

[工作流视频展示](https://www.bilibili.com/video/av56958199/)
---
视频中预先装好了 Python 2.7 和 [project-generator](https://github.com/project-generator/project_generator)<br>

如何取得视频中的 demo 源码
---
方法一：[点此链接](https://github.com/SuWeipeng/lcd1602_rttthread_demo)<br>
方法二：[百度网盘](https://pan.baidu.com/s/1jsNnhnDIDpMf5jHHLib5Cw),提取码 ` 2k2u `

精简 RTT 内核获取方法
---
方法一：[github 开源地址](https://github.com/SuWeipeng/rt-thread)<br>
方法二：[百度网盘](https://pan.baidu.com/s/1jsNnhnDIDpMf5jHHLib5Cw),提取码 ` 2k2u `

本工作流的优点
---
1. CubeMX 与 RT-Thread 无缝接合。<br>
2. 不怕 IDE 工程丢失，随时可用配置文件生成。<br>
3. 只唯护代码和配置文件，不用维护 IDE 工程。<br>
4. 通过配置文件区分编译哪些代码，比在代码里用宏进行区分更直观。<br>
5. MDK5、IAR、GCC三平台兼容，需要换 IDE 时一个命令就搞定，高效省时。
6. 全程 git 护航，不怕改错没有后悔药。

文末彩蛋
---
> 一张图带你从不同层面认识 RT-Thread 线程组成。

![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/RTT-thread.jpg)


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