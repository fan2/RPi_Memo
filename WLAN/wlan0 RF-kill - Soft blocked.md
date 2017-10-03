# wlan0 RF-kill - Soft blocked

> [Wifi on Raspberry Pi 3](http://osric.com/chris/accidental-developer/2017/09/wifi-on-raspberry-pi-3/)  
> [Operation not possible due to RF-kill](https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=146198)  
> [Wireless network configuration](https://wiki.archlinux.org/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)) | Rfkill 警告  

## iwconfig
执行 `iwconfig` 命令，根据显示的信息可知无线网卡 `wlan0` 尚未连接：

```Shell
pi@raspberrypi:~$ iwconfig
eth0      no wireless extensions.

lo        no wireless extensions.

wlan0     IEEE 802.11  ESSID:off/any  
          Mode:Managed  Access Point: Not-Associated   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
```

## iwlist scan
1. 执行 `iwlist wlan0 scan` 命令，查看无线网卡 `wlan0` 扫描到的 WiFi Access Points：

```Shell
pi@raspberrypi:~$ iwlist wlan0 scan
wlan0     Interface doesn't support scanning : Network is down
```

> 提示无法扫描，原因是 `Network is down`。

2. 执行 `ifconfig wlan0 up` 命令，尝试重新 bring wlan0 up：

```Shell
pi@raspberrypi:~$ sudo ifconfig wlan0 up
SIOCSIFFLAGS: Operation not possible due to RF-kill
```

> 提示操作无法执行，原因是 `RF-kill`。

## rfkill unblock
1. 执行 `sudo rfkill list` 命令，列举查看 available rfkill-using devices：

```Shell
pi@raspberrypi:~$ sudo rfkill list
0: phy0: Wireless LAN
        Soft blocked: yes
        Hard blocked: no
```

> 根据提示可知，Soft blocked！

2. 解决：执行 `sudo rfkill unblock wifi` 命令解除软阻塞。

```Shell
pi@raspberrypi:~$ sudo rfkill unblock wifi
pi@raspberrypi:~$ sudo rfkill list
0: phy0: Wireless LAN
        Soft blocked: no
        Hard blocked: no
```

解除软阻塞后，过一会儿 wlan0 恢复正常，自动扫描连接上上次的 WiFi（ESSID:"HiWiFi"）。

重新执行 ifconfig，可以看到 wlan0 连接成功，网络恢复正常。
