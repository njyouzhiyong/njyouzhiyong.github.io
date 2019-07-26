---
layout:     post
title:      ardupilot 日志文件解析
subtitle:   短文不烧脑了解 ardupilot 日志文件
date:       2019-07-26
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

> 2019年04月05日，我开源了自己写的 [ArduPilotLog](https://github.com/SuWeipeng/ArduPilotLog)。<br>
> ardupilot 日志系统非常好用，所以我打算**将之移植出来**。<br>
> 在移植之前，先来解析一下 ardupilot 日志文件，为后面移植代码打个基础。

日志文件的新生命
--
> [ArduPilotLog](https://github.com/SuWeipeng/ArduPilotLog)的重大作用之一，就是：**将日志转为 sqlite 数据库文件**。这个功能为日志文件赋予了新的生命。<br>
> 这个功能是“站在巨人的肩膀上”产生的，因为 ardupilot 原有日志里具有建立数据库所需的全部内容，只是没有以数据库文件的形式存在而已。

![](https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/function_1.jpg)

* ardupilot 日志文件的生命力所在<br>
1、24.9 MB 的 *.bin 日志文件，生成的 sqlit 数据库文件有 48.2MB。说明 *.bin 文件**数据更紧凑、体积更小**。<br>
2、\*.bin 文件本身包含数据库“表头”和“表体”的全部信息，非常方便转换。<br>
3、想在单片机上跑个 sqlite 不是很容易，但在单片机上记录 *.bin 日志文件十分容易。并且**对单片机要求比较低**，低到**只要能跑 FatFS 文件系统就行**。

ardupilot 日志文件分析
---
> 要点提示：<br>
> 1、日志文件**同一内存分布下的两种内容**。<br>
> 2、日志文件与数据库文件的关系。<br>
> 3、日志文件的内存分布。<br>

* 日志文件的两种内容<br>
1、日志**解码格式**；<br>
2、日志**数据**。<br>
![](https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/file_1.jpg)

* 内存分布<br>

![](https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/mem_1.jpg)

读日志文件时怎样区分两种信息
---
> 结合 ArduPilotLog 关键代码说明。

通过上文可以知道：两种信息的**内存分布是相同的**，唯一的联系（也是用以区分的标记）就是 **msgid**。<br>
因此，ArduPilotLog 读到 **msgid 为 0x80 的数据**时将之视为“解码格式”信息。<br>

![](https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/code_1.jpg)

ardupilot 里写入“解码信息”的关键函数
---
> 个函数是移植 ardupilot 日志系统所需的函数之一。<br>

![](https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/code_2.jpg)

移植思路
---
1、将“解码格式”写入日志文件**首部**（因为读文件解码时要**先获知**各个msgid的日志数据按什么格式来解码）。
2、按日志的内存分布封装日志函数，用于记录日志数据。

移植 ardupilot 日志系统其实非常简单。了解日志文件构成之后，按 ardupilot 架构往外搬就行了。

如果对软件架构没有认识，可以看下我的[《软件架构训练计划》](https://mp.weixin.qq.com/s/6wM1kMKWpOJxBatzTNxShQ)，在 github 上有开源训练内容。

无私奉献
---
有关 ardupilot 日志的**更详细**的文档，可以在我的公众号内回复 **apm** 获得。<br>
内容包括：<br>
1、我录制的 ardupilot 入门视频教程。<br>
2、我常用的 ardupilot 开发环境虚拟机。<br>
3、我做过的 ardupilot 相关文档。

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