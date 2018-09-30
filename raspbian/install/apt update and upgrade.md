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

携带 `--installed` 选项可列举查询已安装的软件包。

查询已安装的 vim 软件包：

```shell
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

```shell
pi@raspberrypi:~$ apt list --installed | grep markdown

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

markdown/stable,now 1.0.1-9 all [installed]
python-markdown-doc/stable,now 2.6.8-1 all [installed]
python3-markdown/stable,now 2.6.8-1 all [installed]
```

### --upgradable

携带 `--installed` 选项可查询是否有可更新的软件：

```shell
pi@raspberrypi:~$ apt list --upgradable 
Listing... Done
```

## apt-cache

**apt-cache** - query the APT cache

- apt-cache performs a variety of operations on APT's package cache.  
- apt-cache provide operations to search and generate interesting output from the package metadata that is acquired and updated via the 'update' command of e.g.  apt-get.  

执行 `apt-cache search markdown` 命令搜索 debian 软件源本地索引列表中 markdown 相关的软件包：

```shell
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

在执行 `apt-get install`，经常提示有些包是自动被安装，但是已经不再需要（可能依赖它的包已经卸载）：

```shell
Reading state information... Done
The following packages were automatically installed and are no longer required:
  fcitx-libs fonts-arphic-bsmi00lp fonts-arphic-gbsn00lp fonts-wqy-microhei
  fonts-wqy-zenhei libicu48 liblcms1 liblua5.1-0 libopencc1 libscim8v5
  libtiff4 scim-im-agent scim-modules-socket
Use 'sudo apt autoremove' to remove them.
```

**`autoremove`** is used to remove packages that were automatically installed to satisfy dependencies for other packages and are `now no longer needed as dependencies` changed or the package(s) needing them were removed in the meantime.

按照提示，可执行 `sudo apt autoremove` 删除这些残存包，以释放磁盘空间：

```shell
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

`man apt-get` 的 FILES 章节列举了 apt-get 的配置文件。

## sources.list

```shell
# man sources.list
SOURCES.LIST(5)                              APT                              SOURCES.LIST(5)

NAME
       sources.list - List of configured APT data sources

DESCRIPTION
       The source list /etc/apt/sources.list and the files contained in
       /etc/apt/sources.list.d/ are designed to support any number of active sources and a
       variety of source media. The files list one source per line (one-line style) or
       contain multiline stanzas defining one or more sources per stanza (deb822 style), with
       the most preferred source listed first (in case a single version is available from
       more than one source). The information available from the configured sources is
       acquired by apt-get update (or by an equivalent command from another APT front-end).

SOURCES.LIST.D
       The /etc/apt/sources.list.d directory provides a way to add sources.list entries in
       separate files. Two different file formats are allowed as described in the next two
       sections. Filenames need to have either the extension .list or .sources depending on
       the contained format. The filenames may only contain letters (a-z and A-Z), digits
       (0-9), underscore (_), hyphen (-) and period (.) characters. Otherwise APT will print
       a notice that it has ignored a file, unless that file matches a pattern in the
       Dir::Ignore-Files-Silently configuration list - in which case it will be silently
       ignored.
```

## edit-sources

**`edit-sources`** lets you edit your sources.list(5) files in your preferred texteditor while also providing basic sanity checks.

```shell
pi@raspberrypi:~ $ apt edit-sources
E: Could not open lock file /etc/apt/sources.list - open (13: Permission denied)

pi@raspberrypi:~ $ sudo apt edit-sources

Select an editor.  To change later, run 'select-editor'.
  1. /bin/ed
  2. /bin/nano        <---- easiest
  3. /usr/bin/vim.basic
  4. /usr/bin/vim.nox

Choose 1-4 [2]:
```

## 更新 sources.list

执行 `sudo vim /etc/apt/sources.list` 启动 vim 编辑，注释掉原来的 `deb http://... stretch main contrib non-free rpi`，添加中科大的 deb 和 deb-src。

```shell
pi@raspberrypi:~$ cat /etc/apt/sources.list
# comment by thomasfan, 27Sept17.
#deb http://mirrordirector.raspbian.org/raspbian/ stretch main contrib non-free rpi
# Uncomment line below then 'apt-get update' to enable 'apt-get source'
#deb-src http://archive.raspbian.org/raspbian/ stretch main contrib non-free rpi

#中科大
#deb http://mirrors.ustc.edu.cn/raspbian/raspbian/ stretch main contrib non-free rpi
#deb-src http://mirrors.ustc.edu.cn/raspbian/raspbian/ stretch main contrib non-free rpi

#阿里云
deb http://mirrors.aliyun.com/raspbian/raspbian/ stretch main contrib non-free rpi
deb-src http://mirrors.aliyun.com/raspbian/raspbian/ stretch main contrib non-free rpi

#清华大学
#deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ stretch main contrib non-free rpi
#deb-src http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ stretch main contrib non-free rpi
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

```shell
pi@raspberrypi:~$ cat /etc/apt/sources.list.d/raspi.list
# comment by thomasfan, 03Oct17.
#deb http://archive.raspberrypi.org/debian/ stretch main ui
# Uncomment line below then 'apt-get update' to enable 'apt-get source'
#deb-src http://archive.raspberrypi.org/debian/ stretch main ui

#中科大
deb http://mirrors.ustc.edu.cn/archive.raspberrypi.org/debian/ stretch main ui
deb-src http://mirrors.ustc.edu.cn/archive.raspberrypi.org/debian/ stretch main ui

#阿里云
deb http://mirrors.aliyun.com/debian/ stretch main contrib non-free
deb-src http://mirrors.aliyun.com/debian/ stretch main contrib non-free
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
> [树莓派Raspberry Pi 3 使用阿里云镜像云](https://www.douban.com/note/617546331/)  

## [清除 apt-get update 失败后的缓冲文件](http://blog.csdn.net/wangmi0354/article/details/50836398)

**原因**：当update不成功，直接upgrade会提示失败。  
此外如更换了软件源，也会需要清除缓存数据。  
(这一步更具需求选择执行)

```shell
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

```shell
# sudo apt-get update
```

2. **upgrade** all your installed packages to their latest versions  

```shell
# sudo apt-get upgrade
```

1Oct18: Unpacking raspberrypi-kernel (1.20180919-1) over (1.20171029-1)

3. Upgrade any held back packages:

```shell
# sudo apt-get dist-upgrade
```

## apt-secure issue

```shell
pi@raspberrypi:~ $ sudo apt-get update
Hit:1 http://mirrors.ustc.edu.cn/raspbian/raspbian stretch InRelease
Ign:2 http://mirrors.ustc.edu.cn/archive.raspberrypi.org stretch InRelease
Err:3 http://mirrors.ustc.edu.cn/archive.raspberrypi.org stretch Release
  404  Not Found [IP: 202.38.95.110 80]
Reading package lists... Done
E: The repository 'http://mirrors.ustc.edu.cn/archive.raspberrypi.org stretch Release' does no longer have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
```

执行 `man apt-secure` 查看手册：**apt-secure** - Archive authentication support for APT.

**解决方案**：

> 由于中科大的源未提供 release 文件，导致报错。可以暂时屏蔽 `ustc` 的源，启用 `aliyun` 或 `tsinghua` 的源。

### nodesource

[The repository... does not have a Release file](https://github.com/nodesource/distributions/issues/541)  

> You're seeing this error because of a [PPA](http://ppa.launchpad.net/kaihengfeng/lp1292830/ubuntu) on Launchpad  
> the error is caused by a PPA somewhere in `/etc/apt/sources.list.d` that is actually nothing to do with nodesource. 
>> The solution is to remove or update that PPA path.

1. open `/etc/sources.list.d/nodesource.list` with your favorite text editor.  
2. remove the "s" from "https://" making it "http://" in both lines  
3. save the file.  
4. `apt-get update` && `apt-get install` ....  

> 无效，现在已经是 http 报错。

### ubuntuforums

[Error on running software update](https://ubuntuforums.org/showthread.php?t=2358141&s=c81a3cf63cd93fee22e0ff189a619a7e)  

It looks like there is no connection to the repository on the server your using.  
try changing servers and then

```shell
sudo apt-get autoclean
sudo apt-get clean
sudo apt-get update
```

I was connecting to the main server changed it to India and it is working now.

> 得换 https 源，但现在默认都是 http 源？

### askubuntu

[Force update from unsigned repository Ubuntu 16.04](https://askubuntu.com/questions/732985/force-update-from-unsigned-repository-ubuntu-16-04)

You can bypass some important safeguards by using the following option:

`--allow-unauthenticated`

From the man pages for apt-get:

```shell
# man apt-get

       --allow-unauthenticated
           Ignore if packages can't be authenticated and don't prompt about it. This can be useful while
           working with local repositories, but is a huge security risk if data authenticity isn't
           ensured in another way by the user itself. The usage of the Trusted option for sources.list(5)
           entries should usually be preferred over this global override. Configuration Item:
           APT::Get::AllowUnauthenticated.
```

But be a little cautious about using this option more widely, the safeguards are in place to protect your computer not limit your freedom...

You can set options in your sources.list:

```shell
deb [trusted=yes] http://www.deb-multimedia.org jessie main
deb [allow-insecure=yes] http://www.deb-multimedia.org jessie main
```

> 可行。

### stackexchange

[Why getting this ouput for apt update?](https://unix.stackexchange.com/questions/388599/why-getting-this-ouput-for-apt-update)  

`ppa.launchpad.net`？

```shell
sudo rm -i /etc/apt/sources.list.d/tmsu-ubuntu-daily-artful.list
sudo apt update
```