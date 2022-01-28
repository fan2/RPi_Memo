## [RASPBERRY PI BOOT MODES](https://www.raspberrypi.org/documentation/hardware/raspberrypi/bootmodes/)

[**HOW TO BOOT FROM A USB MASS STORAGE DEVICE ON A RASPBERRY PI**](https://www.raspberrypi.org/documentation/hardware/raspberrypi/bootmodes/msd.md)

## instruction

[How to Make Raspberry Pi 3 Boot From USB](https://www.makeuseof.com/tag/make-raspberry-pi-3-boot-usb/)  

[How to boot your Raspberry Pi from a USB mass storage device](https://thepi.io/how-to-boot-your-raspberry-pi-from-a-usb-mass-storage-device/)  

[**BOOT THE RASPBERRY PI FROM USB**](https://www.instructables.com/id/Boot-the-Raspberry-Pi-from-USB/)  

## forums

[How can I boot CentOS 7 from USB drive not from SD card in RPI3?](https://raspberrypi.stackexchange.com/questions/78394/how-can-i-boot-centos-7-from-usb-drive-not-from-sd-card-in-rpi3)

[How to boot ANY pi distro from usb?](https://www.raspberrypi.org/forums/viewtopic.php?f=29&t=189147)

### [Booting from USB](https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=198258&sid=4cf685017c1dde9bdeb136cb89fa1882)  

**`boot options`**：

The Pi3 will check for a boot SD card first, before booting from a USB device. If no boot SD card is found in 5 seconds, then it looks for a boot USB device. So even if the boot USB device is still connected, inserting an SD card will override it.

**`boot from the sd and get the OS from an ssd`**:

I'm sure if i tried every USB MSD in my rather extensive collection I could find something that worked, but I'm fine with leaving `/boot` on the **SD** card and running the OS from **SSD**. It's 100% reliable (boot, restart and shutdown all function as expected), and the boot time is actually quicker since there is no 5 second SD card timeout.

### [Running Raspbian on USB Devices : Made Easy](https://www.raspberrypi.org/forums/viewtopic.php?f=29&t=196778)

How to configure and reliably run Raspbian on a USB flash drive, USB hard drive, or USB SSD instead of an SD card?

A Raspberry Pi 3 has a USB boot mode that has to be permanently enabled by setting an `OTP` bit.

The easiest and most reliable way to run Raspbian on a USB device is to leave an SD card containing Raspbian in place, but use it only for starting Raspbian that is residing on a USB device.

**`usb-boot`**

usb-boot first presents a list of available USB mass storage devices and asks: **'Select the USB mass storage device to boot'**

Use the `arrow` keys on your keyboard to navigate to the desired device and press the `spacebar` to select it. Then use the `tab` key to navigate to the **'Ok'** or **'Cancel'** button and press the `return` key.

usb-boot will then ask: **'Replicate BOOT/ROOT contents from /dev/mmcblk0 to /dev/sdX?'**

`/dev/mmcblk0` is the SD card and `/dev/sdX` is the USB device.

- Select **'No'** if the USB device already has Raspbian on it and you wish to use it (nothing will be copied).  
- Select **'Yes'** if you want to copy the Raspbian on your SD card to the USB device (everything will be copied).  

If you select **'Yes'**, you will be warned: **'All existing data on USB device /dev/sdX will be destroyed!' and asked: 'Do you wish to continue?'**

If you select **'Yes'**, the copy will begin. The time required for this process will depend on the amount of data on your SD card and the speed of your storage devices.

usb-boot will then complete the configuration process and warn you of any potential conflicts it detects.

When usb-boot has finished, you should be able to simply reboot and be running Raspbian on the USB device.

Note: Do NOT use usb-boot with `NOOBS`.

---

The Pi3 will default to booting from an SD card even with that bit set, so setting the bit does not **REQUIRE** you to boot from USB, it only *enables* it.

If you want to experiment with USB boot, then go right ahead and set the bit, and if you find that USB boot does not suit your needs, then just insert a boot SD card and your Pi3 will boot from it exactly like it did before.
