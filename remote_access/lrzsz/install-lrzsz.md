## macOS 安装 lrzsz
1. 在 macOS 上执行 `brew install lrzsz` 命令安装 lrzsz。

```Shell
faner@THOMASFAN-MB0:~|⇒  brew search lrzsz
==> Searching local taps...
lrzsz
==> Searching taps on GitHub...
==> Searching blacklisted, migrated and deleted formulae...
faner@THOMASFAN-MB0:~|⇒  brew install lrzsz

==> Downloading https://homebrew.bintray.com/bottles/lrzsz-0.12.20.sierra.bottle.tar.gz
######################################################################## 100.0%
==> Pouring lrzsz-0.12.20.sierra.bottle.tar.gz
🍺  /usr/local/Cellar/lrzsz/0.12.20: 18 files, 415.9KB
```

2. 执行 `sz -h` 查看发送组件命令 sz 的帮助说明：

```Shell
faner@THOMASFAN-MB0:~|⇒  sz -h
sz version 0.12.20
Usage: sz [options] file ...
   or: sz [options] -{c|i} COMMAND
Send file(s) with ZMODEM/YMODEM/XMODEM protocol
```

3. 执行 `rz -h` 查看接收组件命令 rz 的帮助说明：

```Shell
faner@THOMASFAN-MB0:~|⇒  rz -h
rz version 0.12.20
Usage: rz [options] [filename.if.xmodem]
Receive files with ZMODEM/YMODEM/XMODEM protocol
```

## raspbian 安装 lrzsz
1. 在 raspbian 上执行 `sudo apt-get install lrzsz` 命令安装 lrzsz。

```Shell
pi@raspberrypi:~$ sudo apt-get install lrzsz
Reading package lists... 0%Reading package lists... 100%Reading package lists... Done
Building dependency tree... 0%Building dependency tree... 0%Building dependency tree... 50%Building dependency tree... 50%Building dependency tree... 96%Building dependency tree       
Reading state information... 0%Reading state information... 0%Reading state information... Done
Suggested packages:
  minicom
The following NEW packages will be installed:
  lrzsz
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 81.8 kB of archives.
After this operation, 196 kB of additional disk space will be used.
0% [Working]0% [Working]0% [Working]0% [Working]0% [Connecting to mirrordirector.raspbian.org (93.93.128.193)]                                                              0% [Waiting for headers]                        0% [Working]0% [Working]0% [Working]0% [Connecting to mirrors.zju.edu.cn (210.32.158.231)]                                                      Get:1 http://mirrors.zju.edu.cn/raspbian/raspbian stretch/main armhf lrzsz armhf 0.12.21-8 [81.8 kB]
                                                      3% [1 lrzsz 2,625 B/81.8 kB 3%]72% [1 lrzsz 73.2 kB/81.8 kB 89%]                                 100% [Working]              Fetched 81.8 kB in 5s (15.6 kB/s)
Selecting previously unselected package lrzsz.
(Reading database ... (Reading database ... 5%(Reading database ... 10%(Reading database ... 15%(Reading database ... 20%(Reading database ... 25%(Reading database ... 30%(Reading database ... 35%(Reading database ... 40%(Reading database ... 45%(Reading database ... 50%(Reading database ... 55%(Reading database ... 60%(Reading database ... 65%(Reading database ... 70%(Reading database ... 75%(Reading database ... 80%(Reading database ... 85%(Reading database ... 90%(Reading database ... 95%(Reading database ... 100%(Reading database ... 122683 files and directories currently installed.)
Preparing to unpack .../lrzsz_0.12.21-8_armhf.deb ...
Unpacking lrzsz (0.12.21-8) ...
Setting up lrzsz (0.12.21-8) ...
Processing triggers for man-db (2.7.6.1-2) ...
```

2. 执行 `sz -h` 查看发送组件命令 sz 的帮助说明：

```Shell
pi@raspberrypi:~$ sz -h
sz version 0.12.21rc
Usage: sz [options] file ...
   or: sz [options] -{c|i} COMMAND
Send file(s) with ZMODEM/YMODEM/XMODEM protocol
```

3. 执行 `rz -h` 查看接收组件命令 rz 的帮助说明：

```Shell
pi@raspberrypi:~$ rz -h
rz version 0.12.21rc
Usage: rz [options] [filename.if.xmodem]
Receive files with ZMODEM/YMODEM/XMODEM protocol
```
