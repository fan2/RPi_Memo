
## SSH服务

[How to Enable SSH on Ubuntu 18.04](https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-18-04/)  
[Ubuntu Linux install OpenSSH server](https://www.cyberciti.biz/faq/ubuntu-linux-install-openssh-server/)  

安装 SSH 服务：

```Shell
sudo apt update
sudo apt install openssh-server
```

查看 SSH 服务状态：

```Shell
sudo systemctl status ssh
```

应该看到 ssh.service 默认已启动：`Active: active (running)`。

否则，执行以下命令启动 SSH 服务：

```Shell
sudo systemctl enable ssh
sudo systemctl start ssh
```

开启防火墙，并放行 ssh 端口 22：

```Shell
sudo ufw enable
sudo ufw status
# sudo ufw allow 22
sudo ufw allow ssh
```

接下来，即可在其他 ssh client 上通过 ssh 命令远程访问 rpi4b-ubuntu：

```Shell
ssh username@ip_address
```

### ssh via local host

[Connect to Linux by name rather than IP](https://superuser.com/questions/185678/connect-to-linux-by-name-rather-than-ip)  

> mDNS - [Avahi](http://avahi.org/) with nss_mdns on Linux; Host names are always in the form `hostname.local`.

[Cannot ssh into Ubuntu Server by hostname](https://askubuntu.com/questions/144280/cannot-ssh-into-ubuntu-server-by-hostname)  

Install the avahi-daemon package on your Ubuntu server. This utilizes the **mDNS** protocol to "advertise" its hostname on your local network. Once it's installed and running, you should be able to `ssh ubuntu-server.local` (notice the `.local` domain) and access the server.

在 RPi4B/ubuntu 首次开机设置向导，设置了机器名为 `rpi4b-ubuntu`，则同一局域网内可通过 ssh 直接连接 local 域名的 hostname：

```Shell
ssh faner@rpi4b-ubuntu.local
```

#### change username

microHDMI + USB 连接键盘进入 Ubuntu Server tty，参考 [How do I change my username?](https://askubuntu.com/questions/34074/how-do-i-change-my-username) - Valentin Uveges，以 root 登录后修改用户名为 pifan。

- [Proper way of changing username in Ubuntu or any linux](https://unix.stackexchange.com/questions/98461/proper-way-of-changing-username-in-ubuntu-or-any-linux)  
- [Ubuntu set hostname permanently (computer name) command](https://www.cyberciti.biz/faq/ubuntu-set-hostname-permanently-command/)  

#### change hostname

也可在 ubuntu 中通过 hostnamectl set-hostname 修改机器名：

- [如何在 Ubuntu 20.04 上修改主机名](https://cloud.tencent.com/developer/article/1649332)  
- [Ubuntu set hostname permanently command](https://www.cyberciti.biz/faq/ubuntu-set-hostname-permanently-command/)  

```Shell
pifan@ubuntu:~$ hostnamectl
 Static hostname: ubuntu
       Icon name: computer
      Machine ID: c45f627961184d0f900ea534eb047c6f
         Boot ID: 4fb0fe66f1154654bc8d06942a2bf09b
Operating System: Ubuntu 21.10
          Kernel: Linux 5.13.0-1008-raspi
    Architecture: arm64
# 修改hostname
pifan@ubuntu:~$ sudo hostnamectl set-hostname rpi4b-ubuntu
pifan@ubuntu:~$ echo $HOST
rpi4b-ubuntu
```

执行 `avahi-daemon -V` 查看版本，提示没有安装，执行 apt install 安装。

```Shell
pifan@rpi4b-ubuntu:~$ avahi-daemon -V
Command 'avahi-daemon' not found, but can be installed with:
sudo apt install avahi-daemon

pifan@rpi4b-ubuntu:~$ sudo apt install avahi-daemon
```

安装 avahi-daemon 0.8 后， 通过 `ssh pifan@rpi4b-ubuntu.local` 命令成功连接上。

### arp detect ip from mac

如果RPi没有设置静态IP地址，那么每次DHCP获取的IP地址可能不一样。

如果记住了 RPi 无线网口 wlan0 的 MAC 地址：

```Shell
rpi4b-ubuntu% ifconfig wlan0
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.114  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::389c:b4c0:a546:e78  prefixlen 64  scopeid 0x20<link>
        ether dc:a6:32:**:**:**  txqueuelen 1000  (Ethernet)
        RX packets 48345  bytes 57983063 (57.9 MB)
        RX errors 0  dropped 1  overruns 0  frame 0
        TX packets 26624  bytes 4374785 (4.3 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

在 macOS SSH 客户端，通过 arp 查询该 MAC 地址所在的 IP：

```Shell
$ arp -a | grep "dc:a6:32"
? (192.168.0.114) at dc:a6:32:**:**:** on en0 ifscope [ethernet]
```

通过以下脚本，提取括号中的 IP 地址：

```Shell
# awk -F 指定多个分割符
arp -na | grep "dc:a6:32" | awk -F '[()]' '{print$2}'
# sed前向引用，替换提取指定子模式
arp -na | grep "dc:a6:32" | sed 's/.*(\(.*\)).*/\1/'
# awk先分割左括号，再替换右括号后面为空
arp -na | grep "dc:a6:32" | awk -F '(' '{sub(/\).*/, "", $2);print$2}'
# 其他思路：字符串处理，先截左留右，再截右留左
```
