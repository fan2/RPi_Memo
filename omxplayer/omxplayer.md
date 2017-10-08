
[omxplayer](https://github.com/popcornmix/omxplayer) -- Raspberry Pi command line OMX player

omxplayer是专门针对树莓派的GPU的播放器，该 GPU（VideoCore）提供的官方API接口是 OpenMAX。

[omxplayer](http://www.raspberry-projects.com/pi/software_utilities/media-players/omxplayer) on [elinux](http://elinux.org/Omxplayer)

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

# usage

[Playing audio on the Raspberry Pi](https://www.raspberrypi.org/documentation/usage/audio/README.md)  
[Playing video on the Raspberry Pi](https://www.raspberrypi.org/documentation/usage/video/README.md)  

[raspbian 中的 OMXPlayer 播放器的使用](http://www.xuebuyuan.com/2060857.html)

```Shell
omxplayer -r -o hdmi filename
```

[树莓派 omxplayer 播放电影小记](http://hi.ktsee.com/372.html)  
[converting a video to H.264 for omxplayer with Handbrake](https://learn.adafruit.com/raspberry-pi-video-looper/omxplayer)  
