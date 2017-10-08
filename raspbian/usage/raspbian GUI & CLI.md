# SoC & OS

- **SoC**：`Raspberry Pi 3 Model B v1.2`(2015)  
- **OS**：`2017-09-07-raspbian-stretch.zip`  

```Shell
pi@raspberrypi:~ $ cat /proc/version
Linux version 4.9.41-v7+ (dc4@dc4-XPS13-9333) (gcc version 4.9.3 (crosstool-NG crosstool-ng-1.22.0-88-g8460611) ) #1023 SMP Tue Aug 8 16:00:15 BST 2017

pi@raspberrypi:~ $ lsb_release -a
No LSB modules are available.
Distributor ID:	Raspbian
Description:	Raspbian GNU/Linux 9.1 (stretch)
Release:	9.1
Codename:	stretch
```

# UI

- GUI (Graphical User Interface)
- CLI(Command Line Interface) / CUI(Console User Interface)

## GUI

![GUI-layers-Window_Manager](https://upload.wikimedia.org/wikipedia/commons/9/95/Schema_of_the_layers_of_the_graphical_user_interface.svg)

![Window_System](https://upload.wikimedia.org/wikipedia/commons/1/14/Window_%28windowing_system%29.svg)

## [X Window](https://www.x.org/wiki/)
[wiki](https://en.wikipedia.org/wiki/X_Window_System): X primarily defines protocol and graphics primitives  

> [What is X Window System? ](https://unix.stackexchange.com/questions/149066/what-is-x-window-system)

![X-Arch](https://upload.wikimedia.org/wikipedia/commons/0/03/X_client_server_example.svg)

A **window manager** controls the *placement* and *appearance* of application windows.  
This may result in desktop interfaces reminiscent of those of Microsoft Windows or of the Apple Macintosh (examples include GNOME 2, KDE, Xfce) or have radically different controls.  

> [Comparison of X Window System desktop environments](https://en.wikipedia.org/wiki/Comparison_of_X_Window_System_desktop_environments)  

### [KDE](https://www.kde.org/)
[wiki](https://en.wikipedia.org/wiki/KDE): K Desktop Environment

Ettrich chose to use Trolltech’s [**Qt framework**](https://en.wikipedia.org/wiki/Qt_(software)) for the KDE project

The original GPL licensed version of this toolkit only existed for platforms which used the [X11](https://en.wikipedia.org/wiki/X11) display server, but with the release of Qt 4, LGPL licensed versions are available for more platforms. This allowed KDE software based on Qt 4 or newer versions to theoretically be distributed to `Microsoft Windows` and `OS X`.

![KDE](https://upload.wikimedia.org/wikipedia/commons/5/54/KDE_4.png)

### [GNOME](https://www.gnome.org/)
[wiki](https://en.wikipedia.org/wiki/GNOME): is a desktop environment composed of free and open-source software that runs on Linux and most BSD derivatives.  
In place of Qt, the [**GTK+**](https://en.wikipedia.org/wiki/GTK%2B) toolkit was chosen as the base of GNOME.  
[GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell) is the official user interface of the GNOME desktop environment.  

![GNOME-Shell](https://upload.wikimedia.org/wikipedia/commons/9/97/GNOME_Shell.png)

GNOME runs on Wayland and the X Window System Wayland support was introduced in GNOME 3.10 and prioritized them over X sessions.  

since GNOME 3, [Mutter](https://en.wikipedia.org/wiki/Mutter_(software)) replaced [Metacity](https://en.wikipedia.org/wiki/Metacity) as the default window manager.

### [Xfce](https://xfce.org/)
[wiki](https://en.wikipedia.org/wiki/Xfce) / [archlinux](https://wiki.archlinux.org/index.php/Xfce_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))  

**Xfce** is a free and open-source desktop environment for Unix and Unix-like operating systems, such as Linux, Solaris, and BSD.

Like [GNOME](https://en.wikipedia.org/wiki/GNOME), Xfce is based on the [GTK](https://en.wikipedia.org/wiki/GTK) toolkit but it is not a GNOME fork. It uses the Xfwm [window manager](https://en.wikipedia.org/wiki/Window_manager).

![Xfce-4.4](https://upload.wikimedia.org/wikipedia/commons/7/71/Xfce-4.4.png)

> [Xfce之所以大行其道的七大原因](http://www.linuxidc.com/Linux/2015-08/121517.htm)  
> [KDE、GNOME和XFCE的三款Linux桌面对比](http://www.sohu.com/a/73173138_185201)  

### [LXDE](http://lxde.org/)
[**LXDE**](https://en.wikipedia.org/wiki/LXDE)(Lightweight X11 Desktop Environment) is a free desktop environment with comparatively low resource requirements.  
The goal of the project is to provide a desktop environment that is fast and energy efficient.  
LXDE is written in the C programming language, using the [GTK+](https://en.wikipedia.org/wiki/GTK%2B) 2 toolkit.  

![LXDE_desktop_full](https://upload.wikimedia.org/wikipedia/commons/4/4c/LXDE_desktop_full.png)

Components         | Descriptions
-------------------|-----------------------
PCMan File Manager | File manager and Desktop metaphor provider
LXInput            | Mouse and keyboard configuration tool
LXLauncher         | Easy-mode application launcher
LXPanel            | Desktop panel
LXSession          | X session manager
LXAppearance       | GTK+ theme switcher
GPicView           | Image viewer
LXMusic            | A frontend for the XMMS2 audio player
LXTerminal         | Terminal emulator
LXTask             | Task manager
LXRandR            | A GUI to RandR
LXDM               | X display manager
LXNM               | Lightweight network connection helper daemon
Leafpad            | Text editor
Openbox            | Window manager
ObConf             | A GUI tool to configure Openbox
Xarchiver          | File archiver

> [LXDE in Debian](https://wiki.debian.org/LXDE): Running LXDE  
> [lubuntu](http://lubuntu.me/)/[wiki](https://en.wikipedia.org/wiki/Lubuntu)  

#### PIXEL
[**PIXEL**](https://www.raspberrypi.org/blog/introducing-pixel/)(Pi Improved Xwindows Environment Lightweight): a fork (or a branch) of LXDE,  default desktop environment of Raspbian Stretch.  

桌面版 raspbian（RASPBIAN STRETCH WITH DESKTOP）默认搭载的图形视窗系统是 [PIXEL](https://fossbytes.com/raspberry-pi-adds-a-new-pixel-to-raspbian-linux-distro/) —— 针对 Pi 高度定制的轻量级 X11 Window 桌面环境。  

执行 `raspi-config` 选择进入 `3 Boot Options`，点击进入 `B1 Desktop / CLI`：

```Shell
B1 Desktop / CLI                 Choose whether to boot into a desktop  
```

有四种启动方式可供选择：

- B1 Console  
- B2 Console Autologin  
- B3 Desktop  
- B4 Desktop  Autologin - default  

如果按 B1/B2 的 CUI 非 GUI 的命令行 lite 模式启动 raspbian，可在命令行键入 `sudo startlxde` 切换到图形用户界面。

# references
[使用Raspbian图形用户界面](http://www.epubit.com.cn/book/onlinechapter/33817)  
[树莓派Raspbian系统定制 - LXDE桌面系统定制 - 基本概念](http://blog.csdn.net/inmyhouse123/article/details/47151865)  
[配置树莓派自动登录 Raspbian 图形界面 LXDE](http://shumeipai.nxez.com/2015/02/27/raspberry-pi-configured-to-automatically-log-lxde.html)  
[树梅派应用49：配置树莓派自动登录 Raspbian 图形界面 LXDE](http://blog.csdn.net/huayucong/article/details/54406726)  

[How To Properly Remove LXDE And Install XFCE On Raspbian](http://linuxg.net/how-to-properly-remove-lxde-and-install-xfce-on-raspbian-debian-for-raspberry-pi/)  
[Raspbian Lite with PIXEL/LXDE/XFCE/MATE/i3 GUI](https://www.raspberrypi.org/forums/viewtopic.php?f=66&t=133691&sid=a349228419d0b6936f88bd0d2c1aea7b)  
raspbian-lite-安装-pixel-lxde-xfce-mate-openbox-界面：[上](https://wangmingg.tk/2017/04/15/raspbian-lite-%E5%AE%89%E8%A3%85-pixellxdexfcemateopenbox-%E7%95%8C%E9%9D%A2%EF%BC%88%E4%B8%8A%EF%BC%89/) [下](https://wangmingg.tk/2017/04/15/raspbian-lite-%E5%AE%89%E8%A3%85-pixellxdexfcemateopenbox-%E7%95%8C%E9%9D%A2%EF%BC%88%E4%B8%8B%EF%BC%89/)  
