[**Raspberry Pi Screenshots**](http://www.instructables.com/id/Raspberry-Pi-Screenshots/)

[How To Take Screenshots On The Raspberry Pi](https://www.raspberrypi-spy.co.uk/2013/10/how-to-take-screenshots-on-the-raspberry-pi/) OCTOBER 5, 2013  
[How to take a screenshot on Raspberry Pi](https://www.imore.com/how-take-screenshot-raspberry-pi) Mar 14, 2016  
[How to take a screenshot on the Raspberry Pi](https://www.cnet.com/how-to/how-to-take-a-screenshot-on-the-raspberry-pi/) MAY 26, 2016  

## Step 2: Instal Scrot
```Shell
pi@raspberrypi:~$ sudo apt-get install scrot
Reading package lists... Done
Building dependency tree       
Reading state information... Done
scrot is already the newest version (0.8-18).
scrot set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
pi@raspberrypi:~$ 
```

## Step 3: Basic Usage
```Shell
scrot
```

Scrot's default name convention will give you a date, time and resolution stamped file like:

`2014-10-05-132309_1824x984_scrot.png`

You can specify the file name by typing

```Shell
scrot example.png
```

The image will now be called "example", rather than “2014-10-05-132309_1824x984_scrot.png”.  
This command will not work if you do not specify a file extension (for example ".png").  
Change the output file format by changing the extension (for example ".jpeg", ".gif", etc).

## Step 4: Specify File Location
Specify where screenshots are saved with the command

```Shell
scrot /home/pi/Desktop/example.png
```

where, for example, "`/home/pi/Desktop/`" is the file path and "`example.png`" is the screenshot.

## Step 5: Delay a Screen Shot
To delay a screenshot, type

```Shell
scrot -d 10
```

where 10 is the number of seconds before capturing an image. 

To display a countdown, add the `-c` option

```Shell
scrot -cd 10
```

## Step 6: Capture Only Part of the Screen
Capture sections of the screen with the `-s` option, as can be seen in the image included, with the commands

```Shell
scrot -s
```

or

```Shell
scrot -s /home/pi/Desktop/example.png
```

to specify the file path. 

Then click and **drag** a box over the area you want to capture.

Capture the current window with the `-u` option

```Shell
scrot -u
```
