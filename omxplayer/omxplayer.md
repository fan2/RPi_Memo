
[omxplayer](https://github.com/popcornmix/omxplayer) -- Raspberry Pi command line OMX player

omxplayer是专门针对树莓派的GPU的播放器，该 GPU（VideoCore）提供的官方API接口是 OpenMAX。

[omxplayer](http://www.raspberry-projects.com/pi/software_utilities/media-players/omxplayer) on [elinux](http://elinux.org/Omxplayer)

# SoC & OS

- **SoC**：`Raspberry Pi 3 Model B v1.2`(2015)  
- **OS**：`2017-09-07-raspbian-stretch.zip`  

```shell
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

[raspbian 中的 OMXPlayer 播放器的使用](http://www.xuebuyuan.com/2060857.html)  

执行 `omxplayer -h` 查看帮助，或执行 `man omxplayer` 查看手册。

## play media

[Playing audio on the Raspberry Pi](https://www.raspberrypi.org/documentation/usage/audio/README.md)  

```shell
omxplayer example.mp3
```

[Playing video on the Raspberry Pi](https://www.raspberrypi.org/documentation/usage/video/README.md)  

```shell
omxplayer example.mp4
```

[树莓派 omxplayer 播放电影小记](http://hi.ktsee.com/372.html)  

```shell
omxplayer -r -o hdmi filename
```

[converting a video to H.264 for omxplayer with Handbrake](https://learn.adafruit.com/raspberry-pi-video-looper/omxplayer)  

## KEY BINDINGS

`man omxplayer` 或 `omxplayer -k` 可查看命令行播放控制快捷键。

```shell
pi@raspberrypi:~ $ omxplayer -k

    1           decrease speed
    2           increase speed
    <           rewind
    >           fast forward
    z           show info
    j           previous audio stream
    k           next audio stream
    i           previous chapter
    o           next chapter
    n           previous subtitle stream
    m           next subtitle stream
    s           toggle subtitles
    w           show subtitles
    x           hide subtitles
    d           decrease subtitle delay (- 250 ms)
    f           increase subtitle delay (+ 250 ms)
    q           exit omxplayer
    p / space   pause/resume
    -           decrease volume
    + / =       increase volume
    left arrow  seek -30 seconds
    right arrow seek +30 seconds
    down arrow  seek -600 seconds
    up arrow    seek +600 seconds

```
