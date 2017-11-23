macOS 通过 OpenSSH 连接 raspbian，然后 ls 列举目录下的中文乱码：

```Shell
pi@raspberrypi:~ $ ls Pictures/
4.JPG       ?????????-?????????.JPG   ?????????-?????????.JPG  ????????????.png
Scrot       ?????????-?????????2.JPG  ??????.JPG
System.png  ?????????-??????.JPG      ??????-2.png
pi@raspberrypi:~ $ 
```

检查 raspi-config 中的 `Localisation Options` 一切如初。

执行 `locale` 或 `locale -a` 提示 `locale: Cannot set LC_CTYPE to default locale: No such file or directory`：

```Shell
pi@raspberrypi:~ $ locale -a
locale: Cannot set LC_CTYPE to default locale: No such file or directory
C
C.UTF-8
en_US.utf8
POSIX
zh_CN
zh_CN.gb18030
zh_CN.gb2312
zh_CN.gbk
zh_CN.utf8
```

```Shell
pi@raspberrypi:~ $ locale
locale: Cannot set LC_CTYPE to default locale: No such file or directory
locale: Cannot set LC_ALL to default locale: No such file or directory
LANG=en_US.UTF-8
LANGUAGE=
LC_CTYPE=UTF-8
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=
```

尝试 export 修改 LC_CTYPE 为当初的 `en_US.UTF-8`，重新执行 locale 命令恢复正常：

```Shell
pi@raspberrypi:~ $ export LC_CTYPE="en_US.UTF-8"
pi@raspberrypi:~ $ echo $LC_CTYPE 
en_US.UTF-8
pi@raspberrypi:~ $ locale
LANG=en_US.UTF-8
LANGUAGE=
LC_CTYPE=en_US.UTF-8
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=
```

重新执行 `ls Pictures/`，恢复正常显示中文字符：

```Shell
pi@raspberrypi:~ $ ls Pictures/
4.JPG  System.png         三角山-俯瞰图2.JPG  三角山-灵秀山.JPG  绿叶-2.png
Scrot  三角山-一枝杉.JPG  三角山-枯松.JPG     坳口.JPG           范式家训.png
```

## references
[locale的设定中LANG、LC_ALL、LANGUAGE环境变量的区别](http://blog.csdn.net/nick357/article/details/8513699)  
[Linux中Locale及shell编码问题](http://www.drupal001.com/2012/04/shell-utf8/)  
[linux环境通过ssh连接控制台显示中文乱码问题](http://blog.csdn.net/songylwq/article/details/8842748)  
[解决Debian SSH中文乱码](http://linji.cn/4015.html)  
[Debian SSH乱码万能解决方案](http://www.zxsdw.com/index.php/archives/265/)  
[Debian控制台中文为乱码，ssh登录乱码](http://forum.ubuntu.org.cn/viewtopic.php?t=247291)  
