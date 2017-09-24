wlan0 RF-kill - Soft blocked
===

[Operation not possible due to RF-kill](https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=146198)  
[Wifi on Raspberry Pi 3](http://osric.com/chris/accidental-developer/2017/09/wifi-on-raspberry-pi-3/)  

```Shell
pi@raspberrypi:~$ ifconfig
eth0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether b8:27:eb:15:21:7c  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1  (Local Loopback)
        RX packets 9  bytes 524 (524.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 9  bytes 524 (524.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

```Shell
pi@raspberrypi:~$ ifconfig wlan0
wlan0: flags=4098<BROADCAST,MULTICAST>  mtu 1500
        ether b8:27:eb:40:74:29  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

```Shell
pi@raspberrypi:~$ iwconfig
eth0      no wireless extensions.

lo        no wireless extensions.

wlan0     IEEE 802.11  ESSID:off/any  
          Mode:Managed  Access Point: Not-Associated   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
```

```Shell
pi@raspberrypi:~$ sudo iwlist wlan0 scan
wlan0     Interface doesn't support scanning : Network is down

pi@raspberrypi:~$ sudo cat /etc/wpa_supplicant/wpa_supplicant.conf
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=CN

network={
        ssid="HiWiFi"
        psk="***"
        key_mgmt=WPA-PSK
}
```

如何配置，如何连接指定 SSID？

```Shell
pi@raspberrypi:~$ sudo ifconfig wlan0 up
SIOCSIFFLAGS: Operation not possible due to RF-kill
```

```Shell
pi@raspberrypi:~$ sudo rfkill list
0: phy0: Wireless LAN
        Soft blocked: yes
        Hard blocked: no
```

解决：执行 `sudo rfkill unblock wifi` 命令解除软阻塞。

```Shell
pi@raspberrypi:~$ sudo rfkill unblock wifi
pi@raspberrypi:~$ sudo rfkill list
0: phy0: Wireless LAN
        Soft blocked: no
        Hard blocked: no
```

```Shell
pi@raspberrypi:~$ ifconfig
eth0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether b8:27:eb:15:21:7c  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1  (Local Loopback)
        RX packets 17  bytes 1004 (1004.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 17  bytes 1004 (1004.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.106  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::2028:ac98:d786:60e7  prefixlen 64  scopeid 0x20<link>
        ether b8:27:eb:40:74:29  txqueuelen 1000  (Ethernet)
        RX packets 1173  bytes 111556 (108.9 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1519  bytes 1013928 (990.1 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
