[SSH (SECURE SHELL)](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md)  
[SSH USING LINUX OR MAC OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)  
[SCP (SECURE COPY)](https://www.raspberrypi.org/documentation/remote-access/ssh/scp.md)  
[RSYNC](https://www.raspberrypi.org/documentation/remote-access/ssh/rsync.md)  

[Exit SSH session in OSX Terminal](https://superuser.com/questions/404103/exit-ssh-session-in-osx-terminal)  
[无屏幕和键盘配置树莓派WiFi和SSH](http://shumeipai.nxez.com/2017/09/13/raspberry-pi-network-configuration-before-boot.html?variant=zh-cn)  

## SCP
[SCP](http://blog.163.com/fjm_520/blog/static/18904914820119284847660/)：secure copy (remote file copy program) 是一个基于 SSH 安全协议的文件传输命令。

与 sftp 不同的是，它只提供主机间的文件传输功能，没有文件管理的功能。

1. 复制 local_file 到远程目录 remote_folder 下：

```Shell
scp local_file remote_user@host:remote_folder
```

2. 复制 local_folder 到远程 remote_folder（需要加参数 `-r` 递归）

```Shell
scp –r local_folder remote_user@host:remote_folder
```

以上命令反过来写就是从远程复制（下载）到本地。
