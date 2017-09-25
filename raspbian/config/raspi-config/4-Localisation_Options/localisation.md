# localisation

## Change Locale
执行 `sudo raspi-config`，依次选择 4 Localisation Options | I1 Change Locale，

- 用空格键反选：[] en_GB.UTF-8 UTF-8  
- 用空格键选中：[*] en_US.UTF-8 UTF-8  
- 用空格键选中：[*] zh_CN.GBK GBK  
- 用空格键选中：[*] zh_CN.UTF-8 UTF-8  

依次用空格键选中3项后，tab键移到Ok确认，返回根据需要选择默认语言：

- 英语：[*] en_US.UTF-8 UTF-8  
- 汉语：[] zh_CN.UTF-8 UTF-8  

## install fonts
1. 同步更新 apt 仓库列表信息：

```Shell
sudo apt-get update 
```

2. 为 raspbian 系统安装中文字库：

```Shell
sudo apt-get install ttf-wqy-zenhei
sudo apt-get install ttf-wqy-microhei
```

## Input Method
[树莓派(Raspberry Pi 3) - Raspbian中文输入法安装及中文环境配置](http://blog.csdn.net/u012313335/article/details/53519302)  

安装 scim 及拼音：

```Shell
sudo apt-get install scim
sudo apt-get install scim-tables-zh
sudo apt-get install scim-pinyin
```

或者安装 fcitx 及五笔：

```Shell
sudo apt-get install fcitx
sudo apt-get install fcitx-tables-wbpy
```

## references
[树莓派设置支持中文](http://www.jianshu.com/p/00fc5725d3fc)  
[如何让树莓派显示中文？](http://shumeipai.nxez.com/2016/03/13/how-to-make-raspberry-pi-display-chinese.html)  
[树莓派中文支持(中文显示和中文输入法)](http://blog.csdn.net/rocklee/article/details/50083031)  
[树莓派 中文乱码 解决方法](http://blog.csdn.net/y511374875/article/details/73548195)  
[树莓派(Raspberry Pi 3) - Raspbian中文输入法安装及中文环境配置](http://blog.csdn.net/u012313335/article/details/53519302)  
