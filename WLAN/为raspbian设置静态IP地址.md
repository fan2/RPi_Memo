# SoC & OS

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

# 设置静态 IP

旧的 raspbian 系统配置静态IP都是修改配置文件 [`/etc/network/interfaces`](http://blog.csdn.net/github_35160620/article/details/52107766)，最新的 raspbian stretch 系统配置静态 IP 需要修改的是 `/etc/dhcpcd.conf` 文件，如下 [`/etc/network/interfaces`](http://blog.csdn.net/shaopengf/article/details/52412429) 所示。

```Shell
pi@raspberrypi:~$ cat /etc/network/interfaces
# interfaces(5) file used by ifup(8) and ifdown(8)

# Please note that this file is written to be used with dhcpcd
# For static IP, consult /etc/dhcpcd.conf and 'man dhcpcd.conf'

# Include files from /etc/network/interfaces.d:
source-directory /etc/network/interfaces.d
```

执行 `cat /etc/dhcpcd.conf` 查看配置文件 `/etc/dhcpcd.conf` 内容：

```Shell
pi@raspberrypi:~$ cat /etc/dhcpcd.conf

# Example static IP configuration:
#interface eth0
#static ip_address=192.168.0.10/24
#static ip6_address=fd51:42f8:caae:d92e::ff/64
#static routers=192.168.0.1
#static domain_name_servers=192.168.0.1 8.8.8.8 fd51:42f8:caae:d92e::1

# It is possible to fall back to a static IP if DHCP fails:
# define static profile
#profile static_eth0
#static ip_address=192.168.1.23/24
#static routers=192.168.1.1
#static domain_name_servers=192.168.1.1

# fallback to static profile on eth0
#interface eth0
#fallback static_eth0

```

参考 Example static IP configuration，将有线网卡 eth0 和无线网卡 wlan0  都设置为静态IP：

```Shell

# add by thomasfan, 02Oct17
interface eth0
static routers=192.168.1.1
#inform 192.168.1.128/24
static ip_address=192.168.1.128/24
static domain_search=192.168.1.1
static domain_name_servers=192.168.1.1 8.8.8.8 114.114.114.114

# add by thomasfan, 02Oct17
interface wlan0
static routers=192.168.1.1
#inform 192.168.1.128/24
static ip_address=192.168.1.128/24
static domain_search=192.168.1.1
static domain_name_servers=192.168.1.1 8.8.8.8 114.114.114.114

```

先 down 再 up 无线网卡 wlan0，如果指定IP尚在路由器DHCP地址池且仍未被占用，将可配得该静态 IP。

```Shell
sudo ifconfig wlan0 down # 禁用无线网卡wlan0
sudo ifconfig wlan0 up # 启用无线网卡wlan0
```

正常情况下，执行 `ifconfig` 将可以看到无线网卡 wlan0 分配得到 IP：192.168.1.128。

```Shell
pi@raspberrypi:~$ ifconfig

wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500

...
inet 192.168.1.128  netmask 255.255.255.0  broadcast 192.168.1.255
...
```

# 参考

- [Raspberry Pi 3安装配置Raspbian过程 - 8. 设置静态IP](http://blog.csdn.net/yss28/article/details/51874104)  
- [Raspberry PI 3静态IP配置](http://blog.csdn.net/u011973222/article/details/72843127)  
