# Raspberry Pi Configuration(GUI)
在安装好 raspbian 系统后，通过 USB 接口为 Raspberry Pi 3 连接上键盘鼠标、通过 HDMI 接口接上显示屏后，可进入系统的图形用户界面（GUI）。

在系统偏好菜单 `Preferences | Raspberry Pi Configuration` 中可修改相关系统配置。

![Raspberry_Pi_Configuration](Raspberry_Pi_Configuration.png)

## System
![1-System](./Raspberry_Pi_Configuration/1-System.png)  

## Interfaces
![2-Interfaces](./Raspberry_Pi_Configuration/2-Interfaces.png)  

## Performance
![3-Performance](./Raspberry_Pi_Configuration/3-Performance.png)  

## Localisation
![4-Localisation](./Raspberry_Pi_Configuration/4-Localisation.png)  

# raspi-config(CUI)
```Shell
sudo raspi-config

Raspberry Pi 3 Model B Rev 1.2

┌─────────┤ Raspberry Pi Software Configuration Tool (raspi-config) ├──────────┐
│                                                                              │
│    1 Change User Password           Change password for the current u        │
│    2 Hostname                       Set the visible name for this Pi         │
│    3 Boot Options                   Configure options for start-up           │
│    4 Localisation Options           Set up language and regional sett        │
│    5 Interfacing Options            Configure connections to peripher        │
│    6 Overclock                      Configure overclocking for your P        │
│    7 Advanced Options               Configure advanced settings              │
│    8 Update                         Update this tool to the latest ve        │
│    9 About raspi-config             Information about this configurat        │
│                                                                              │
│                                                                              │
│                                                                              │
│                     <Select>                     <Finish>                    │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

**操作说明**：

<kbd>↑</kbd><kbd>↓</kbd>：选择选项。  
<kbd>←</kbd><kbd>→</kbd>：切换菜单（Select / Finish）。  

![raspi-config](raspi-config.png)

## 1 Change User Password
raspbian 默认账户为 pi，默认密码为 raspberry。  
该项可修改默认密码：

![1-Change_User_Password](./raspi-config/1-Change_User_Password/1-Change_User_Password.png)

## 2 Hostname
raspbian 默认机器名称为 raspberrypi，该项可修改：

![2-Hostname-Edit](./raspi-config/2-Hostname/2-Hostname-Edit.png)

## 4 Localisation Options
此项可设置语言、时区、键盘布局 和 WiFi 国家等本地化配置：

![4-Localisation_Options-Items](./raspi-config/4-Localisation_Options/4-Localisation_Options-Items.png)

- [] en_GB.UTF-8 UTF-8  
- [*] en_US.UTF-8 UTF-8  
- [*] zh_CN.GBK GBK  
- [*] zh_CN.UTF-8 UTF-8  

![4-Localisation_Options-Change_Locale](./raspi-config/4-Localisation_Options/4-Localisation_Options-Change_Locale.png)

## 5 Interfacing Options
此项可配置一些接口选项，对应 GUI 图形界面的系统偏好菜单 `Preferences | Raspberry Pi Configuration | Interfaces`。

默认全部为 Disabled 状态，建议开启 SSH、VNC、Serial 三项。  
以下选择VNC进入设置为 enabled 状态：

![5-Interfacing_Options-P3_VNC](./raspi-config/5-Interfacing_Options/5-Interfacing_Options-P3_VNC.png)

![5-Interfacing_Options-P3_VNC-switch](./raspi-config/5-Interfacing_Options/5-Interfacing_Options-P3_VNC-switch.png)

## 7 Advanced Options
### A1 Expand Filesystem
之前的 Raspberry Pi 2，默认只能识别 4GB 的 SD 存储空间，需要 Expand Filesystem 才能识别整个 SD 卡的存储空间。

![A1-Expand_Filesystem](./raspi-config/7-Advanced_Options/A1-Expand_Filesystem/A1-Expand_Filesystem.png)

![A1-Expand_Filesystem-result](./raspi-config/7-Advanced_Options/A1-Expand_Filesystem/A1-Expand_Filesystem-result.png)

实际上，Raspberry Pi 3 默认已经能够识别整个 SD 卡的存储空间了，无需再执行此步骤。

### A3 Memory Split
依据 [VNC Connect and Raspberry Pi](https://www.realvnc.com/en/connect/docs/raspberry-pi.html) 的建议，可将 GPU 缓存从默认的 64 MB 扩大到 128 MB：

![A3-Memory_Split](./raspi-config/7-Advanced_Options/A3-Memory_Split/A3-Memory_Split.png)

![A3-Memory_Split-Edit](./raspi-config/7-Advanced_Options/A3-Memory_Split/A3-Memory_Split-Edit.png)

### A5 Resolution
raspbian 默认分辨率为 720x480，可以将其调整到支持的最高分辨率 —— 1080P。

![A5-Resolution](./raspi-config/7-Advanced_Options/A5-Resolution/A5-Resolution.png)

![A5-Resolution-Choose](./raspi-config/7-Advanced_Options/A5-Resolution/A5-Resolution-Choose.png)