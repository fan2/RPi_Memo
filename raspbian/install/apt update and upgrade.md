# [APT (Debian)](https://en.wikipedia.org/wiki/APT_(Debian))  
Apt: [en](https://wiki.debian.org/Apt) / [cn](https://wiki.debian.org/zh_CN/Apt)  
[APT HOWTO (Obsolete Documentation) ](https://www.debian.org/doc/manuals/apt-howto/)  

debian 下的 deb 包可以把一个应用的文件打包在一起，大体就如同 Windows 上的安装文件。  

**apt** provides a high-level commandline interface for the package management system.  

- Provides commands for *searching* and *managing* as well as *querying* information about packages.  
- Apt can be considered a front-end to [dpkg](https://en.wikipedia.org/wiki/Dpkg). Three such programs are `apt`, `apt-get` and `apt-cache`.  

Most used commands:

- **list** - list packages based on package names  
- **search** - search in package descriptions  
- **show** - show package details  
- **install** - install packages  
- **remove** - remove packages  
- **autoremove** - Remove automatically all unused packages  
- **update** - update（同步索引） list of available packages  
- **upgrade** - upgrade（升级更新） the system by installing/upgrading packages  
- **full-upgrade** - upgrade the system by removing/installing/upgrading packages  
- **edit-sources** - edit the source information file  

## apt list
**list** is somewhat similar to **dpkg-query** --list in that it can display a list of packages satisfying certain criteria.  
It supports glob(7) patterns for matching package names as well as options to list installed (`--installed`), upgradeable (`--upgradeable`) or all available (`--all-versions`) versions.  

### --installed
携带 --installed 选项可列举查询已安装的软件包。

查询已安装的 vim 软件包：

```Shell
pi@raspberrypi:~$ apt list --installed | grep vim

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

vim/stable,now 2:8.0.0197-4 armhf [installed]
vim-addon-manager/stable,now 0.5.6 all [installed,automatic]
vim-common/stable,now 2:8.0.0197-4 all [installed,automatic]
vim-nox/stable,now 2:8.0.0197-4 armhf [installed,automatic]
vim-runtime/stable,now 2:8.0.0197-4 all [installed,automatic]
vim-voom/stable,now 5.2-1 all [installed]
```

查询已安装的 markdown 软件包：

```Shell
pi@raspberrypi:~$ apt list --installed | grep markdown

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

markdown/stable,now 1.0.1-9 all [installed]
python-markdown-doc/stable,now 2.6.8-1 all [installed]
python3-markdown/stable,now 2.6.8-1 all [installed]
```

### --upgradable
查询是否有可更新的软件：

```Shell
pi@raspberrypi:~$ apt list --upgradable 
Listing... Done
```

## apt-cache
**apt-cache** - query the APT cache

- apt-cache performs a variety of operations on APT's package cache.  
- apt-cache provide operations to search and generate interesting output from the package metadata that is acquired and updated via the 'update' command of e.g.  apt-get.  

执行 `apt-cache search markdown` 命令搜索 debian 软件源本地索引列表中 markdown 相关的软件包：

```Shell
pi@raspberrypi:~/Projects/retext$ apt-cache search markdown
...

cmark - CommonMark parsing and rendering program
discount - implementation of the Markdown markup language in C

grip - Preview GitHub Markdown files like Readme locally

markdown - Text-to-HTML conversion tool

pandoc - general markup converter
pandoc-data - general markup converter - data files

python-markdown - text-to-HTML conversion library/tool (Python 2 version)
python3-markdown - text-to-HTML conversion library/tool (Python 3 version)

retext - Simple text editor for Markdown and reStructuredText

ruby-github-markdown - Markdown parser for GitHub.com
ruby-github-markup - GitHub Markup rendering

...
```

- 执行 `apt-cache showpkg markdown` 可查看 markdown 软件源信息，例如 **Dependencies**、Reverse Depends；  
- 执行 `apt-cache show markdown` 可查看 markdown 安装包信息，例如 **Description**、Homepage、Section（所属分类）；  
- 执行 `apt-cache showsrc markdown` 可查看 markdown 源代码信息，例如 **Homepage**、Maintainer、*Architecture*、Version、Section（所属分类）；  
- 执行 `apt-cache depends markdown` 命令可查看 markdown 软件包**依赖**关系；  
- 执行 `apt-cache rdepends markdown` 命令可查看 markdown 软件包**被依赖**关系；  

## apt-get
**apt-get** - APT package handling utility

- apt-get is the command-line tool for handling packages, and may be considered the user's "back-end" to other tools using the APT library.  
- Several "front-end" interfaces exist, such as aptitude(8), synaptic(8) and wajig(1).  

**aptitude** - high-level interface to the package manager.

- aptitude is a text-based interface to the Debian GNU/Linux package system.
- Actions may be performed from a visual interface or from the command-line.

[`apt-get`](http://man.linuxde.net/apt-get) 命令是 Debian Linux 发行版中的 APT 软件包管理工具，所有基于 Debian 的发行都使用这个包管理系统。  

## autoremove
在执行 `apt-get install`，经常提示有些包是自动安装但是并不再需要（可能依赖的包已经卸载）：

```Shell
Reading state information... Done
The following packages were automatically installed and are no longer required:
  fcitx-libs fonts-arphic-bsmi00lp fonts-arphic-gbsn00lp fonts-wqy-microhei
  fonts-wqy-zenhei libicu48 liblcms1 liblua5.1-0 libopencc1 libscim8v5
  libtiff4 scim-im-agent scim-modules-socket
Use 'sudo apt autoremove' to remove them.
```

按照提示，可执行 `sudo apt autoremove` 删除这些残存包，以释放磁盘空间：

```Shell
pi@raspberrypi:~$ sudo apt autoremove
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages will be REMOVED:
  fcitx-libs fonts-arphic-bsmi00lp fonts-arphic-gbsn00lp fonts-wqy-microhei
  fonts-wqy-zenhei libicu48 liblcms1 liblua5.1-0 libopencc1 libscim8v5
  libtiff4 scim-im-agent scim-modules-socket
0 upgraded, 0 newly installed, 13 to remove and 0 not upgraded.
Do you want to continue? [Y/n] Y
Progress: [ 97%] [########################################################..] 
```

此外，在执行 `sudo apt-get install pkg` 之前可以执行 `sudo apt-get autoremove pkg`，删掉本地可能已安装的旧版 pkg。

# [Mirrors](https://www.raspbian.org/RaspbianMirrors)
Asia | China

## 更新 sources.list
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

#阿里云
#deb http://mirrors.aliyun.com/raspbian/raspbian/ stretch main contrib non-free  
rpi
#deb-src http://mirrors.aliyun.com/raspbian/raspbian/ stretch main contrib non-ff
ree rpi

#清华大学 
#deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ stretch main contribb
 non-free rpi
#deb-src http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ stretch main conn
trib non-free rpi
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

## 更新 sources.list.d/raspi.list
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

## [清除 apt-get update 失败后的缓冲文件](http://blog.csdn.net/wangmi0354/article/details/50836398)
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


# [UPDATING AND UPGRADING RASPBIAN](https://www.raspberrypi.org/documentation/raspbian/updating.md)
> [How do I upgrade Raspbian?](https://raspberrypi.stackexchange.com/questions/4020/how-do-i-upgrade-raspbian)  
> [How to Update Raspbian: All you need to know!](https://pimylifeup.com/update-raspbian/)  

## update & upgrade
1. **update** your system's package list  

```Shell
# sudo apt-get update
```

2. **upgrade** all your installed packages to their latest versions  

```Shell
# sudo apt-get upgrade
```

3. Upgrade any held back packages:

```Shell
# sudo apt-get dist-upgrade
```
