---
layout:     post
title:      vmware 与 Windows Sandbox 冲突的解决办法
subtitle:   以管理员身份运行批处理脚本解决问题
date:       2019-04-21
author:     Sugar
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - sandbox
    - VMWare
    - 沙盒
---

# vmware 与 Windows Sandbox 冲突的解决办法
1. 新建 vm_sandbox.bat 文件
2. 复制下面代码到 vm_sandbox.bat 文件中
> 注意：以ANSI编码保存，防止中文乱码。
```bash
cls
@ECHO OFF
CLS
color 0a

GOTO MENU

:MENU
ECHO.
ECHO.     =-=-=-=-=批处理菜单示例=-=-=-=-=
ECHO.
ECHO.       1-使用VMWare
ECHO.
ECHO.       2-使用SandBox
ECHO.
ECHO.       3-重启
ECHO.
ECHO.       4-退 出
ECHO.
ECHO. 
ECHO.
echo.      请输入选择项目的序号：
set /pID=
if "%id%"=="1" goto cmd1

if "%id%"=="2" goto cmd2

if "%id%"=="3" goto cmd3

IF "%id%"=="4"exit
PAUSE

:cmd1

bcdedit /set hypervisorlaunchtype off
cls
@ECHO OFF
CLS
color 0a
echo 需要重启!
goto MENU

:cmd2

bcdedit /set hypervisorlaunchtype auto
cls
@ECHO OFF
CLS
color 0a
echo 需要重启!
GOTO MENU

:cmd3

shutdown -r -c "立即重启" -t 0

```
3. 以“管理员身份”运行 vm_sandbox.bat
