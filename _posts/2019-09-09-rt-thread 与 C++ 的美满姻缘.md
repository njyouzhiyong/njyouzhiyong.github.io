---
layout:     post
title:      rt-thread 与 C++ 的美满姻缘
subtitle:   rt-thread 系列推文
date:       2019-09-09
author:     Sugar
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - rt-thread
    - RTT
    - RTOS
    - 操作系统
---

> 背景介绍：
> 网上搜关键词“**rt-thread C++**”发现可参考的文章不算多。<br>
> Sugar 在自己开源遥控车代码中促成了 rt-thread 和 C++ 的美满姻缘。<br>
> 美好姻缘是指：不论是用 MDK5、IAR 或者 GCC，都可以**亲密配合**。<br>
> 过程中有参考：**https://www.rt-thread.org/qa/thread-11707-1-1.html**<br>
> 遥控车开源地址：**https://github.com/SuWeipeng/car_407ve**

rt-thread 的 C++ 组件
---
* 组件在哪里<br>
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/cpp_1.jpg)<br>
* 组件的依赖<br>
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/cpp_2.jpg)<br>

给 rt-thread 和 C++ 牵红线的过程
---
> Sugar 只是做个媒，其实大多数工作 rt-thread 都做完了。<br>
> Sugar 觉得 rt-thread 潜力大的原因之一是：工作做得全面细致。<br>
> 开源代码发展得既健壮又精细真的不容易。<br>
 
* 不同平台下的 libc<br>
Sugar 开源代码不维护工程，只维护配置文件，工程可以交给 progen 自动生成。<br>
这样的好处之一就是：通过配置文件能够很清楚地知道哪些代码参与了编译。<br>
对于配置文件的介绍请见[《一招通吃 MDK5、IAR、GCC》](https://mp.weixin.qq.com/s/aPUbSAndjvs4CaPj3CFsJg)和[《【升级】一招通吃 MDK5、IAR、GCC》](https://mp.weixin.qq.com/s/iVmaQ3S4vcitbJ8iXZyArw)<br>
(1) MDK5 下的 libc<br>
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/libc_1.jpg)<br>
(2) IAR 下的 libc<br>
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/libc_2.jpg)<br>
(3) GCC 下的 libc<br>
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/libc_3.jpg)<br>
* GCC 下需要注意的地方<br>
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/gcc_link_1.jpg)<br>
由于 Sugar 在自己的 ubuntu 虚拟机里配置了 ardupilot 开发环境，该有的都有了，所以 Sugar 没有用 rt-thread 官网推荐的 env。<br>
这样在 gcc 编译的时候就要定义一个宏，防止 rt-thread 的 libc 和系统的 libc 冲突。<br>
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/libc_4.jpg)<br>
GCC 下的链接脚本：<br>
链接脚本使用 rt-thread 官方代码里的 link.lds 最省事了，该折腾的 rt-thread 官方都折腾好了。<br>
以前 Sugar 使用 CubeMX 生成的 链接脚本，要是用 C++ 的话要改的地方比较多。<br>
因为 Sugar 没有用 env，所以用 link.lds 的时候遇到了这个错误：<br>
```
/opt/gcc-arm-none-eabi-4_9-2015q3/bin/../lib/gcc/arm-none-eabi/4.9.3/../../../../arm-none-eabi/bin/ld: section .ARM.extab.text._Z15constrain_floatfff loaded at [08058358,08058363] overlaps section .data loaded at [08058358,0805871f]
collect2: error: ld returned 1 exit status
Makefile:145: recipe for target 'build/stm32f407ze-rtt.elf' failed
make: *** [build/stm32f407ze-rtt.elf] Error 1
```
别担心，其实在链接脚本里加一行就能解决这个问题了。<br>
```
.ARM.extab   : { *(.ARM.extab* .gnu.linkonce.armextab.*) } >CODE
```
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/gcc_link_2.jpg)<br>
* 代码上要注意的地方<br>
(1) IAR 下不能有重名文件的解决办法。<br>
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/cpp_3.jpg)<br>
(2) `C++11` 标准与 rt-thread。<br>
在遥控车的开源代码里 Sugar 移了 ardupilot 的库，ArduPilot 代码使用 `C++11` 标准。<br>
为了增加 rt-thread 和 `C++11` 的亲密度，让遥控车代码能三平台(MDK5、IAR、GCC)通用。这里 Sugar 花了不少时间。<br>
最终没有找到完美解决办法，折了个中。<br>
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/cpp11_1.jpg)<br>
IAR 下 rt-thread 和 `C++11` 兼容的办法。<br>
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/cpp11_2.jpg)<br>
MDK 下 rt-thread 与 C++ 编译要注意的地方。<br>
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/cpp_4.jpg)<br>
GCC 下就不说了（因为要说的话比较多，且背景介绍时那个引用的链接已经说得比较全面了）。<br>
(3) C++ 使用 rtthread 命名空间<br>
```cpp
using namespace rtthread;
```
![](https://github.com/SuWeipeng/img/raw/master/12_RT-Thread/cpp_5.jpg)<br>
至此，rt-thread 和 C++ 已拜过天地，可以共入洞房了。<br>

说了半天，这个代码控制效果到底是啥样？
---
> 这部分就要上 ArduPilotLog 来展示了。<br>
> Sugar 不想写这一节，因为与本次推文关系不大。<br>
> 控制效果主要取决于算法和参数，rt-thread 为算法和日志的记录提供了良好的运行环境。<br>
> 上两张 ArduPilotLog 的图，说明 Sugar 本文不是在瞎掰。

![](https://github.com/SuWeipeng/img/raw/master/13_car/pid_5.jpg)<br>
![](https://github.com/SuWeipeng/img/raw/master/13_car/pid_4.jpg)<br>
![](https://github.com/SuWeipeng/img/raw/master/13_car/pid_3.jpg)<br>

从数据可以看出控制效果是相当不错的哦。<br>

PS
---
> 不是 Sugar 造的代码，Sugar 只是代码的搬运工。<br>
> 这么说虽然很 LOW，但咱实事求是。<br>

PID 是搬的 ardupilot 最新的 AC_PID 库。<br>
Log 是移植 ardupilot 的日志系统（改为 C 语言版）。<br>
用上国产 RTOS 实时系统 rt-thread。<br>

懂架构的好处就是：可以当个合格的搬运工。（这么说真是 LOW 到家了）<br>
换个高大上的方式：懂架构可以用一点点吹灰之力就能高效的完成一整套优质可靠的代码实现目标任务。(这么说有没有更有吸引力？）

如果读者有想提高软件架构能力的意愿，欢迎加入 Sugar 的[《软件架构训练计划》](https://mp.weixin.qq.com/s/6wM1kMKWpOJxBatzTNxShQ)

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