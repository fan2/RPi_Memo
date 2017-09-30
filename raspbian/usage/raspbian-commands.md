# commands
## systemctl
执行 `man systemctl` 命令，查看 Manual page systemctl：

```Shell
pi@raspberrypi:~$ man systemctl
SYSTEMCTL(1)                       systemctl                      SYSTEMCTL(1)

NAME
       systemctl - Control the systemd system and service manager

```

执行 `systemctl -h`（`systemctl --help`）查看帮助说明，以下节选 **System Commands** 部分：

```Shell
System Commands:
  is-system-running               Check whether system is fully running
  default                         Enter system default mode
  rescue                          Enter system rescue mode
  emergency                       Enter system emergency mode
  halt                            Shut down and halt the system
  poweroff                        Shut down and power-off the system
  reboot [ARG]                    Shut down and reboot the system
  kexec                           Shut down and reboot the system with kexec
  exit [EXIT_CODE]                Request user instance or container exit
  switch-root ROOT [INIT]         Change to a different root file system
  suspend                         Suspend the system
  hibernate                       Hibernate the system
  hybrid-sleep                    Hibernate and suspend the system
```

## dmesg
执行 `man dmesg` 命令，查看 Manual page dmesg：

```Shell
pi@raspberrypi:~$ man dmesg
DMESG(1)                         User Commands                        DMESG(1)

NAME
       dmesg - print or control the kernel ring buffer

DESCRIPTION
       dmesg is used to examine or control the kernel ring buffer.
```

执行 `dmesg -h`（`dmesg --help`）查看帮助说明，以下节选 **log** 部分：

```Shell
pi@raspberrypi:~$ dmesg -h

Usage:
 dmesg [options]

Display or control the kernel ring buffer.

Supported log facilities:
    kern - kernel messages
    user - random user-level messages
    mail - mail system
  daemon - system daemons
    auth - security/authorization messages
  syslog - messages generated internally by syslogd
     lpr - line printer subsystem
    news - network news subsystem

Supported log levels (priorities):
   emerg - system is unusable
   alert - action must be taken immediately
    crit - critical conditions
     err - error conditions
    warn - warning conditions
  notice - normal but significant condition
    info - informational
   debug - debug-level messages
```