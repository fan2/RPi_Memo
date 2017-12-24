macOS 通过 OpenSSH 连接 raspbian，然后 ls 列举目录下的中文乱码：

```shell
pi@raspberrypi:~ $ ls Pictures/
4.JPG       ?????????-?????????.JPG   ?????????-?????????.JPG  ????????????.png
Scrot       ?????????-?????????2.JPG  ??????.JPG
System.png  ?????????-??????.JPG      ??????-2.png
pi@raspberrypi:~ $ 
```

检查 raspi-config 中的 `Localisation Options` 一切如初。

执行 `locale` 或 `locale -a` 提示 `locale: Cannot set LC_CTYPE to default locale: No such file or directory`：

```shell
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

```shell
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

执行 `env` 命令可查看环境变量。执行 `env | grep LC_CTYPE` 命令可将 env 结果通过管道传给 grep 过滤出 LC_CTYPE 变量：

```shell
pi@raspberrypi:~ $ env | grep LANG
LANG=en_US.UTF-8
pi@raspberrypi:~ $ env | grep LC_CTYPE
LC_CTYPE=UTF-8
```

执行 `export | grep LC_CTYPE` 命令可获取等效结果：

```shell
pi@raspberrypi:~ $ export | grep LANG
declare -x LANG="en_US.UTF-8"
pi@raspberrypi:~ $ export | grep LC_CTYPE
declare -x LC_CTYPE="UTF-8"
```

执行 `set | grep LC_CTYPE` 命令也可获取等效结果：

```shell
pi@raspberrypi:~ $ set | grep LANG
LANG=en_US.UTF-8
varLANG='env LANG=$LANG' # 自定义 shell 变量

pi@raspberrypi:~ $ set | grep LC_CTYPE
LC_CTYPE=UTF-8
varLC_CTYPE='LC_CTYPE = $LC_CTYPE' # 自定义 shell 变量
    local LC_CTYPE=C;
```

> 使用 `set` 命令显示所有变量（包括环境变量与自定义变量）；使用 `unset` 命令来清除环境变量。

尝试 export 修改 LC_CTYPE 为当初的 `en_US.UTF-8`，重新执行 locale 命令可以看到 `LC_CTYPE=en_US.UTF-8`：

```shell
pi@raspberrypi:~ $ export LC_CTYPE="en_US.UTF-8"

# echo $ 打印环境变量
pi@raspberrypi:~ $ echo $LC_CTYPE 
en_US.UTF-8

pi@raspberrypi:~ $ locale
LANG=en_US.UTF-8
LANGUAGE=
LC_CTYPE=en_US.UTF-8

```

重新执行 `ls Pictures/`，正常显示中文字符：

```shell
pi@raspberrypi:~ $ ls Pictures/
4.JPG  System.png         三角山-俯瞰图2.JPG  三角山-灵秀山.JPG  绿叶-2.png
Scrot  三角山-一枝杉.JPG  三角山-枯松.JPG     坳口.JPG           范式家训.png
```

---

执行 `sudo apt-get dist-upgrade` 时也会报类似错误：

```shell
pi@raspberrypi:~ $ sudo apt-get dist-upgrade

apt-listchanges: Can't set locale; make sure $LC_* and $LANG are correct!
Reading changelogs... Done
perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
    LANGUAGE = (unset),
    LC_ALL = (unset),
    LC_CTYPE = "UTF-8",
    LANG = "en_US.UTF-8"
    are supported and installed on your system.
perl: warning: Falling back to a fallback locale ("en_US.UTF-8").
locale: Cannot set LC_CTYPE to default locale: No such file or directory
locale: Cannot set LC_ALL to default locale: No such file or directory

```

可参考《鸟哥的linux私房菜》<11.2 shell 的变量功能> - 11.2.4 影响显示结果的语系变量（locale） 。

当我们在启动某些 Perl 的程序时，它会主动去分析语系数据文件。  
如果发现有它无法解析的编码语系，可能会报错，这时可能需要修改一下语系配置。

## references

[locale的设定中LANG、LC_ALL、LANGUAGE环境变量的区别](http://blog.csdn.net/nick357/article/details/8513699)  
[Linux中Locale及shell编码问题](http://www.drupal001.com/2012/04/shell-utf8/)  
[linux环境通过ssh连接控制台显示中文乱码问题](http://blog.csdn.net/songylwq/article/details/8842748)  
[解决Debian SSH中文乱码](http://linji.cn/4015.html)  
[Debian SSH乱码万能解决方案](http://www.zxsdw.com/index.php/archives/265/)  
[Debian控制台中文为乱码，ssh登录乱码](http://forum.ubuntu.org.cn/viewtopic.php?t=247291)  
