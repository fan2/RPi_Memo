
- **SoC**：`Raspberry Pi 4 Model B Rev 1.4`  

[linux 如何查看硬盘大小,内存大小等系统信息及硬件信息](https://blog.csdn.net/qq_15437629/article/details/51601521)

## uname

uname - print system information

```Shell
pi@raspberrypi:~ $ uname
Linux
pi@raspberrypi:~ $ uname -mrs
Linux 5.10.63-v8+ aarch64
pi@raspberrypi:~ $ uname -a
Linux raspberrypi 5.10.63-v8+ #1496 SMP PREEMPT Wed Dec 1 15:59:46 GMT 2021 aarch64 GNU/Linux
```

## cpuinfo

[Linux查看CPU配置信息、内存大小](https://blog.csdn.net/u011983531/article/details/80240879)

查看 cpu 信息：

```Shell
pi@raspberrypi:~ $ cat /proc/cpuinfo
processor	: 0
BogoMIPS	: 108.00
Features	: fp asimd evtstrm crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd08
CPU revision	: 3

processor	: 1
BogoMIPS	: 108.00
Features	: fp asimd evtstrm crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd08
CPU revision	: 3

processor	: 2
BogoMIPS	: 108.00
Features	: fp asimd evtstrm crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd08
CPU revision	: 3

processor	: 3
BogoMIPS	: 108.00
Features	: fp asimd evtstrm crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd08
CPU revision	: 3

Hardware	: BCM2835
Revision	: d03114
Serial		: 10000000a744c93f
Model		: Raspberry Pi 4 Model B Rev 1.4
```

### lscpu

**lscpu** - display information about the CPU architecture

lscpu  gathers  CPU  architecture information from sysfs, /proc/cpuinfo and any applicable architecture specific  libraries  (e.g.  librtas  on Powerpc).

```Shell
pi@raspberrypi:~ $ lscpu
Architecture:        aarch64
Byte Order:          Little Endian
CPU(s):              4
On-line CPU(s) list: 0-3
Thread(s) per core:  1
Core(s) per socket:  4
Socket(s):           1
Vendor ID:           ARM
Model:               3
Model name:          Cortex-A72
Stepping:            r0p3
CPU max MHz:         1500.0000
CPU min MHz:         600.0000
BogoMIPS:            108.00
Flags:               fp asimd evtstrm crc32 cpuid

pi@raspberrypi:~ $ cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq
600000

pi@raspberrypi:~ $ vcgencmd get_config arm_freq
arm_freq=1500
```

## diskinfo

查看磁盘信息，约合64G：

```Shell
pi@raspberrypi:~ $ df -lh
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        59G  2.6G   54G   5% /
devtmpfs        3.7G     0  3.7G   0% /dev
tmpfs           3.9G     0  3.9G   0% /dev/shm
tmpfs           3.9G  8.5M  3.9G   1% /run
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           3.9G     0  3.9G   0% /sys/fs/cgroup
/dev/mmcblk0p1  253M   31M  222M  13% /boot
tmpfs           782M     0  782M   0% /run/user/1000
```

## meminfo

[Linux 查看内存使用情况](https://www.cnblogs.com/qinxu/p/9649129.html)  

查看内存信息，约合8G：

```Shell
pi@raspberrypi:~ $ cat /proc/meminfo
MemTotal:        8000520 kB
MemFree:         7650708 kB
MemAvailable:    7799852 kB
Buffers:           35996 kB
Cached:           207084 kB
SwapCached:            0 kB
Active:           176504 kB
Inactive:          90380 kB
```

执行 `free -m` 查看剩余可用内存：

```Shell
pi@raspberrypi:~ $ free -m
              total        used        free      shared  buff/cache   available
Mem:           7813          74        7471           8         266        7617
Swap:            99           0          99
```

## OSTYPE & MACHTYPE

```Shell
pi@raspberrypi:~ $ echo $OSTYPE
linux-gnu
pi@raspberrypi:~ $ echo $HOSTTYPE
aarch64
pi@raspberrypi:~ $ echo $MACHTYPE
aarch64-unknown-linux-gnu
```

## arch & word

arch - print machine hardware name (same as uname -m)

```Shell
pi@raspberrypi:~ $ arch
aarch64
pi@raspberrypi:~ $ uname -m
aarch64
pi@raspberrypi:~ $ getconf WORD_BIT
32
pi@raspberrypi:~ $ getconf LONG_BIT
64
```

## debian_version

```Shell
pi@raspberrypi:~ $ cat /proc/version
Linux version 5.10.63-v8+ (dom@buildbot) (aarch64-linux-gnu-gcc-8 (Ubuntu/Linaro 8.4.0-3ubuntu1) 8.4.0, GNU ld (GNU Binutils for Ubuntu) 2.34) #1496 SMP PREEMPT Wed Dec 1 15:59:46 GMT 2021
pi@raspberrypi:~ $ cat /boot/issue.txt
Raspberry Pi reference 2020-08-20
Generated using pi-gen, https://github.com/RPi-Distro/pi-gen, 7252c154838ec5b4576f29c996ac8fe3750cae12, stage4
pi@raspberrypi:~ $ cat /etc/issue
Debian GNU/Linux 10 \n \l

pi@raspberrypi:~ $ cat /etc/debian_version
10.11
```

### lsb_release

lsb_release - print distribution-specific information

```Shell
pi@raspberrypi:~ $ lsb_release -a
No LSB modules are available.
Distributor ID:	Debian
Description:	Debian GNU/Linux 10 (buster)
Release:	10
Codename:	buster
```
