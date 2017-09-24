- raspberrypi 官方参考文档：remote access raspberrypi by [VNC (VIRTUAL NETWORK COMPUTING)](https://www.raspberrypi.org/documentation/remote-access/vnc/)；  
- realVNC 官方参考文档：[VNC Connect and Raspberry Pi](https://www.realvnc.com/en/connect/docs/raspberry-pi.html)。  

[Setting Up a VNC Server on Your Raspberry Pi](http://www.instructables.com/id/Setting-up-a-VNC-Server-on-your-Raspberry-Pi/)  

- [realVNC](https://www.realvnc.com/en/): apps for all platforms  
- [TightVNC](http://www.tightvnc.com/): simple Web Browser for macOS with Java Viewer  
- [UltraVNC](http://www.uvnc.com/): simple Web Browser for macOS with Java Viewer  

## [realVNC](https://www.realvnc.com/en/)
### [realVNC for raspberrypi](https://www.realvnc.com/en/raspberrypi/)

VNC Connect is included with Raspbian for Raspberry Pi  
Connect to your Raspberry Pi from anywhere  

RealVNC/[raspi-preview](https://github.com/RealVNC/raspi-preview)

### [VNC Connect and Raspberry Pi](https://www.realvnc.com/en/connect/docs/raspberry-pi.html)

- **VNC Server** enables you to connect to your Pi from a desktop computer or mobile device, watch its screen in real-time, and exercise control as though you were sitting in front of it.  
- **VNC Viewer** enables you to connect to and control a desktop computer (or another Pi) from your Pi, should you want to.  

```Shell
sudo apt-get update 
sudo apt-get install realvnc-vnc-server 
sudo apt-get install realvnc-vnc-viewer
```

### [Download VNC Viewer to the device to control from](https://www.realvnc.com/en/connect/download/viewer/raspberrypi/)

### geometry
[How can I change the geometry of a VNC Server in Virtual Mode desktop?](https://support.realvnc.com/Knowledgebase/Article/View/393/5/how-can-i-change-the-geometry-of-a-vnc-server-in-virtual-mode-desktop)  

```Shell
vncserver -geometry 800x600
```

[Change screen resolution over VNC](https://www.raspberrypi.org/forums/viewtopic.php?f=66&t=41378&sid=f2b85139e6fb9b707ddff076dc17c5c6)
[Troubleshooting VNC Server on the Raspberry Pi](https://support.realvnc.com/Knowledgebase/Article/View/523/2/troubleshooting-vnc-server-on-the-raspberry-pi) / Changing the Raspberry Pi's screen resolution  

## Apple Remote Desktop
[Remote Desktop Support](https://support.apple.com/remote-desktop) / [Apple Remote Desktop 3](https://www.apple.com/cn/remotedesktop/)  

[下载：Apple Remote Desktop 3.9.2 客户端](https://support.apple.com/kb/DL1909?locale=zh_CN)  
[Download: Apple Remote Desktop 3.9.3 Client](https://support.apple.com/kb/DL1924?locale=en_US)  

[macOS Sierra: Allow Remote Desktop to access your computer](https://support.apple.com/kb/PH25556?viewlocale=en_US&locale=en_US)  

## references
[树莓派 raspbian 开启VNC](http://bbs.shumeipaiba.com/thread-12-1-1.html)  
[VNC远程登录树莓派的图形界面](http://shumeipai.nxez.com/2013/09/04/login-rpi-with-vnc.html?variant=zh-cn)  
[使用VNC远程登录树莓派的图形界面](http://www.cnblogs.com/haochuang/p/6743387.html)  
[树莓派：VNC远程登录Raspbian图形界面（tightvncserver）](http://blog.csdn.net/lu_embedded/article/details/50621203)  
