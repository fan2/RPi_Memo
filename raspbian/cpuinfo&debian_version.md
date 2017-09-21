[Raspberry Pi 3 Hardware and System Software Reference](http://www.codeguru.com/IoT/raspberry-pi-3-hardware-and-system-software-reference.html)

## [cpuinfo](https://www.zybuluo.com/SiberiaBear/note/336984)

```Shell
pi@raspberrypi:/ $ cat /proc/cpuinfo
processor	: 0
model name	: ARMv7 Processor rev 4 (v7l)
BogoMIPS	: 38.40
Features	: half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32 
CPU implementer	: 0x41
CPU architecture: 7
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

processor	: 1
model name	: ARMv7 Processor rev 4 (v7l)
BogoMIPS	: 38.40
Features	: half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32 
CPU implementer	: 0x41
CPU architecture: 7
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

processor	: 2
model name	: ARMv7 Processor rev 4 (v7l)
BogoMIPS	: 38.40
Features	: half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32 
CPU implementer	: 0x41
CPU architecture: 7
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

processor	: 3
model name	: ARMv7 Processor rev 4 (v7l)
BogoMIPS	: 38.40
Features	: half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32 
CPU implementer	: 0x41
CPU architecture: 7
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 4

Hardware	: BCM2835
Revision	: a02082
Serial		: 000000007615217c
pi@raspberrypi:/ $ 
```

### lscpu

```Shell
pi@raspberrypi:~ $ lscpu 
Architecture:          armv7l
Byte Order:            Little Endian
CPU(s):                4
On-line CPU(s) list:   0-3
Thread(s) per core:    1
Core(s) per socket:    4
Socket(s):             1
Model:                 4
Model name:            ARMv7 Processor rev 4 (v7l)
CPU max MHz:           1200.0000
CPU min MHz:           600.0000
BogoMIPS:              38.40
Flags:                 half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32

pi@raspberrypi:~ $ arch
armv7l

pi@raspberrypi:~ $ cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq 
600000

pi@raspberrypi:~ $ vcgencmd get_config arm_freq
arm_freq=1200
```

## debian_version

```Shell
pi@raspberrypi:~ $ uname -a
Linux raspberrypi 4.9.41-v7+ #1023 SMP Tue Aug 8 16:00:15 BST 2017 armv7l GNU/Linux

pi@raspberrypi:~ $ cat /proc/version 
Linux version 4.9.41-v7+ (dc4@dc4-XPS13-9333) (gcc version 4.9.3 (crosstool-NG crosstool-ng-1.22.0-88-g8460611) ) #1023 SMP Tue Aug 8 16:00:15 BST 2017

pi@raspberrypi:~ $ cat /etc/issue
Raspbian GNU/Linux 9 \n \l

pi@raspberrypi:~ $ cat /etc/debian_version 
9.1

pi@raspberrypi:~ $ lsb_release -a
No LSB modules are available.
Distributor ID:	Raspbian
Description:	Raspbian GNU/Linux 9.1 (stretch)
Release:	9.1
Codename:	stretch
```

## misc.etc
`cat /proc/meminfo`  
`cat /proc/diskstats`  
`cat /proc/filesystems`  
**`man hier`** - description of the filesystem hierarchy  
