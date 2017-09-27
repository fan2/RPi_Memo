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

pi@raspberrypi:~ $ cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq 
600000

pi@raspberrypi:~ $ vcgencmd get_config arm_freq
arm_freq=1200
```

## arch
```Shell
pi@raspberrypi:~ $ arch
armv7l

pi@raspberrypi:~ $ getconf WORD_BIT
32

pi@raspberrypi:~ $ getconf LONG_BIT
32
```

## debian_version
```Shell
pi@raspberrypi:~ $ cat /proc/version 
Linux version 4.9.41-v7+ (dc4@dc4-XPS13-9333) (gcc version 4.9.3 (crosstool-NG crosstool-ng-1.22.0-88-g8460611) ) #1023 SMP Tue Aug 8 16:00:15 BST 2017

pi@raspberrypi:~$ more /boot/issue.txt
Raspberry Pi reference 2017-09-07
Generated using pi-gen, https://github.com/RPi-Distro/pi-gen, 496e41575eeb9fa13f
394ffb407b7bc1d00b21c2, stage5

pi@raspberrypi:~ $ uname -a
Linux raspberrypi 4.9.41-v7+ #1023 SMP Tue Aug 8 16:00:15 BST 2017 armv7l GNU/Linux

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

## dmesg
```Shell
pi@raspberrypi:~/Projects/WORDSIZE $ dmesg more
[    0.000000] Booting Linux on physical CPU 0x0
[    0.000000] Linux version 4.9.41-v7+ (dc4@dc4-XPS13-9333) (gcc version 4.9.3 (crosstool-NG crosstool-ng-1.22.0-88-g8460611) ) #1023 SMP Tue Aug 8 16:00:15 BST 2017
[    0.000000] CPU: ARMv7 Processor [410fd034] revision 4 (ARMv7), cr=10c5383d
[    0.000000] CPU: div instructions available: patching division code
[    0.000000] CPU: PIPT / VIPT nonaliasing data cache, VIPT aliasing instruction cache
[    0.000000] OF: fdt:Machine model: Raspberry Pi 3 Model B Rev 1.2
[    0.000000] cma: Reserved 8 MiB at 0x37800000
[    0.000000] Memory policy: Data cache writealloc
[    0.000000] On node 0 totalpages: 229376
[    0.000000] free_area_init_node: node 0, pgdat 80c6eec0, node_mem_map b7016000
[    0.000000]   Normal zone: 2016 pages used for memmap
[    0.000000]   Normal zone: 0 pages reserved
[    0.000000]   Normal zone: 229376 pages, LIFO batch:31
[    0.000000] percpu: Embedded 14 pages/cpu @b6fd0000 s25600 r8192 d23552 u57344
[    0.000000] pcpu-alloc: s25600 r8192 d23552 u57344 alloc=14*4096
[    0.000000] pcpu-alloc: [0] 0 [0] 1 [0] 2 [0] 3 
[    0.000000] Built 1 zonelists in Zone order, mobility grouping on.  Total pages: 227360
[    0.000000] Kernel command line: 8250.nr_uarts=1 bcm2708_fb.fbwidth=1280 bcm2708_fb.fbheight=720 bcm2708_fb.fbswap=1 vc_mem.mem_base=0x3ec00000 vc_mem.mem_size=0x40000000  dwc_otg.lpm_enable=0 console=ttyS0,115200 console=tty1 root=PARTUUID=38b25fe3-02 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait quiet splash plymouth.ignore-serial-consoles
[    0.000000] PID hash table entries: 4096 (order: 2, 16384 bytes)
[    0.000000] Dentry cache hash table entries: 131072 (order: 7, 524288 bytes)
[    0.000000] Inode-cache hash table entries: 65536 (order: 6, 262144 bytes)
[    0.000000] Memory: 887576K/917504K available (7168K kernel code, 484K rwdata, 2012K rodata, 1024K init, 778K bss, 21736K reserved, 8192K cma-reserved)
[    0.000000] Virtual kernel memory layout:
                   vector  : 0xffff0000 - 0xffff1000   (   4 kB)
                   fixmap  : 0xffc00000 - 0xfff00000   (3072 kB)
                   vmalloc : 0xb8800000 - 0xff800000   (1136 MB)
                   lowmem  : 0x80000000 - 0xb8000000   ( 896 MB)
                   modules : 0x7f000000 - 0x80000000   (  16 MB)
                     .text : 0x80008000 - 0x80800000   (8160 kB)
                     .init : 0x80b00000 - 0x80c00000   (1024 kB)
                     .data : 0x80c00000 - 0x80c79094   ( 485 kB)
                      .bss : 0x80c7b000 - 0x80d3da64   ( 779 kB)
[    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=4, Nodes=1
[    0.000000] Hierarchical RCU implementation.
[    0.000000] 	Build-time adjustment of leaf fanout to 32.
[    0.000000] NR_IRQS:16 nr_irqs:16 16
[    0.000000] arm_arch_timer: Architected cp15 timer(s) running at 19.20MHz (phys).
[    0.000000] clocksource: arch_sys_counter: mask: 0xffffffffffffff max_cycles: 0x46d987e47, max_idle_ns: 440795202767 ns
[    0.000007] sched_clock: 56 bits at 19MHz, resolution 52ns, wraps every 4398046511078ns
[    0.000019] Switching to timer-based delay loop, resolution 52ns
[    0.000290] Console: colour dummy device 80x30
[    0.000306] console [tty1] enabled
[    0.000330] Calibrating delay loop (skipped), value calculated using timer frequency.. 38.40 BogoMIPS (lpj=192000)
[    0.000345] pid_max: default: 32768 minimum: 301
[    0.000650] Mount-cache hash table entries: 2048 (order: 1, 8192 bytes)
[    0.000659] Mountpoint-cache hash table entries: 2048 (order: 1, 8192 bytes)
[    0.001514] Disabling cpuset control group subsystem
[    0.001640] CPU: Testing write buffer coherency: ok
[    0.001674] ftrace: allocating 22396 entries in 66 pages
[    0.048110] CPU0: update cpu_capacity 1024
[    0.048126] CPU0: thread -1, cpu 0, socket 0, mpidr 80000000
[    0.048162] Setting up static identity map for 0x100000 - 0x100034
[    0.050006] CPU1: update cpu_capacity 1024
[    0.050013] CPU1: thread -1, cpu 1, socket 0, mpidr 80000001
[    0.050698] CPU2: update cpu_capacity 1024
[    0.050704] CPU2: thread -1, cpu 2, socket 0, mpidr 80000002
[    0.051369] CPU3: update cpu_capacity 1024
[    0.051376] CPU3: thread -1, cpu 3, socket 0, mpidr 80000003
[    0.051463] Brought up 4 CPUs
[    0.051473] SMP: Total of 4 processors activated (153.60 BogoMIPS).
[    0.051477] CPU: All CPU(s) started in HYP mode.
[    0.051481] CPU: Virtualization extensions available.
[    0.052266] devtmpfs: initialized
[    0.063539] VFP support v0.3: implementor 41 architecture 3 part 40 variant 3 rev 4
[    0.063813] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns
[    0.063830] futex hash table entries: 1024 (order: 4, 65536 bytes)
[    0.064361] pinctrl core: initialized pinctrl subsystem
[    0.065250] NET: Registered protocol family 16
[    0.067579] DMA: preallocated 1024 KiB pool for atomic coherent allocations
[    0.076511] hw-breakpoint: found 5 (+1 reserved) breakpoint and 4 watchpoint registers.
[    0.076517] hw-breakpoint: maximum watchpoint size is 8 bytes.
[    0.076663] Serial: AMBA PL011 UART driver
[    0.078536] bcm2835-mbox 3f00b880.mailbox: mailbox enabled
[    0.079054] uart-pl011 3f201000.serial: could not find pctldev for node /soc/gpio@7e200000/uart0_pins, deferring probe
[    0.079369] irq: no irq domain found for /soc/aux@0x7e215000 !
[    0.148943] bcm2835-dma 3f007000.dma: DMA legacy API manager at b880f000, dmachans=0x1
[    0.150758] SCSI subsystem initialized
[    0.150909] usbcore: registered new interface driver usbfs
[    0.150983] usbcore: registered new interface driver hub
[    0.151073] usbcore: registered new device driver usb
[    0.157919] raspberrypi-firmware soc:firmware: Attached to firmware from 2017-08-08 12:01
[    0.159403] clocksource: Switched to clocksource arch_sys_counter
[    0.206547] VFS: Disk quotas dquot_6.6.0
[    0.206623] VFS: Dquot-cache hash table entries: 1024 (order 0, 4096 bytes)
[    0.206820] FS-Cache: Loaded
[    0.207058] CacheFiles: Loaded
[    0.219154] NET: Registered protocol family 2
[    0.220057] TCP established hash table entries: 8192 (order: 3, 32768 bytes)
[    0.220166] TCP bind hash table entries: 8192 (order: 4, 65536 bytes)
[    0.220350] TCP: Hash tables configured (established 8192 bind 8192)
[    0.220438] UDP hash table entries: 512 (order: 2, 16384 bytes)
[    0.220480] UDP-Lite hash table entries: 512 (order: 2, 16384 bytes)
[    0.220686] NET: Registered protocol family 1
[    0.221099] RPC: Registered named UNIX socket transport module.
[    0.221104] RPC: Registered udp transport module.
[    0.221109] RPC: Registered tcp transport module.
[    0.221113] RPC: Registered tcp NFSv4.1 backchannel transport module.
[    0.222163] hw perfevents: enabled with armv7_cortex_a7 PMU driver, 7 counters available
[    0.224422] workingset: timestamp_bits=14 max_order=18 bucket_order=4
[    0.240456] FS-Cache: Netfs 'nfs' registered for caching
[    0.241419] NFS: Registering the id_resolver key type
[    0.241443] Key type id_resolver registered
[    0.241448] Key type id_legacy registered
[    0.243869] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 251)
[    0.243971] io scheduler noop registered
[    0.243977] io scheduler deadline registered (default)
[    0.244262] io scheduler cfq registered
[    0.249873] BCM2708FB: allocated DMA memory f7910000
[    0.249896] BCM2708FB: allocated DMA channel 0 @ b880f000
[    0.276151] Console: switching to colour frame buffer device 160x45
[    0.291421] Serial: 8250/16550 driver, 1 ports, IRQ sharing enabled
[    0.292026] bcm2835-aux-uart 3f215040.serial: could not get clk: -517
[    0.293228] bcm2835-rng 3f104000.rng: hwrng registered
[    0.293337] vc-cma: Videocore CMA driver
[    0.293343] vc-cma: vc_cma_base      = 0x00000000
[    0.293349] vc-cma: vc_cma_size      = 0x00000000 (0 MiB)
[    0.293354] vc-cma: vc_cma_initial   = 0x00000000 (0 MiB)
[    0.293545] vc-mem: phys_addr:0x00000000 mem_base=0x3ec00000 mem_size:0x40000000(1024 MiB)
[    0.308877] brd: module loaded
[    0.317660] loop: module loaded
[    0.317672] Loading iSCSI transport class v2.0-870.
[    0.318211] usbcore: registered new interface driver smsc95xx
[    0.318227] dwc_otg: version 3.00a 10-AUG-2012 (platform bus)
[    0.546322] Core Release: 2.80a
[    0.546330] Setting default values for core params
[    0.546361] Finished setting default values for core params
[    0.746749] Using Buffer DMA mode
[    0.746754] Periodic Transfer Interrupt Enhancement - disabled
[    0.746759] Multiprocessor Interrupt Enhancement - disabled
[    0.746764] OTG VER PARAM: 0, OTG VER FLAG: 0
[    0.746777] Dedicated Tx FIFOs mode
[    0.747117] WARN::dwc_otg_hcd_init:1032: FIQ DMA bounce buffers: virt = 0xb7904000 dma = 0xf7904000 len=9024
[    0.747142] FIQ FSM acceleration enabled for :
               Non-periodic Split Transactions
               Periodic Split Transactions
               High-Speed Isochronous Endpoints
               Interrupt/Control Split Transaction hack enabled
[    0.747148] dwc_otg: Microframe scheduler enabled
[    0.747196] WARN::hcd_init_fiq:459: FIQ on core 1 at 0x8058f7fc
[    0.747205] WARN::hcd_init_fiq:460: FIQ ASM at 0x8058fb6c length 36
[    0.747215] WARN::hcd_init_fiq:486: MPHI regs_base at 0xb887a000
[    0.747274] dwc_otg 3f980000.usb: DWC OTG Controller
[    0.747309] dwc_otg 3f980000.usb: new USB bus registered, assigned bus number 1
[    0.747340] dwc_otg 3f980000.usb: irq 62, io mem 0x00000000
[    0.747386] Init: Port Power? op_state=1
[    0.747390] Init: Power Port (0)
[    0.747592] usb usb1: New USB device found, idVendor=1d6b, idProduct=0002
[    0.747603] usb usb1: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    0.747610] usb usb1: Product: DWC OTG Controller
[    0.747618] usb usb1: Manufacturer: Linux 4.9.41-v7+ dwc_otg_hcd
[    0.747625] usb usb1: SerialNumber: 3f980000.usb
[    0.748470] hub 1-0:1.0: USB hub found
[    0.748507] hub 1-0:1.0: 1 port detected
[    0.749219] dwc_otg: FIQ enabled
[    0.749225] dwc_otg: NAK holdoff enabled
[    0.749229] dwc_otg: FIQ split-transaction FSM enabled
[    0.749242] Module dwc_common_port init
[    0.749485] usbcore: registered new interface driver usb-storage
[    0.749700] mousedev: PS/2 mouse device common for all mice
[    0.750639] bcm2835-wdt 3f100000.watchdog: Broadcom BCM2835 watchdog timer
[    0.750917] bcm2835-cpufreq: min=600000 max=1200000
[    0.751308] sdhci: Secure Digital Host Controller Interface driver
[    0.751312] sdhci: Copyright(c) Pierre Ossman
[    0.751584] sdhost-bcm2835 3f202000.sdhost: could not get clk, deferring probe
[    0.753759] mmc-bcm2835 3f300000.mmc: could not get clk, deferring probe
[    0.753858] sdhci-pltfm: SDHCI platform and OF driver helper
[    0.756476] ledtrig-cpu: registered to indicate activity on CPUs
[    0.756663] hidraw: raw HID events driver (C) Jiri Kosina
[    0.756858] usbcore: registered new interface driver usbhid
[    0.756862] usbhid: USB HID core driver
[    0.757651] vchiq: vchiq_init_state: slot_zero = 0xb7980000, is_master = 0
[    0.759706] Initializing XFRM netlink socket
[    0.759728] NET: Registered protocol family 17
[    0.759837] Key type dns_resolver registered
[    0.760342] Registering SWP/SWPB emulation handler
[    0.761084] registered taskstats version 1
[    0.761423] vc-sm: Videocore shared memory driver
[    0.761432] [vc_sm_connected_init]: start
[    0.768242] [vc_sm_connected_init]: end - returning 0
[    0.774287] 3f201000.serial: ttyAMA0 at MMIO 0x3f201000 (irq = 87, base_baud = 0) is a PL011 rev2
[    0.775819] console [ttyS0] disabled
[    0.775845] 3f215040.serial: ttyS0 at MMIO 0x0 (irq = 220, base_baud = 31250000) is a 16550
[    0.782451] console [ttyS0] enabled
[    0.783120] sdhost: log_buf @ b7907000 (f7907000)
[    0.859431] mmc0: sdhost-bcm2835 loaded - DMA enabled (>1)
[    0.861642] mmc-bcm2835 3f300000.mmc: mmc_debug:0 mmc_debug2:0
[    0.861651] mmc-bcm2835 3f300000.mmc: DMA channel allocated
[    0.926268] mmc0: host does not support reading read-only switch, assuming write-enable
[    0.928120] mmc0: new high speed SDXC card at address 0001
[    0.928736] mmcblk0: mmc0:0001 EC2QT 59.6 GiB
[    0.930289]  mmcblk0: p1 p2
[    0.939573] of_cfs_init
[    0.939649] of_cfs_init: OK
[    0.955824] mmc1: queuing unknown CIS tuple 0x80 (2 bytes)
[    0.957374] mmc1: queuing unknown CIS tuple 0x80 (3 bytes)
[    0.958738] EXT4-fs (mmcblk0p2): mounted filesystem with ordered data mode. Opts: (null)
[    0.958786] VFS: Mounted root (ext4 filesystem) readonly on device 179:2.
[    0.958928] mmc1: queuing unknown CIS tuple 0x80 (3 bytes)
[    0.959539] Indeed it is in host mode hprt0 = 00021501
[    0.959671] devtmpfs: mounted
[    1.021494] Freeing unused kernel memory: 1024K (80b00000 - 80c00000)
[    1.021853] mmc1: queuing unknown CIS tuple 0x80 (7 bytes)
[    1.033197] random: fast init done
[    1.112975] mmc1: new high speed SDIO card at address 0001
[    1.159460] usb 1-1: new high-speed USB device number 2 using dwc_otg
[    1.159609] Indeed it is in host mode hprt0 = 00001101
[    1.389739] usb 1-1: New USB device found, idVendor=0424, idProduct=9514
[    1.389753] usb 1-1: New USB device strings: Mfr=0, Product=0, SerialNumber=0
[    1.390603] hub 1-1:1.0: USB hub found
[    1.390692] hub 1-1:1.0: 5 ports detected
[    1.448251] systemd[1]: System time before build time, advancing clock.
[    1.571835] NET: Registered protocol family 10
[    1.582782] ip_tables: (C) 2000-2006 Netfilter Core Team
[    1.622525] systemd[1]: systemd 232 running in system mode. (+PAM +AUDIT +SELINUX +IMA +APPARMOR +SMACK +SYSVINIT +UTMP +LIBCRYPTSETUP +GCRYPT +GNUTLS +ACL +XZ +LZ4 +SECCOMP +BLKID +ELFUTILS +KMOD +IDN)
[    1.623108] systemd[1]: Detected architecture arm.
[    1.624136] systemd[1]: Set hostname to <raspberrypi>.
[    1.709548] usb 1-1.1: new high-speed USB device number 3 using dwc_otg
[    1.849768] usb 1-1.1: New USB device found, idVendor=0424, idProduct=ec00
[    1.849782] usb 1-1.1: New USB device strings: Mfr=0, Product=0, SerialNumber=0
[    1.852595] smsc95xx v1.0.5
[    1.953247] smsc95xx 1-1.1:1.0 eth0: register 'smsc95xx' at usb-3f980000.usb-1.1, smsc95xx USB 2.0 Ethernet, b8:27:eb:15:21:7c
[    2.107160] systemd[1]: Created slice System Slice.
[    2.110470] systemd[1]: Mounting POSIX Message Queue File System...
[    2.111016] systemd[1]: Listening on udev Control Socket.
[    2.112171] systemd[1]: Created slice system-systemd\x2dfsck.slice.
[    2.112879] systemd[1]: Created slice system-serial\x2dgetty.slice.
[    2.113192] systemd[1]: Listening on fsck to fsckd communication Socket.
[    2.117090] systemd[1]: Mounting Debug File System...
[    2.264275] i2c /dev entries driver
[    2.753719] EXT4-fs (mmcblk0p2): re-mounted. Opts: (null)
[    2.842976] systemd-journald[123]: Received request to flush runtime journal from PID 1
[    3.132891] gpiomem-bcm2835 3f200000.gpiomem: Initialised: Registers at 0x3f200000
[    3.445554] usbcore: registered new interface driver brcmfmac
[    3.557288] brcmfmac: Firmware version = wl0: Aug  7 2017 00:46:29 version 7.45.41.46 (r666254 CY) FWID 01-f8a78378
[    4.955598] Bluetooth: Core ver 2.22
[    4.955747] NET: Registered protocol family 31
[    4.955757] Bluetooth: HCI device and connection manager initialized
[    4.957767] Bluetooth: HCI socket layer initialized
[    4.957792] Bluetooth: L2CAP socket layer initialized
[    4.957846] Bluetooth: SCO socket layer initialized
[    5.344176] IPv6: ADDRCONF(NETDEV_UP): wlan0: link is not ready
[    5.344206] brcmfmac: power management disabled
[    5.821728] smsc95xx 1-1.1:1.0 eth0: hardware isn't capable of remote wakeup
[    5.822165] IPv6: ADDRCONF(NETDEV_UP): eth0: link is not ready
[    6.185315] Adding 102396k swap on /var/swap.  Priority:-1 extents:1 across:102396k SSFS
[    6.324490] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready
[   11.372578] fuse init (API version 7.26)
[   56.479099] random: crng init done
pi@raspberrypi:~/Projects/WORDSIZE $ 

```

## gcc
```Shell
pi@raspberrypi:~ $ gcc -v
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/usr/lib/gcc/arm-linux-gnueabihf/6/lto-wrapper
Target: arm-linux-gnueabihf
Configured with: ../src/configure -v --with-pkgversion='Raspbian 6.3.0-18+rpi1' --with-bugurl=file:///usr/share/doc/gcc-6/README.Bugs --enable-languages=c,ada,c++,java,go,d,fortran,objc,obj-c++ --prefix=/usr --program-suffix=-6 --program-prefix=arm-linux-gnueabihf- --enable-shared --enable-linker-build-id --libexecdir=/usr/lib --without-included-gettext --enable-threads=posix --libdir=/usr/lib --enable-nls --with-sysroot=/ --enable-clocale=gnu --enable-libstdcxx-debug --enable-libstdcxx-time=yes --with-default-libstdcxx-abi=new --enable-gnu-unique-object --disable-libitm --disable-libquadmath --enable-plugin --with-system-zlib --disable-browser-plugin --enable-java-awt=gtk --enable-gtk-cairo --with-java-home=/usr/lib/jvm/java-1.5.0-gcj-6-armhf/jre --enable-java-home --with-jvm-root-dir=/usr/lib/jvm/java-1.5.0-gcj-6-armhf --with-jvm-jar-dir=/usr/lib/jvm-exports/java-1.5.0-gcj-6-armhf --with-arch-directory=arm --with-ecj-jar=/usr/share/java/eclipse-ecj.jar --with-target-system-zlib --enable-objc-gc=auto --enable-multiarch --disable-sjlj-exceptions --with-arch=armv6 --with-fpu=vfp --with-float=hard --enable-checking=release --build=arm-linux-gnueabihf --host=arm-linux-gnueabihf --target=arm-linux-gnueabihf
Thread model: posix
gcc version 6.3.0 20170516 (Raspbian 6.3.0-18+rpi1) 
```

### data types
```Shell
pi@raspberrypi: $ cpp -dD /dev/null | grep __SIZEOF_LONG__
#define __SIZEOF_LONG__ 4
```

可执行 `gcc -dM -E -x c /dev/null` 或 `cpp -dD /dev/null` 查看工具链支持的原始类型信息。

> [how to get word address of label in gcc avr gas?](http://www.avrfreaks.net/forum/how-get-word-address-label-gcc-avr-gas)    
> [find out the sizes of data types on a system, without writing a C program?](https://unix.stackexchange.com/questions/115222/possible-to-find-out-the-sizes-of-data-types-int-float-double-on-a-syst)  

## misc.etc
`cat /proc/meminfo`  
`cat /proc/diskstats`  
`cat /proc/filesystems`  
**`man hier`** - description of the filesystem hierarchy  
