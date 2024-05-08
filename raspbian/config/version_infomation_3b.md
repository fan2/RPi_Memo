
- **SoC**：`Raspberry Pi 3 Model B v1.2`(2015)  
- **OS**：`2017-09-07-raspbian-stretch.zip`

## uname

uname - print system information

```Shell
pifan@rpi3b-ubuntu $ uname -a
Linux rpi3b-ubuntu 5.15.0-1049-raspi #52-Ubuntu SMP PREEMPT Thu Mar 14 08:39:42 UTC 2024 aarch64 aarch64 aarch64 GNU/Linux
```

## cpuinfo

[Linux查看CPU配置信息、内存大小](https://blog.csdn.net/u011983531/article/details/80240879)

查看 cpu 信息：

```Shell
pifan@rpi3b-ubuntu $ cat /proc/cpuinfo
processor	: 0
BogoMIPS	: 38.40
Features	: fp asimd evtstrm crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

processor	: 1
BogoMIPS	: 38.40
Features	: fp asimd evtstrm crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

processor	: 2
BogoMIPS	: 38.40
Features	: fp asimd evtstrm crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

processor	: 3
BogoMIPS	: 38.40
Features	: fp asimd evtstrm crc32 cpuid
CPU implementer	: 0x41
CPU architecture: 8
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

Hardware	: BCM2835
Revision	: a02082
Serial		: 000000007615217c
Model		: Raspberry Pi 3 Model B Rev 1.2
```

### lscpu

**lscpu** - display information about the CPU architecture

lscpu  gathers  CPU  architecture information from sysfs, /proc/cpuinfo and any applicable architecture specific  libraries  (e.g.  librtas  on Powerpc).

```Shell
pifan@rpi3b-ubuntu $ lscpu
Architecture:            aarch64
  CPU op-mode(s):        32-bit, 64-bit
  Byte Order:            Little Endian
CPU(s):                  4
  On-line CPU(s) list:   0-3
Vendor ID:               ARM
  Model name:            Cortex-A53
    Model:               4
    Thread(s) per core:  1
    Core(s) per cluster: 4
    Socket(s):           -
    Cluster(s):          1
    Stepping:            r0p4
    CPU max MHz:         1200.0000
    CPU min MHz:         600.0000
    BogoMIPS:            38.40
    Flags:               fp asimd evtstrm crc32 cpuid
Caches (sum of all):
  L1d:                   128 KiB (4 instances)
  L1i:                   128 KiB (4 instances)
  L2:                    512 KiB (1 instance)

pifan@rpi3b-ubuntu $ cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq
1200000
```

## diskinfo

查看磁盘信息，约合64G：

```Shell
pifan@rpi3b-ubuntu $ df -lh
Filesystem      Size  Used Avail Use% Mounted on
tmpfs            91M  3.5M   88M   4% /run
/dev/mmcblk0p2   59G  8.6G   48G  16% /
tmpfs           453M     0  453M   0% /dev/shm
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
/dev/mmcblk0p1  253M  119M  134M  47% /boot/firmware
tmpfs            91M   76K   91M   1% /run/user/128
tmpfs            91M   68K   91M   1% /run/user/1000
```

## meminfo

[Linux 查看内存使用情况](https://www.cnblogs.com/qinxu/p/9649129.html)  

查看内存信息，约合8G：

```Shell
pifan@rpi3b-ubuntu $ cat /proc/meminfo | head -n 16
MemTotal:         927028 kB
MemFree:          189568 kB
MemAvailable:     384856 kB
Buffers:           10808 kB
Cached:           229512 kB
SwapCached:          784 kB
Active:           141508 kB
Inactive:         362996 kB
Active(anon):      28848 kB
Inactive(anon):   238264 kB
Active(file):     112660 kB
Inactive(file):   124732 kB
Unevictable:           0 kB
Mlocked:               0 kB
SwapTotal:       1048572 kB
SwapFree:         962556 kB
```

执行 `free -m` 查看剩余可用内存：

```Shell
pifan@rpi3b-ubuntu $ free -m
               total        used        free      shared  buff/cache   available
Mem:             905         453         178           2         273         369
Swap:           1023          84         939
```

## OSTYPE & MACHTYPE

```Shell
pifan@rpi3b-ubuntu $ echo $OSTYPE
linux-gnu
pifan@rpi3b-ubuntu $ echo $HOSTTYPE

pifan@rpi3b-ubuntu $ echo $MACHTYPE
aarch64
```

## arch & word

arch - print machine hardware name (same as uname -m)

```Shell
pifan@rpi3b-ubuntu $ arch
aarch64
pifan@rpi3b-ubuntu $ uname -m
aarch64
pifan@rpi3b-ubuntu $ getconf WORD_BIT
32
pifan@rpi3b-ubuntu $ getconf LONG_BIT
64
```

## debian_version

```Shell
pifan@rpi3b-ubuntu $ cat /proc/version
Linux version 5.15.0-1049-raspi (buildd@bos01-arm64-020) (gcc (Ubuntu 11.4.0-1ubuntu1~22.04) 11.4.0, GNU ld (GNU Binutils for Ubuntu) 2.38) #52-Ubuntu SMP PREEMPT Thu Mar 14 08:39:42 UTC 2024
pifan@rpi3b-ubuntu $ cat /etc/issue
Ubuntu 22.04.4 LTS \n \l
pifan@rpi3b-ubuntu $ cat /etc/debian_version
bookworm/sid
```

### lsb_release

lsb_release - print distribution-specific information

```Shell
pifan@rpi3b-ubuntu $ lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 22.04.4 LTS
Release:	22.04
Codename:	jammy
```
