---
layout:     post
title:      ardupilot 日志系统移植
subtitle:   怎样在自己的单片机上记日志
date:       2019-07-28
author:     Sugar
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - ardupilot
    - log
    - ardupilotlog
    - 日志
    - 文件
---

> 上一篇推文[《ardupilot 日志文件解析》](https://mp.weixin.qq.com/s/gXxV2U8AP5DOXrHZIWVkrw)中表述了日志文件的构成。<br>
> 本篇推文用 C 语言来做一个简单的 ardupilot 日志系统移植 demo。
> （使用“潘多拉”开发板上 spi 模式的 MicroSD 卡槽）

“解码格式”结构体数组
---
> 这部分与 ardupilot 的源码结构一致。

![](https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/log_code_1.jpg)

初始化时，将解码格式写入文件首部
---

![](https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/log_code_2.jpg)

C语言形式封装一个测试函数
---
> 到这里，已经完成了 80% 的工作。<br>
> 什么？原来这个日志系统就这么点儿代码？<br>
> 不要怀疑，真的就是这么简单。

![](https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/log_code_3.jpg)

看看还差点啥
---
* 日志系统函数都有了，怎么写到 SD 卡上呢？<br>
简单，用 FatFS 实验上面的 WriteBlock() 接口就行了。<br>
一个函数就搞定。

![](https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/log_code_4.jpg)

* 放 main() 函数里跑一下试试。
用 CubeMX 的一看下图里的注释就知道是在 main() 的哪个地方，我就不截全图了。

![](https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/log_code_5.jpg)

看一下头文件，看看能不能找到 ardupilot 的感觉
---

![](https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/log_code_6.jpg)

总结
---
本篇就先简单的写到这里，后面我会用这个日志存些有用的数据，到时候代码就多起来了。<br>
给宝宝装了个小车，后面把日志用在这个小车上，上 RT-Thread 操作系统。边玩边学代码。


PS
---
* 上一篇说得那么牛的 ardupilot 日志系统，移植过来就这么几行代码，轻松不轻松？<br>
* ardupilot 代码虽然长，但构架非常清晰。经常是好几种功能都打一个套路。<br>
* 程咬金最拿手的三板斧使了一辈子，ardupilot 代码构架优秀简单又实用，就跟程咬金那三板斧似的。
* 看代码首先看的不是函数怎么实现功能的，而是看函数实现的是什么功能。尤其是看开源代码，量大、功能多，要拎清各个功能之间的区别和联系才能看得懂。

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