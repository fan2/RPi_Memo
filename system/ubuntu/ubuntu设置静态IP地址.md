## docs

[Ubuntu Server Network Configuration](https://ubuntu.com/server/docs/network-configuration)

To quickly identify all available Ethernet interfaces, you can use the `ip` command as shown below.

[Netplan configuration examples](https://netplan.io/examples/)

[Network Manager | Ubuntu](https://ubuntu.com/core/docs/networkmanager)

**NetworkManager** is a system network service that manages your network devices and connections and attempts to keep network connectivity active when available. It manages Ethernet, WiFi, mobile broadband (WWAN) and PPPoE devices while also providing VPN integration with a variety of different VPN services.

By default network management on Ubuntu Core is handled by systemd’s [networkd](https://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html) and [netplan](https://launchpad.net/netplan). However, when NetworkManager is installed, it will take control of all networking devices in the system by creating a netplan configuration file in which it sets itself as the default network renderer.

What NetworkManager Offers? Currently we provide support for the following high level features:

- WiFi connectivity
- WAN connectivity (together with ModemManager)
- Ethernet connectivity
- WiFi access point creation
- Shared connections
- VPN connections

### netplan1

[Ubuntu Static IP configuration](https://linuxconfig.org/how-to-configure-static-ip-address-on-ubuntu-18-10-cosmic-cuttlefish-linux)

set static IP address on Ubuntu Server via `netplan` and Ubuntu Desktop using `NetworkManager`.

- Set static IP address on Ubuntu Desktop using a `NetworkManager`  
- Configure static IP address on Ubuntu server via `networkd` daemon  

The simplest approach on how to configure a static IP address on Ubuntu *Desktop* is via **GNOME** graphical user interface.

---

To configure a static IP address on your Ubuntu *server* you need to modify a relevant **netplan** network configuration file within `/etc/netplan/` directory.

1. /etc/netplan/50-cloud-init.yaml  
2. /etc/netplan/01-netcfg.yaml  

Once ready apply changes with:

```Shell
$ sudo netplan apply
```

In case you run into some issues execute:

```Shell
$ sudo netplan --debug apply
```

### netplan2

[How to Configure Static IP Address on Ubuntu 20.04](https://linuxize.com/post/how-to-configure-static-ip-address-on-ubuntu-20-04/)

Ubuntu 17.10 and later uses [Netplan](https://netplan.io/) as the default network management tool. The previous Ubuntu versions were using *ifconfig* and its configuration file `/etc/network/interfaces` to configure the network.

Netplan configuration files are written in YAML syntax with a `.yaml` file extension. To configure a network interface with Netplan, you need to create a YAML description for the interface, and Netplan will generate the required configuration files for the chosen renderer tool.

Netplan supports two renderers, **NetworkManager** and Systemd-**networkd**. NetworkManager is mostly used on Desktop machines, while the Systemd-networkd is used on servers without a GUI.

If your Ubuntu cloud instance is provisioned with cloud-init, you’ll need to **disable** it. To do so create the following file:

```Shell
$ sudo vim /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg
$ cat /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg
network: {config: disabled}
```

To assign a static IP address on the network interface, open the YAML configuration file with your text editor :

```Shell
# 初始配置内容如下
$ cat /etc/netplan/01-netcfg.yaml

network:
  version: 2
  renderer: networkd
  ethernets:
    ens3:
      dhcp4: yes
```

编辑 `01-netcfg.yaml` 文件，禁用 dhcp4，设置静态IP地址：

```Shell
$ sudo vim /etc/netplan/01-netcfg.yaml
$ cat /etc/netplan/01-netcfg.yaml

network:
  version: 2
  renderer: networkd
  ethernets:
    ens3:
      dhcp4: no
      addresses:
        - 192.168.121.221/24
      gateway4: 192.168.121.1
      nameservers:
          addresses: [8.8.8.8, 1.1.1.1]
```

执行 apply 命令应用最新配置：

```Shell
sudo netplan apply
```

查看网口的 IP 地址：

```Shell
ip addr show dev ens3
```

### netplan3

[How to Configure Static IP Address on Ubuntu 20.04](https://www.tecmint.com/set-static-ip-address-in-ubuntu/)

1. How to Set Static IP Address On Ubuntu Desktop via `GNOME`  
2. How to Set Static IP Address on Ubuntu Server Using `Netplan`  


```Shell
$ cat /etc/netplan/01-network-manager-all.yaml

network:
  version: 2
  ethernets:
     enp0s3:
        dhcp4: false
        addresses: [192.168.2.100/24]
        gateway4: 192.168.2.1
        nameservers:
          addresses: [8.8.8.8, 8.8.4.4]
```

---

[Configure Ubuntu WiFi Adapter with Netplan](https://dev.to/joeneville_/configure-ubuntu-wifi-with-netplan-4je0)

1. Create a netplan yaml file `mynet1.yaml` in the /etc/netplan directory.

```YAML
network:
  ethernets:
    eno1:
      addresses:
        - 10.150.15.25/24
  wifis:
    wlan0:
      dhcp4: yes
      dhcp6: yes
      access-points:
        your_wifi_name:
          password: "your_wifi_password"
  version: 2
  renderer: NetworkManager
```

2. Apply the Netplan file：`netplan apply <your-netplan-file-name>`

## rpi4b-netplan

[Ubuntu Server 1804 之 WiFi设置](https://zhuanlan.zhihu.com/p/93445338)

Netplan 是一个简便的Linux网络配置工具，其会从 /etc/netplan/*.yaml 读取网络设置，并在 /run 生成特定的后端配置文件，用于网络设备进程控制。

Netplan 当前版本支持两种网络管理接口:

- NetworkManager  
- Systemd-networkd  

服务器版与桌面版相比，其默认安装的程序包较少，所以在进行wifi配置管理时，有需特别注意的地方。

- 如需使用 NetworkManager ，记得安装此程序包。而使用 Systemd-networkd ，则无需安装。  
- 记得安装 wpa-supplicant 程序包，用于wifi密码相关功能，否则无法登陆有密码的wifi网络。  
- 接着使用 `ip a` 命令，获取无线网卡设备名称，这个设备名称将用于下一步的配置文件中。  

[Ubuntu 通过 Netplan 配置网络教程](https://segmentfault.com/a/1190000040728591)  
[How to configure networking with Netplan on Ubuntu](https://vitux.com/how-to-configure-networking-with-netplan-on-ubuntu/)  

### 查看网口名称

执行相关命令查看 RPi4B/ubuntu 网络接口名称：

1. 有线以太网口：`eth0`；  
2. 无线WiFi网卡：`wlan0`；  

```Shell
rpi4b-ubuntu% ls /sys/class/net
eth0  lo  wlan0

rpi4b-ubuntu% ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000
    link/ether dc:a6:32:**:**:** brd ff:ff:ff:ff:ff:ff
3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether dc:a6:32:**:**:** brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.114/24 brd 192.168.0.255 scope global dynamic noprefixroute wlan0
       valid_lft 4690sec preferred_lft 4690sec
    inet6 fe80::389c:b4c0:a546:e78/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

### 增加网络配置

rpi4b-ubuntu 的 /etc/netplan/ 下默认有两个 yaml 配置文件：

```Shell
rpi4b-ubuntu% ls -lhFA /etc/netplan
total 8.0K
-rw-r--r-- 1 root root 104 Oct 13 21:47 01-network-manager-all.yaml
-rw-r--r-- 1 root root 201 Sep 22 17:39 10-rpi-ethernet-eth0.yaml
```

执行 `sudo vim /etc/netplan/11-rpi-wifi-wlan0.yaml` 新建无线网络配置：

```YAML
network:
#   version: 2
#   renderer: NetworkManager
#   ethernets:
#     eth0:
#       dhcp4: true
#       optional: true
# config wifi
  wifis:
    wlan0:
      dhcp4: false
      dhcp6: false
      access-points:
        "HiWiFi-2.4":
          password: "your_wifi_password"
      addresses: [192.168.0.124/24, 192.168.0.128/24]
      nameservers:
        addresses: [192.168.0.1, 8.8.8.8, 8.8.4.4]
      routes:
        - to: default
          via: 192.168.0.1
```

**注意**：网关配置用了新的关键字 routes，不再用旧的过期关键字 gateway4。

### 测试配置文件

在应用任何更改之前，先执行 try 命令测试配置文件。

```Shell
sudo netplan try
```

如果没有问题，它将返回配置接受消息。如果配置文件未通过测试，它将恢复为以前的工作配置。

```Shell
rpi4b-ubuntu% sudo netplan try

An error occurred: 'NetplanApply' object has no attribute 'state'

Reverting.
```

参考 [Ubuntu 21.10 - Netplan: object has no attribute 'state'](https://askubuntu.com/questions/1369646/ubuntu-21-10-netplan-object-has-no-attribute-state)，改为携带 `--state` 选项执行：

```Shell
rpi4b-ubuntu% sudo netplan try --state /etc/netplan
Do you want to keep these settings?


Press ENTER before the timeout to accept the new configuration


Changes will revert in 101 seconds
Configuration accepted.
```

### 应用配置文件

接下来，可以执行 `sudo netplan apply` 命令应用配置更新。

可携带 `--debug` 选项输出调试信息：

```Shell
sudo netplan -d apply /etc/netplan/10-rpi-ethernet-eth0.yaml
sudo netplan --debug apply /etc/netplan/11-rpi-wifi-wlan0.yaml
```

#### 以太网配置排错

默认的 eth0 有线以太网配置报错，参考 [netplan apply fails with "Cannot find unique matching interface for eth0"](https://raspberrypi.stackexchange.com/questions/133639/netplan-apply-fails-with-cannot-find-unique-matching-interface-for-eth0)：

```Shell
rpi4b-ubuntu% sudo netplan apply
[]
Cannot find unique matching interface for eth0: {'driver': 'bcmgenet smsc95xx lan78xx'}
```

暂时不用以太网连接，先将 match 和 set-name 这三行注释掉。

```Shell
rpi4b-ubuntu% cat /etc/netplan/10-rpi-ethernet-eth0.yaml
network:
  ethernets:
    eth0:
      # Rename the built-in ethernet device to "eth0"
      # match:
      #  driver: bcmgenet smsc95xx lan78xx
      # set-name: eth0
      dhcp4: true
      optional: true
```

### 重启网络服务

成功应用所有配置后，通过运行以下命令重新启动 network 服务：

如果是 Ubuntu Desktop 桌面版，请用以下命令：

```Shell
sudo systemctl restart network-manager
```

如果是 Ubuntu Server 服务版，请改用以下命令：

```Shell
sudo systemctl restart system-networkd
```

[ubuntu network manager 网络管理](https://blog.csdn.net/superjunenaruto/article/details/109280157)  
[【解决】Failed to restart network.service: Unit network.service not found.](https://www.cnblogs.com/leozhanggg/p/11772251.html)  

[Ubuntu 20.04 Server 64-bit - Raspberry Pi 4 - The network icon shows me disconnected while in reality I am properly connected to the internet](https://askubuntu.com/questions/1337824/ubuntu-20-04-server-64-bit-raspberry-pi-4-the-network-icon-shows-me-disconne)

Run `sudo service network-manager restart` or `sudo reboot`.

[Installing Network Manager on Raspbian](https://gist.github.com/jjsanderson/ab2407ab5fd07feb2bc5e681b14a537a)

去掉 sudo 执行 restart，输入密码：

```Shell
systemctl status NetworkManager
systemctl restart NetworkManager
```

## rpi4b-manual

RPi4B/ubuntu desktop 下经过一番 netplan 折腾，还是没能成功设置静态IP地址。
最终还是通过键鼠屏进入 rpi4b-ubuntu 桌面，进入设置-网络，手动配置wifi的IPv4静态IP地址。

## Feb21, 2024

好久没有启动 RPi 4B，今天启动后，发现IP没有起来。
找到之前玩 RPi 3B 时捎带的 PL2303 USB2TTL 串口线，连接上使用命令行 `ls /dev/tty.usbserial*` 找到串口tty名称。
在 macOS Sonoma 终端通过命令 `screen /dev/tty.usbserial-1130 115200` 成功连接上 RPi 4B。

执行 `ip link show` 显示 wlan0 为 DOWN 状态：

```
3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state DOWN mode DORMANT group default qlen 1000
    link/ether d0:a0:30:d0:30:d3 brd ff:ff:ff:ff:ff:ff
```

执行 `ip link set wlan0 up`，报错提示如下：

```
/etc/netplan/50-cloud-init.yaml  Error in network definition: Updated definition 'wlan0' changes device type
```

**问题分析**：/etc/netplan/50-cloud-init.yaml 中定义了 ethernets/wlan0，与 /etc/netplan/11-rpi-wifi-wlan0.yaml 定义的 wifis/wlan0 冲突了。

**解决方案**：把 /etc/netplan/50-cloud-init.yaml 中关于 ethernets/wlan0 的配置注释屏蔽掉：

```
$ cat /etc/netplan/50-cloud-init.yaml
# This file is generated from information provided by the datasource.  Changes
# to it will not persist across an instance reboot.  To disable cloud-init's
# network configuration capabilities, write a file
# /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
# network: {config: disabled}
network:
  #    ethernets:
  #        wlan0:
  #            dhcp4: true
  #            match:
  #                macaddress: dc:a6:32:d1:33:d3
  #            set-name: wlan0
    version: 2
```

再执行 `sudo netplan apply`，成功应用 11-rpi-wifi-wlan0.yaml，bring up wlan0 并配置静态IP。

### refs

[networking - Fail to up interface wlan0 in ubuntu server 22.04 Raspberry Pi - Ask Ubuntu](https://askubuntu.com/questions/1407831/fail-to-up-interface-wlan0-in-ubuntu-server-22-04-raspberry-pi)

> According to the netplan(5) man page, wifi interface(wlan0) needs to be in a `wifis:` section instead of a `ethernets:` section.

[ubuntu - Netplan - Error in network definition: Updated definition changes device type - Server Fault](https://serverfault.com/questions/1088663/netplan-error-in-network-definition-updated-definition-changes-device-type)

按照 Huobur@Medium 提供的方法，没有解决。问题不一样，我这是接口名称冲突，他那是有线和无限网络冲突。

[How to Setup WiFi on Raspberry Pi 4 with Ubuntu 20.04 LTS 64-bit ARM Server](https://huobur.medium.com/how-to-setup-wifi-on-raspberry-pi-4-with-ubuntu-20-04-lts-64-bit-arm-server-ceb02303e49b)
