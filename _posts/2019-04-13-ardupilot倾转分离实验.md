---
layout:     post
title:      ardupilot倾转分离实验
subtitle:   且看ArduPilotLog如何让数据展现得清清楚楚
date:       2019-04-13
author:     Sugar
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - ardupilot
    - ArduPilotLog
---

> 这是一次失败的折腾，且看[ArduPilotLog](https://github.com/SuWeipeng/ArduPilotLog)如何让败也败得有理有据。
> <br/>实验数据下载：
> <br/>[百度网盘](https://pan.baidu.com/s/108RIzw5gnYXO7hFGmBXgpw),提取码：5o2s 
> <br/>[google网盘](https://drive.google.com/drive/folders/1GJ7wyecbgA1nWgby8jqnjU-J-3ooBO_C?usp=sharing)

[ArduPilotLog](https://github.com/SuWeipeng/ArduPilotLog)要说话
---
<br/> ![YawOutOfControl_1.png](
https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/YawOutOfControl_1.png)

[ArduPilotLog](https://github.com/SuWeipeng/ArduPilotLog)有话说
---
<br/> ![YawOutOfControl_2.png](
https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/YawOutOfControl_2.png)
<br/> ![YawOutOfControl_3.png](
https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/YawOutOfControl_3.png)

怎么会这样，究竟干了啥？
---
1. 理论背景先看ZingHD的发文[倾转分离(一)-APM的倾转分离竟然没有效果？](https://zinghd.gitee.io/tilt_torsion_1/)
<br/>注意文中提到一句话：**【倾斜误差】可以对齐z轴**
<br/>这里用图示说明什么叫“对齐z轴”
<br/> ![YawOutOfControl_4.gif](
https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/YawOutOfControl_4.gif)
上图展示了两个不同姿态Z轴对齐的样子，可见：“对齐Z轴”就是 *对齐“桨平面”* 的意思。
2. 即然MATLAB仿真证明倾斜误差可以对齐Z轴，那么现在就可以开始折腾代码了。
<br/>(1) 先截断【旋转误差】 
<br/> ![YawOutOfControl_4.png](
https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/YawOutOfControl_4.png)
<br/>(2) 加自定义日志"TILT"记录飞行数据
> <br/>TILT.ErrAng 对应 thrust_vec_dot
> <br/>TILT.ErrZ 对应 att_diff_angle.z

<br/> ![YawOutOfControl_5.png](
https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/YawOutOfControl_5.png)
 
结合[ArduPilotLog](https://github.com/SuWeipeng/ArduPilotLog)分析各种现象原因
---
1. “DesYaw被带走”、以及“特征3”的原因分析
``` cpp
    // Limit Yaw Error based on maximum acceleration - Update to include output saturation and maximum error.
    // Currently the limit is based on the maximum acceleration using the linear part of the SQRT controller.
    // This should be updated to be based on an angle limit, saturation, or unlimited based on user defined parameters.
    if(!is_zero(_p_angle_yaw.kP()) && fabsf(att_diff_angle.z) > AC_ATTITUDE_ACCEL_Y_CONTROLLER_MAX_RADSS/_p_angle_yaw.kP()){
        att_diff_angle.z = constrain_float(wrap_PI(att_diff_angle.z), -AC_ATTITUDE_ACCEL_Y_CONTROLLER_MAX_RADSS/_p_angle_yaw.kP(), AC_ATTITUDE_ACCEL_Y_CONTROLLER_MAX_RADSS/_p_angle_yaw.kP());
        yaw_vec_correction_quat.from_axis_angle(Vector3f(0.0f,0.0f,att_diff_angle.z));
        att_to_quat = att_from_quat*thrust_vec_correction_quat*yaw_vec_correction_quat;
    }
```
<br/>(1) 先解释“特征3”
``` cpp
att_diff_angle.z = constrain_float(...)
```
表示 z 向的角度差被限幅，按代码展开，可知其被限制的幅值为
```
pi()*(120/4.5)/180 = 0.465421133865
```
参考线1“const: 0.465421” 表示 “常量：0.465421”。
<br/>至此，解释了“特征3”在代码中的什么地方被限幅。
<br/>(2) 飞手感觉 Yaw 失控，目标曲线被检测曲线带走。
```cpp
att_to_quat = att_from_quat*thrust_vec_correction_quat*yaw_vec_correction_quat;
```
表示改变目标 att_to_quat ，正是这句代码在飞手没有主动改变目标的情况下，程序因角度差过大自动改变了目标。因此飞手会觉得 Yaw 不受自己控制。

2. “特征1”和“特征2”原因分析
<br/>这个原因很明显，是本次修改代码所导致。
<br/>上面的修改“截断【旋转误差】”，在 thrust_vec_dot 足够小时又暴力恢复。引起了 _rate_target_ang_vel.z 突变，进而引起“特征2”的“断崖式”突变。
<br/>_rate_target_ang_vel.z 突变同时引起了给PID控制器输入的差值突变，既“特征1”。
> 所谓“断崖式”突变，指在数据的骤然变化过程中存在数据缺失。[ArduPilotLog](https://github.com/SuWeipeng/ArduPilotLog)在曲线上标出数据点，在“特征2”处两个相差很大的数值之间没有数据点，这种跳变称之为“断崖式”突变。

下图给出 PIDY.E 和 PIDY.LPE 是什么：
> 注意：C++每个对象有不同的资源，图示中是在“类”内。
<br/> ![YawOutOfControl_6.png](
https://github.com/SuWeipeng/img/raw/master/1_ArduPilotLog/YawOutOfControl_6.png)
 
3. “特征4”原因分析
<br/>这个原因也是本次修改代码所致。
``` cpp
    static uint32_t timestamp_last_ms = AP_HAL::millis();
    if(fabsf(thrust_vec_dot) < AC_ATTITUDE_THRUST_ERROR_ANGLE / 5){
        if(AP_HAL::millis() - timestamp_last_ms > 20){
        	yaw_vec_correction_quat.to_axis_angle(rotation);
        	att_diff_angle.z = rotation.z;
        }
    } else {
    	timestamp_last_ms = AP_HAL::millis();
    }
```
按代码展开，第一个 if 的限定条件是 thrust_vec_dot 小于 6 度。正是这个“生硬”的 if 导致了 TILT.ErrZ(既 att_diff_angle.z)的突变。
```
pi()*6/180 = 0.10471975512
```
参考线2“const: 0.10472” 表示 “常量：0.10472”。

结论
---
<br/>这次修改效果不好，是一次失败的修改。
<br/>[ArduPilotLog](https://github.com/SuWeipeng/ArduPilotLog)显示的飞行数据清晰指出了失败在什么地方，不怕瞎折腾，就怕折腾来折腾去都不明所以。
<br/>[ArduPilotLog](https://github.com/SuWeipeng/ArduPilotLog)就是给爱折腾的朋友们提供数据分析支持的。
> <br/>失败了没关系，只要清楚知道败在哪里，总还是有希望成功的。

待进一步讨论的点
---
<br/>ArduPilot 这种硬拆分“轴角向量”的做法我认为过于暴力，难（没）于（有）理（道）解（理），数据背后也许有更神秘的原因。
<br/>按说“轴角向量”是不能从一个地方取x、y，从另一个地方取个z，然后拼成(x,y,z)的。
<br/>至于为什么不能，其原因简言之就是：不是一家人，不进一家门。若想从原理上搞懂，请参阅ZingHD的另一篇文章《[姿态控制-加速度转倾斜角和四元数转轴角函数解析(2018-10-27更新)](https://zinghd.gitee.io/accel_to_lean_angles-to_axis_angle/)》

请我喝杯咖啡如何？
---
1. 微信
<br/>![](https://github.com/SuWeipeng/img/raw/master/weixinfukuan.jpg)
2. 支付宝
<br/>![](https://github.com/SuWeipeng/img/raw/master/zhifubaofukuan.jpg)
3. 微信好友
<br/>![](https://github.com/SuWeipeng/img/raw/master/weixinhaoyou.png)