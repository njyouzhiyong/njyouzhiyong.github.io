---
layout:     post
title:      怎样掌握 rt-thread（RTOS该怎么学）
subtitle:   RTOS 学习方法
date:       2019-10-28
author:     Sugar
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - RTOS
    - RT-Thread
    - RTT
    - 学习方法
---

> 背景介绍：      
> Sugar 曾写过一篇[《未来嵌软开发趋势》](https://mp.weixin.qq.com/s/AW8JSqS2vUHn3n-jqaGf-A)，描述了嵌入式编程方法的发展。      
> 对于 RTOS 的必要性已经不用再多加解释，现在新问题是：      
> 1、怎样快速掌握一种 RTOS 呢？      
> 2、初学者选择哪一种 RTOS 最合适呢？      
> 3、有必要买书么，看书学习有什么优势又有哪些不足？      
> 本篇 Sugar 就对这几个最常见的问题来发表一下个人看法。

怎样快速会用一种 RTOS
---
一、提出问题      
每一种 ROTS（RT-Thread、uC/OS II、uC/OS III、FreeRTOS、ChibiOS、NuttX 等等）都是历经十多年甚至更长时间沉淀下来的成果。       
一听说“十多年甚至更长时间”，就有不少人担忧了：这玩儿艺儿这么难，可怎么办啊？别怕，Sugar 既然开了头儿，就不会不给出方法。      
Sugar 十几年的软件开发经历总结出这么一句话：当我们面对问题的时候，第一反应不是去解决问题，而是把问题进行拆分。拆分到什么程度算合适呢？Sugar 认为拆分到个人能力能覆盖被拆出的小问题就算合适。问题经过拆分后，能很清晰地划分出自己能解决的部分、需要求教他人的部分。这么做除了自己容易下手外，向别人求教的时候也能更具体地描述哪里需要帮助（别人更容易理解你的问题，你自然也更容易得到答案）。      
二、拆分问题      
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/learn_1.jpg)     
如上图，Sugar 把“如何会用一种 RTOS”的问题拆分成四个步骤，每个步骤用最合适的方式下手，学起来就是轻松加愉快了。下文会给出每个步骤 Sugar 认为的最合适的方式是啥样儿的。     

初学者选哪一种 RTOS 最合适呢？
---
Sugar 认为 RT-Thread 最合适，原因如下：     
1、原生中文文档，降低阅读难度，是不是很有吸引力？      
2、官方文档多用 UML 示图，图形表述比文字更容易理解和记忆。     
3、RT-Thread 是一个带 RTOS 的嵌软解决方案，[《Sugar 在火车上写的 RTT 巡回培训（武汉站）的背书》](https://mp.weixin.qq.com/s/58Ypzab6nMOWpbgKXPAkGQ)中有述。      

书
---
Sugar 喜欢看书（当然要是好书），因为书上的内容很系统，可以大大节省学习时间。      
新知识“系统化”是书的优点，但凡是书，都有一个避不开的缺点，尤其是在科技日新月异极速发展的今天，这个缺点就更加明显，这个缺点就是：但凡是已经出版的书，在其写书、排版、印刷所消耗的时间里，相关技术已经又发展了。换句话说：当你第一次拿到书的时候，你从书里看到的内容可能已经跟当下最新的模样不一样了。（但这并不代表书过时了。）       
“三人行必有我师”，“三人”尚有我师，何况是几十甚至几百页的书呢？“学会有选择地从书里吸收想要的营养”是每个读者的智慧所在。

Sugar 新动作
---
> 上面说的“每个步骤最合适的方式”在这部分会有具体展开。     

在说新动作之前，先说一下在 Sugar 心里程序的组成，如下图：     
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/learn_2.jpg)        
从软件设计本身来看，其核心的三个点就是“逻辑”、“算法”和“参数”。逻辑是思维能力的体现，算法是科学知识的归宿；参数本身并不包含什么内容，但其对于系统架构而言则有至关重要的作用。       
正如读者看到的这样，在 Sugar 上面这段表述中并没有 RTOS 的出现。之所以要先说这段话，是要表达：Sugar 认为编程的灵感之始和动力之源是来自对上面三个点的思考，所有的知识最终都可以在这三个点中找到归宿。RTOS 的作用就是：使得对上面三个点的思考结果能够快速、便捷地以软件形式具象化。为了能够让初学者用最佳的方式学会用 RT-Thread，Sugar 开始做新的探索。
**目标硬件：** STM32 系列单片机（不限详细型号，但 Sugar 会以手边常用的“开源麦轮车的控制板 STM32F407VE”、“RT-Thread IoT Board 主控芯片 STM32L475VE”、“开源麦轮车遥控器主控芯片 STM32F103C8”为示例平台）。      
**工具软件：** STM32CubeMX、project generator（见[《一招通吃MDK5、IAR、GCC》](https://mp.weixin.qq.com/s/aPUbSAndjvs4CaPj3CFsJg)和[《【升级】一招通吃MDK5、IAR、GCC》](https://mp.weixin.qq.com/s/iVmaQ3S4vcitbJ8iXZyArw)）、MDK5.24（最高 MDK5.26）、IAR 8.40.1、Sugar 共享的 Ubuntu 环境下的 gcc、SmartGit。

**永不过时的参照**      
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/learn_3.jpg)       
Sugar 一直觉得 Git 的开发 log 做好了会是个永不过时的参照。好好做其作用就相当于书，而且比书更明确，使用 git 方便与时俱进、永不过时。       
在“会裸机编程”和“RT-Thread 怎样使用片上资源”这两块，Sugar 以 IoT Board 的 uart 为例，现在开始逐渐在 github 上提供示例并好好写 Git 的 Log，并且有空会写推文讲解（跟 Git 的 Log 做，可以不等 Sugar 推文，相当于学的人不用等写书、排版、印刷的过程）。     
“了解 RTOS 运作机制”这一块，Sugar 会继续如“RTT架构训练二”一样用些简单的题目做实例讲解。目前，读者可以参照[《RTT架构训练二（总结）》](https://mp.weixin.qq.com/s/Yuupu9qm7rwpgCkDRWtD2g)了解这部分的展开方式。       
“实况练习”这部分就要做点完整的东西了，目前 Sugar 的开源麦克纳姆轮小车代码是一个 Sugar 正在维护的实况练习的例子。本来这部分 Sugar 是想结合 RT-Thread 做一套开源飞控的，但考虑到面向的是初学者，飞控的算法比麦轮车的算法门槛高，所以选择了麦轮车。“实况练习”主要围绕如何设计“逻辑”、“算法”和“参数”并将之融入一套软件来实现具体功能展开的。如上面所说，这三个核心点与是否用 RTOS 无关，所以 Sugar 有开源两套方案，一套有 RT-Thread，一套裸机程序，正好可以对比感受一下上面说到的那句“RTOS 的作用就是：使得对上面三个点的思考结果能够快速、便捷地以软件形式具象化。”          
（麦轮车的裸机程序可以参考软件架构训练三，[《一起来做遥控车（软件架构训练三终篇》](https://mp.weixin.qq.com/s/ASKcCaGkyCwLIaf57nVj-w)有全部推文汇总。）

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