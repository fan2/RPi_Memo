## 入门
[树莓派初识](http://blog.csdn.net/iluzhiyong/article/details/77791646)  
[树莓派折腾录](http://blog.csdn.net/wangmi0354/article/details/50836398)  

## 快捷键
<kbd>control</kbd>+<kbd>D</kbd>：显示桌面。

## 分辨率
[自定义树莓派的显示分辨率](http://shumeipai.nxez.com/2013/08/31/custom-display-resolution-raspberry-pie.html)  
[树莓派3B+ Raspbian桌面分辨率设置](http://www.jianshu.com/p/a65b295eb285)  

接显示器默认的分辨率太高，有可能会导致树莓派功率支持不住，屏幕闪或者出横线，建议折中设置成 1280x720p。

## 耳机
默认音频输出只有HDMI，如果需要用3.5mm耳机插头，需要到设置里设成 ”HDMI+Analog” 同时输出。

## 设置静态 IP

## vi
使用vi的时候，按方向键会出现字母，而不是移动光标，是因为vi不是完整版，先卸载vi，再安装vim：

```Shell
sudo apt-get remove vim-common
sudo apt-get install vim
```