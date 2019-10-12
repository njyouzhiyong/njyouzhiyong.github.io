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
    - 友元
---

> 背景介绍：     
> 紧跟 C++ 基础推文开篇[《跟着 ardupilot 学 C++ 系列之多态》](https://mp.weixin.qq.com/s/ixhfR7zmlFlsUV7m6zy0Yg)，再来推一篇关于友元的文章。     
> 还是以 ArduCopter 的模式代码为列来展开。就着上一篇的热乎劲儿，把模式相关的代码完整地扫一遍。

本篇核心语句
---
**被你抱在怀里的人便能听到你的“咚咚咚”的心跳声。**

白话讲 C++ 友元
---
“友元”开头一“友”字跟汉语的意思一样，咱就来说一说这个“友”字。          
1、友人能获得什么     
Sugar 是个非常爱分享的人，能够从分享中体会到快乐。提到分享，就必然要有个分享的圈子，而这个圈子的构成一定离不开友人，这一点想必大家都是一样的。说这么多，就是一个目的：你的友人能够接受来自你的分享。     
什么东西会拿来分享呢？一般 Sugar 觉得有分享意义的东西是 Sugar 觉得在别的地方找不到的，至少是难得找到的，而且 Sugar 拥有的。就是说 Sugar 拿来分享的大多是 Sugar 私有的东西，也就是说 Sugar 的友人能够接收到 Sugar 私有的东西。     
2、友人的位置     
友人可以在任何时间联系你，不论是你的个人生活时间还是你的工作时间，朋友打开的电话、发来的信息都是会看的。      
友人存在于生命里，只要活着友谊长存，无视时间与空间。

以模式为例说说 ArduCopter 如何使用 C++ 友元
---
![](https://github.com/SuWeipeng/img/raw/master/4_ardupilot/cpp_friend_1.jpg)     
有关 C++ 友元的专业解释，可以看下面链接（好文推荐）：
https://blog.csdn.net/fanyun_01/article/details/79122916     
1、友元必须的 C++ 关键字 friend     
如上图所示，Copter 类的友元类前都有 friend ，这些友元类都可以访问 Copter 类的私有成员。（对应上面说的“友人能获得什么”更便于理解）     
一开始会有人在“谁能访问谁的私有成员？”这个问题上蒙一阵，如果你怕蒙掉或忘掉，请回头看上面写的“本篇核心语句”。下面解释一下这句话：     
```cpp
class A{
...
public:
  friend class B;
...
};
```
我们把 A 类的两个大括号当成两条胳膊，则 B 类就是被 A 类抱在怀里的。心是私有的，B 类被 A 类抱在怀里就能听到 A 类的心跳声，表示：B 类可以访问 A 类的私有成员。     
2、友元关系没有继承性     
通过上一篇推文，我们知道 Mode 是所有模式类的父类。在上面的截图中，Mode 的所有子类也是 Copter 类的友元类，这就是因为友元关系没有继承性。     
类比一下实际生活，就很容易理解和记忆：父母的朋友并不是孩子的朋友。     
3、友元关系没有传递性      
类比生活理解：妻子在丈夫的怀里，妻子能听到丈夫的心跳声；孩子在妈妈的怀里，孩子能听到妈妈的心跳声。但孩子听不到爸爸的心跳声，不是因为妈妈太胖了，而是因为友元关系没有传递性。      
4、友元关系是单向的，不具有交换性     
类比生活理解：孩子在妈妈的怀里，孩子能听到妈妈的心跳声，但妈妈听不到孩子的心跳声。不是因为孩子太矮了，而是因为友元关系是单向的，不具有交换性。

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