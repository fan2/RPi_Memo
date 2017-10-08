## SoC & OS

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

## 入门
[树莓派初识](http://blog.csdn.net/iluzhiyong/article/details/77791646)  
[树莓派折腾录 系列](http://blog.csdn.net/wangmi0354/article/details/50836398)  
[树莓派 Learning 系列](http://blog.csdn.net/github_35160620/article/details/52038918)  
[树莓派应用实践系列](http://blog.csdn.net/huayucong/article/category/5662059/)  
[安装Debian后的基本配置](http://blog.csdn.net/shennongminblog/article/details/76158400)  

## 快捷键
<kbd>control</kbd>+<kbd>D</kbd>：显示桌面。

## 分辨率
[自定义树莓派的显示分辨率](http://shumeipai.nxez.com/2013/08/31/custom-display-resolution-raspberry-pie.html)  
[树莓派3B+ Raspbian桌面分辨率设置](http://www.jianshu.com/p/a65b295eb285)  

raspbian 默认分辨率为 720x480，可以将其调整到支持的最高分辨率 —— 1080P（DMT Mode 82 1920x1080 60Hz 16:9）。

但是 1080P 分辨率太高，有可能会导致树莓派功率支持不住，屏幕闪或者出横线，建议折中设置成 720P（DMT Mode 85 1280x720 60Hz 16:9）。

## 耳机
默认音频输出只有HDMI，如果需要用3.5mm耳机插头，需要到设置里设成 ”HDMI+Analog” 同时输出。

## vi
使用vi的时候，按方向键会出现字母，而不是移动光标，是因为vi不是完整版，先卸载vi，再安装vim：

```Shell
sudo apt-get remove vim-common
sudo apt-get install vim
```

### [VOoM]([https://github.com/vim-voom/VOoM](https://github.com/vim-voom/VOoM))
**vim-voom** - Vim two-pane outliner

```Shell
pi@raspberrypi:~$ apt-cache search vimoutliner
vim-vimoutliner - script for building an outline editor on top of Vim
vim-voom - Vim two-pane outliner
```

执行 `apt-cache show vim-voom` 命令查看 vim-voom 软件包信息

- Homepage: http://www.vim.org/scripts/script.php?script_id=2657  
- Filename: pool/main/v/vim-voom/vim-voom_5.2-1_all.deb  

按下 <kbd>Q</kbd> 进入 Ex 命令模式，输入 :Voom markdown 开启 markdown TOC outline。

> [VOoM(原VOOF)：vim实现带折叠双栏树状文本管理](http://xbeta.info/vim-voof.htm)  

### vim-pandoc
[vim-pandoc](https://github.com/vim-pandoc/vim-pandoc) - pandoc integration and utilities for vim

