[Linux常用网络命令](http://blog.csdn.net/gavin__zhou/article/details/50888962)  
[Linux常用的网络命令](http://www.cnblogs.com/hnrainll/archive/2011/10/12/2208436.html)  

- 链路层；
- 网络层；  
- 传输层；  
- 业务层；  
- 网络诊断。  

## if

```shell
pi@raspberrypi:~ $ if
if        ifconfig  ifdown    ifquery   ifup 
```

### ifconfig

```shell
IFCONFIG(8)                  Linux System Administrator's Manual                  IFCONFIG(8)

NAME
       ifconfig - configure a network interface

SEE ALSO
       route(8), netstat(8), arp(8), rarp(8), iptables(8), ifup(8), interfaces(5).

```

## iw

iw 相关命令：

```shell
pi@raspberrypi:~ $ iw
iw        iwconfig  iwevent   iwgetid   iwlist    iwpriv    iwspy
```

```shell

pi@raspberrypi:~ $ iw
Usage:  iw [options] command
Options:
    --debug     enable netlink debugging
    --version   show version (4.9)
Commands:
    help [command]
    event [-t|-r] [-f]
    features 
    commands

pi@raspberrypi:~ $ man iw
IW(8)                                       Linux                                       IW(8)

NAME
       iw - show / manipulate wireless devices and their configuration

```

### iwgetid

```shell
# man iwgetid
IWGETID(8)                        Linux Programmer's Manual                        IWGETID(8)

NAME
       iwgetid - Report ESSID, NWID or AP/Cell Address of wireless network
```

```shell
pi@raspberrypi:~ $ iwgetid -h
Usage iwgetid [OPTIONS] [ifname]
  Options are:
    -a,--ap       Print the access point address
    -c,--channel  Print the current channel
    -f,--freq     Print the current frequency
    -m,--mode     Print the current mode
    -p,--protocol Print the protocol name
    -r,--raw      Format the output as raw value for shell scripts
    -s,--scheme   Format the output as a PCMCIA scheme identifier
    -h,--help     Print this message
```

```shell
pi@raspberrypi:~ $ iwgetid 
wlan0     ESSID:"HiWiFi"
pi@raspberrypi:~ $ iwgetid -s
HiWiFi
pi@raspberrypi:~ $ iwgetid -a
wlan0     Access Point/Cell: AA:AA:AA:2B:2B:2B
pi@raspberrypi:~ $ iwgetid -c
wlan0     Channel:1
pi@raspberrypi:~ $ iwgetid -f
wlan0     Frequency:2.412 GHz
pi@raspberrypi:~ $ iwgetid -m
wlan0     Mode:Managed
pi@raspberrypi:~ $ iwgetid -p
wlan0     Protocol Name:"IEEE 802.11"
```

### iwlist

```shell
# man iwlist

IWLIST(8)                         Linux Programmer's Manual                         IWLIST(8)

NAME
       iwlist - Get more detailed wireless information from a wireless interface

SYNOPSIS
       iwlist [interface] scanning
       iwlist [interface] frequency
       iwlist [interface] rate
       iwlist [interface] keys
       iwlist [interface] power
       iwlist [interface] txpower
       iwlist [interface] retry
       iwlist [interface] event
       iwlist [interface] auth
       iwlist [interface] wpakeys
       iwlist [interface] genie
       iwlist [interface] modulation
       iwlist --help
       iwlist --version
```

### iwconfig

```shell
pi@raspberrypi:~ $ man iwconfig

IWCONFIG(8)                       Linux Programmer's Manual                       IWCONFIG(8)

NAME
       iwconfig - configure a wireless network interface

SYNOPSIS
       iwconfig [interface]
       iwconfig interface [essid X] [nwid N] [mode M] [freq F]
                          [channel C][sens S ][ap A ][nick NN ]
                          [rate R] [rts RT] [frag FT] [txpower T]
                          [enc E] [key K] [power P] [retry R]
                          [modu M] [commit]
       iwconfig --help
       iwconfig --version
```

## host

```shell
pi@raspberrypi:~ $ host
host         hostid       hostname     hostnamectl  
```

## network

```shell
pi@raspberrypi:~ $ man networkctl 

NETWORKCTL(1)                             networkctl                            NETWORKCTL(1)

NAME
       networkctl - Query the status of network links
```

## arp/rarp

## dhcp

```shell
pi@raspberrypi:~ $ dhc
dhclient         dhclient-script  dhcpcd           dhcpcd5 
```

## ip

```shell
pi@raspberrypi:~ $ ip
ip                 ip6tables-restore  ipcrm              iptables           iptables-save
ip6tables          ip6tables-save     ipcs               iptables-apply     iptables-xml
ip6tables-apply    ipcmk              ipmaddr            iptables-restore   iptunnel
```

## ping

```shell
PING(8)                        System Manager's Manual: iputils                       PING(8)

NAME
       ping - send ICMP ECHO_REQUEST to network hosts
```

## route

```shell
pi@raspberrypi:~ $ route
route   routef  routel 
```

```shell
pi@raspberrypi:~ $ man route

ROUTE(8)                     Linux System Administrator's Manual                     ROUTE(8)

NAME
       route - show / manipulate the IP routing table
```

## traceroute

```shell
pi@raspberrypi:~ $ trace
traceproto        traceroute        traceroute6.db    traceroute-nanog  
traceproto.db     traceroute6       traceroute.db  
```

```shell
pi@raspberrypi:~ $ man traceroute

TRACEROUTE(1)                        Traceroute For Linux                       TRACEROUTE(1)

NAME
       traceroute - print the route packets trace to network host
```

## tcp

```shell
pi@raspberrypi:~ $ tcp
tcpd              tcpdchk           tcpdmatch         tcptraceroute     tcptraceroute.db
```

## netstat

### ss

```shell
pi@raspberrypi:~ $ man ss

SS(8)                              System Manager's Manual                              SS(8)

NAME
       ss - another utility to investigate sockets
```

### nc(netcat)

```shell
NC(1)                            BSD General Commands Manual                            NC(1)

NAME
     nc — arbitrary TCP and UDP connections and listens
```

### netstat

```shell
pi@raspberrypi:~ $ man netstat 

NETSTAT(8)                   Linux System Administrator's Manual                   NETSTAT(8)

NAME
       netstat  - Print network connections, routing tables, interface statistics, masquerade
       connections, and multicast memberships

```

### tcpdump

## tools

### telnet

### lynx

### curl

### wget

### axel

