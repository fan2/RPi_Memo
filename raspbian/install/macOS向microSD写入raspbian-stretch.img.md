
参考官方《INSTALLING OPERATING SYSTEM IMAGES ON MAC OS》 和 《Mac下安装树莓派系统raspbian》。

将 microSD 读卡器插入电脑 USB 口，默认为 “Untitiled”，重命名为 “RPi”。

## 查看 microSD 卡信息
在终端运行 `df –h` 命令查看挂载的设备：

```Shell
faner@THOMASFAN-MB0:~|⇒  df -h
Filesystem                          Size   Used  Avail Capacity iused      ifree %iused  Mounted on
/dev/disk1                         465Gi  381Gi   84Gi    83% 3642819 4291324460    0%   /
devfs                              191Ki  191Ki    0Bi   100%     661          0  100%   /dev
map -hosts                           0Bi    0Bi    0Bi   100%       0          0  100%   /net
map auto_home                        0Bi    0Bi    0Bi   100%       0          0  100%   /home
map -fstab                           0Bi    0Bi    0Bi   100%       0          0  100%   /Network/Servers
localhost:/iP1OctnxPGjSI5sSWt55eI  465Gi  465Gi    0Bi   100%       0          0  100%   /Volumes/MobileBackups
/dev/disk2s3                       466Gi  4.2Gi  461Gi     1%     293 4294966986    0%   /Volumes/macDisk
/dev/disk2s2                       1.4Ti  376Gi  1.0Ti    27% 2315049 4292652230    0%   /Volumes/macExt
/dev/disk3s1                        60Gi  8.8Mi   60Gi     1%      70     488122    0%   /Volumes/RPi
```

`/dev/disk3s1` 为 microSD 卡 RPi 对应的设备节点名称 。

运行 `diskutil list` 命令可查看详细的设备节点：

```Shell

/dev/disk3 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *64.0 GB    disk3
   1:               Windows_NTFS RPi                     64.0 GB    disk3s1
```

出厂为 ExFAT 格式(Windows_NTFS)。

## 格式化为 MS-DOS(FAT)
格式化后运行 `diskutil list` 命令查看详细的设备节点信息，可以看到文件系统已经格式化为 DOS_FAT_32：

```Shell
faner@THOMASFAN-MB0:~|⇒  diskutil list

/dev/disk3 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *64.0 GB    disk3
   1:                 DOS_FAT_32 RPi                     64.0 GB    disk3s1

faner@THOMASFAN-MB0:~|⇒  
```

## 卸载分区卷
运行 `diskutil unmount` 命令将分区卸载：

```Shell
faner@THOMASFAN-MB0:~|⇒  diskutil unmount /dev/disk3s1 
Volume RPi on disk3s1 unmounted
```

## 写入系统镜像
从 [raspberrypi](https://www.raspberrypi.org/products) 官网下载最新的 raspbian 镜像 `2017-09-07-raspbian-stretch.zip`；在 macOS 终端通过 `shasum -a 256` 命令校验下载文件的 SHA-256 是否一致。

```Shell
⇒  shasum -a 256 /Users/faner/Downloads/2017-09-07-raspbian-stretch.zip 
a64d742bc525b548f0435581fac5876b50a4e9ba1d1cd6433358b4ab6c7a770b  /Users/faner/Downloads/2017-09-07-raspbian-stretch.zip
```

1. 将当前目录切换到下载解压的 raspbian 系统镜像（`2017-09-07-raspbian-stretch.img`）所在目录；  
2. 执行 dd 命令 `sudo dd bs=1m if=2017-09-07-raspbian-stretch.img of=/dev/rdisk3 conv=sync` 将 img 写入 microSD 卡。  

```Shell
Last login: Sun Sep 17 12:17:55 on ttys000
faner@THOMASFAN-MB0:~|⇒  cd /Users/faner/Downloads 
faner@THOMASFAN-MB0:~/Downloads|⇒  sudo dd bs=1m if=2017-09-07-raspbian-stretch.img of=/dev/rdisk3 conv=sync
Password:

4688+1 records in
4689+0 records out
4916772864 bytes transferred in 377.643199 secs (13019625 bytes/sec)
faner@THOMASFAN-MB0:~/Downloads|⇒  
```

大约要静默等待几分钟，中途并无 verbose 日志输出。可以按下 control+T 发送 `SIGINFO` 信号，打印写入进度。  
最终写入完成，屏幕输出信息如上。  

## 确认写入结果
写入系统镜像成功后，再次运行 `diskutil list` 命令，可以查看到设备节点 disk3 下多出了一个 boot 分区（disk3s1）和一个 linux 系统分区（disk3s2）。

```Shell
faner@THOMASFAN-MB0:~|⇒  diskutil list

/dev/disk3 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *64.0 GB    disk3
   1:             Windows_FAT_32 boot                    43.8 MB    disk3s1
   2:                      Linux                         4.9 GB     disk3s2
```

## 启动 raspbian
将刻录好的 microSD 卡插入 Raspberry Pi 背面底板的 SD 卡插槽，上电启动。  
默认配置从 microSD 卡引导（启动），当检测到装有 raspbian 系统的可引导 microSD 卡时，将启动 raspbian 系统。  
在没有启动系统前，只有红色电源指示灯常亮；启动 raspbian 系统过程中，绿灯会常亮一段时间；系统启动完毕，绿灯偶尔会闪一下。  
接下来，通过 USB 连接键盘鼠标、HDMI 接上显示屏后，即可进入 raspbian 系统图形界面。  

## references
[树莓派启动：for Mac](http://blog.csdn.net/selina013/article/details/51029900)  
[树莓派Ｂ＋使用心得](http://www.cnblogs.com/uestc-mm/p/6290521.html)  

[Raspbian Stretch not 64bit?](https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=192321&sid=505b5ad936e7d4f9a69253b89ced4b3a)  
[Raspberry Pi 3 has 64-bit CPU, but 32-bit Raspbian OS (for now)](http://linuxgizmos.com/raspberry-pi-3-has-a-64-bit-cpu-but-a-32-bit-raspbian-os/)  
[树莓派升级arm64 debian stretch小记](http://www.jianshu.com/p/7b962b038a6c)  
