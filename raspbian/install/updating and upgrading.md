# [UPDATING AND UPGRADING RASPBIAN](https://www.raspberrypi.org/documentation/raspbian/updating.md)

## [APT (Debian)](https://en.wikipedia.org/wiki/APT_(Debian))  
Apt: [en](https://wiki.debian.org/Apt) / [cn](https://wiki.debian.org/zh_CN/Apt)  
[APT HOWTO (Obsolete Documentation) ](https://www.debian.org/doc/manuals/apt-howto/)  

[`apt-get`](http://man.linuxde.net/apt-get) 命令是 Debian Linux 发行版中的 APT 软件包管理工具，所有基于 Debian 的发行都使用这个包管理系统。  
deb 包可以把一个应用的文件包在一起，大体就如同 Windows 上的安装文件。  

## update & upgrade
1. **update** your system's package list  

```Shell
# apt-get update
```

2. **upgrade** all your installed packages to their latest versions  

```Shell
# apt-get upgrade
```

Upgrade any held back packages:

```Shell
# apt-get dist-upgrade
```

## [How do I upgrade Raspbian?](https://raspberrypi.stackexchange.com/questions/4020/how-do-i-upgrade-raspbian)

## [Raspbian GNU/Linux upgrade from Jessie to Raspbian Stretch 9](https://linuxconfig.org/raspbian-gnu-linux-upgrade-from-jessie-to-raspbian-stretch-9)

Start by fully upgrade your current Raspbian system before you proceed with a Stretch upgrade.

## [How to Update Raspbian: All you need to know!](https://pimylifeup.com/update-raspbian/)
