
## ubuntu

[Install Ubuntu on a Raspberry Pi](https://ubuntu.com/download/raspberry-pi)

Raspberry Pi 4: At least 4 GB RAM required

[How to install Ubuntu Server on your Raspberry Pi](https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi)

1. How to create a bootable Ubuntu Server microSD card  
2. How to setup internet connectivity on the Raspberry Pi  
3. How to access your Raspberry Pi remotely  

## 安装步骤

安装步骤参考 [RPi4B安装Ubuntu_Desktop](./RPi4B安装Ubuntu_Desktop.md)，可通过 RPi-Imager 或手动 Manually 两种方式安装。

[How to check if Ubuntu Desktop or Server is installed? - Ask Ubuntu](https://askubuntu.com/questions/12562/how-to-check-if-ubuntu-desktop-or-server-is-installed)

Check the existing dirs in the home dir(`~/`). In Desktop Edition you'll see folders like Desktop, Downloads, Music, etc. whereas in Server Edition it's empty.

I use only ubuntu-desktop (vanilla) or ubuntu server. For me the `dpkg -l ubuntu-desktop` it's a very reliable method to determine if its a desktop or server.

```bash
$ dpkg -l ubuntu-desktop
dpkg-query: no packages found matching ubuntu-desktop
```

## 无屏配置

> Ubuntu Desktop 无屏折腾了一通，SSH还是无法连接，最终还是连接键鼠屏进去配置！

### guide

We are going to edit files you just downloaded on your SD card to ensure your Pi can connect to the Wi-Fi network at **boot**.
With the SD card still inserted in your laptop, open a file manager and locate the “`system-boot`” partition on the card. It contains initial configuration files that load during the first boot process.

Edit the `network-config` file to add your Wi-Fi credentials.

```Shell
vim /Volumes/system-boot/network-config

wifis:
  wlan0:
    dhcp4: no
    dhcp6: no
    access-points:
      "HiWiFi-2.4":
        password: "password2"
    addresses: 
      - 192.168.0.124/24
    gateway4: 192.168.0.1
    nameservers:
      addresses: [192.168.0.1, 8.8.8.8, 8.8.4.4]
```

### refs

[树莓派4b ubuntu server 设置屏幕热插拔](https://blog.csdn.net/benchuspx/article/details/112576609)

[树莓派raspberry pi 4b ubuntu20.04LTS 配置（含显示器以及wifi）](https://blog.csdn.net/weixin_43403879/article/details/114230532)

- 在 network 文件里面添加wifi信息？

[Setup ubuntu server on Raspberry Pi 4 without keyboard](https://askubuntu.com/questions/1192485/setup-ubuntu-server-on-raspberry-pi-4-without-keyboard)  

[9-Steps Raspberry Pi Headless Setup with Ubuntu 21.04](https://dev.to/henri_rion/9-steps-raspberry-pi-headless-setup-with-ubuntu-21-04-3el3)  

/boot/config.txt  

```
# uncomment if hdmi display is not detected and composite is being output
# a** by faner, 05Feb22.
hdmi_force_hotplug=1

# uncomment to force a specific HDMI mode (this will force VGA)
# a** by faner, 05Feb22.
hdmi_group=2
hdmi_mode=82 # 1080p60Hz
```

/boot/network-config  

```
version: 2
ethernets:
  eth0:
    dhcp4: true
    optional: true
wifis:
  wlan0:
  dhcp4: true
  optional: true
  access-points:
    your_wifi_name:
    password: "your_wifi_password"
```