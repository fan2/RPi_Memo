

[How to install and use “Screen” on Linux](https://www.hugeserver.com/kb/install-use-screen-linux/)  
["Screen" is very useful on the Pi !](https://www.raspberrypi.org/forums/viewtopic.php?t=8099&p=101209#p97107)

```Shell
pi@raspberrypi:~ $ sudo apt-get install screen
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Suggested packages:
  byobu | screenie | iselect
The following NEW packages will be installed:
  screen
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 547 kB of archives.
After this operation, 922 kB of additional disk space will be used.
Get:1 http://mirrordirector.raspbian.org/raspbian stretch/main armhf screen armhf 4.5.0-6 [547 kB]
Fetched 547 kB in 5s (106 kB/s)                               
Selecting previously unselected package screen.
(Reading database ... 123148 files and directories currently installed.)
Preparing to unpack .../screen_4.5.0-6_armhf.deb ...
Unpacking screen (4.5.0-6) ...
Processing triggers for install-info (6.3.0.dfsg.1-1+b1) ...
Processing triggers for systemd (232-25+deb9u1) ...
Processing triggers for man-db (2.7.6.1-2) ...
Setting up screen (4.5.0-6) ...
Processing triggers for systemd (232-25+deb9u1) ...
pi@raspberrypi:~ $ screen -v
Screen version 4.05.00 (GNU) 10-Dec-16

```