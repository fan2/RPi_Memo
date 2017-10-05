# [UPDATING AND UPGRADING RASPBIAN](https://www.raspberrypi.org/documentation/raspbian/updating.md)

## [APT (Debian)](https://en.wikipedia.org/wiki/APT_(Debian))  
Apt: [en](https://wiki.debian.org/Apt) / [cn](https://wiki.debian.org/zh_CN/Apt)  
[APT HOWTO (Obsolete Documentation) ](https://www.debian.org/doc/manuals/apt-howto/)  

[`apt-get`](http://man.linuxde.net/apt-get) 命令是 Debian Linux 发行版中的 APT 软件包管理工具，所有基于 Debian 的发行都使用这个包管理系统。  
deb 包可以把一个应用的文件包在一起，大体就如同 Windows 上的安装文件。  

## update & upgrade
1. **update** your system's package list  

```Shell
# sudo apt-get update
```

2. **upgrade** all your installed packages to their latest versions  

```Shell
# sudo apt-get upgrade
```

Upgrade any held back packages:

```Shell
# sudo apt-get dist-upgrade
```

## [How do I upgrade Raspbian?](https://raspberrypi.stackexchange.com/questions/4020/how-do-i-upgrade-raspbian)

## [Raspbian GNU/Linux upgrade from Jessie to Raspbian Stretch 9](https://linuxconfig.org/raspbian-gnu-linux-upgrade-from-jessie-to-raspbian-stretch-9)

Start by fully upgrade your current Raspbian system before you proceed with a Stretch upgrade.

## [How to Update Raspbian: All you need to know!](https://pimylifeup.com/update-raspbian/)

## [Mirrors](https://www.raspbian.org/RaspbianMirrors)
Asia | China
### 更新 sources.list
执行 `sudo vim /etc/apt/sources.list` 启动编辑，注释掉原来的 `deb http://... stretch main contrib non-free rpi`，添加中科大的 deb 和 deb-src。

```Shell
pi@raspberrypi:~$ cat /etc/apt/sources.list
# comment by thomasfan, 27Sept17.
#deb http://mirrordirector.raspbian.org/raspbian/ stretch main contrib non-free rpi
# Uncomment line below then 'apt-get update' to enable 'apt-get source'
#deb-src http://archive.raspbian.org/raspbian/ stretch main contrib non-free rpi

#中科大
deb http://mirrors.ustc.edu.cn/raspbian/raspbian/ stretch main contrib non-free rpi
deb-src http://mirrors.ustc.edu.cn/raspbian/raspbian/ stretch main contrib non-free rpi

```

1. deb：软件的位置；  
2. deb-src：软件的源代码位置，一般放在同目录下的 `source/` 子文件夹下；   

**url**：镜像源 - http://mirrors.ustc.edu.cn/raspbian/raspbian/  
**dists**：发行版（distributions）；  
**stretch**：为 raspbian 发行版本号  

> http://mirrors.ustc.edu.cn/raspbian/raspbian/dists/stretch/

- *main*：debian 里最基本及主要且符合自由软件规范的软件 (packages)；  

	> http://mirrors.ustc.edu.cn/raspbian/raspbian/dists/stretch/main/

- *contrib*：此类软件虽然可以在 debian 里运作，即使本身属于自由软件，但多半却是相依于非自由 (non-free) 软件；  

	> http://mirrors.ustc.edu.cn/raspbian/raspbian/dists/stretch/contrib/

- *non-free*：不属于自由软件范畴的软件；  

	> http://mirrors.ustc.edu.cn/raspbian/raspbian/dists/stretch/non-free/

- *rpi*：raspberry pi 特有软件包。  

	> http://mirrors.ustc.edu.cn/raspbian/raspbian/dists/stretch/rpi/

### 更新 sources.list.d/raspi.list
执行 `sudo vim /etc/apt/sources.list.d/raspi.list` 启动编辑，注释掉原来的 `deb http://... stretch main ui`，添加中科大的 deb 和 deb-src。

```Shell
pi@raspberrypi:~$ cat /etc/apt/sources.list.d/raspi.list
# comment by thomasfan, 03Oct17.
#deb http://archive.raspberrypi.org/debian/ stretch main ui
# Uncomment line below then 'apt-get update' to enable 'apt-get source'
#deb-src http://archive.raspberrypi.org/debian/ stretch main ui

#中科大
deb http://mirrors.ustc.edu.cn/archive.raspberrypi.org/ stretch main ui
deb-src http://mirrors.ustc.edu.cn/archive.raspberrypi.org/ stretch main ui

```

`sources.list.d` 扩展目录下的 `raspi.list` 为 raspberry pi / raspbian 平台特有的软件源，由 raspberrypi.org 组织提供。

- <http://mirrors.ustc.edu.cn/archive.raspberrypi.org/dists/stretch/main/>  
- <http://mirrors.ustc.edu.cn/archive.raspberrypi.org/dists/stretch/ui/>  

[中科大](http://mirrors.ustc.edu.cn/raspbian/raspbian/) / [帮助](https://lug.ustc.edu.cn/wiki/mirrors/help/raspbian) / [archive.raspberrypi.org](http://mirrors.ustc.edu.cn/archive.raspberrypi.org/)  
[阿里云](http://mirrors.aliyun.com/raspbian/raspbian/) / [清华大学](http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/) / [浙江大学](http://mirrors.zju.edu.cn/raspbian/raspbian/) / [新加坡国立大学](http://mirror.nus.edu.sg/raspbian/raspbian)  

> [apt系统中sources.list文件的解析](http://blog.sina.com.cn/s/blog_406127500101dfv1.html)  
> [debian软件源source.list文件格式说明](http://www.cnblogs.com/beanmoon/p/3387652.html)  
> [树莓派折腾录一 - 3. 替换软件源](http://blog.csdn.net/wangmi0354/article/details/50836398)  
> [树莓派新版raspbian系统换国内源](http://www.des8.com/on_computer/raspbian_jessie_sources/)  
> [为树莓派 raspbian stretch 更换国内镜像源](http://blog.csdn.net/la9998372/article/details/77886806)  

### [清除 apt-get update 失败后的缓冲文件](http://blog.csdn.net/wangmi0354/article/details/50836398)
**原因**：当update不成功，直接upgrade会提示失败。  
此外如更换了软件源，也会需要清除缓存数据。  
(这一步更具需求选择执行)

```Shell
sudo rm -vf /var/lib/apt/lists/*
sudo mkdir -pv /var/lib/apt/lists/partial
sudo apt-get clean
sudo apt-get update ##rebuilds the index files
sudo apt-get upgrade
```
