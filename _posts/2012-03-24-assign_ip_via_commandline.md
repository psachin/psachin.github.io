---
layout: post
title: Assign IP address via command-line
tags: ifconfig, ip, command line, terminal
category: blog
permalink: /blog/ipaddress-commandline/
author: sachin
comments: true
---

Sometimes, assigning IP address using command line is much more easier
than using Network manager applet, this post covers examples with
syntax

(Updated on June 17, 2017)


_Note_: You must be `root` or `sudo` user to run following commands.
`ifconfig` has been deprecated in favor of `ip`

## Assign IP address

Syntax

``` bash
ifconfig <INTERFACE> <IP-ADDRESS> netmask <NETMASK>
# or
ip addr add <IP-ADDRESS/CIDR> dev <INTERFACE>
```

Example

``` bash
ifconfig eth0 192.168.1.11 netmask 255.255.255.0
# or
ip addr add 192.168.1.11/24 dev eth0
```

## Add gateway/route

Syntax


``` bash
route add default gw <GATEWAY-IP> <INTERFACE>
# or
ip route add default via <GATEWAY-IP> dev <INTERFACE>
```

Example

``` bash
route add default gw 192.168.1.1 eth0
# or
ip route add default via 192.168.1.1 dev eth0
```

## Set DNS address

Optionally DNS can be entered in the file `/etc/resolv.conf` in
following format

``` bash
# /etc/resolv.conf
nameserver 8.8.8.8
nameserver 8.8.4.4
```

All the above changes will be temporary(unless you reboot the system)

## Additional scenario

- You want 10.10.10.x address space to bypass default gateway of the
  network. You can reach network range of 10.10.10.0/24 via
  192.168.1.11 on device `eth0`

``` bash
ip route add 10.10.10.0/24 via 192.168.1.11 dev eth0
```

### Make routes persistent on Fedora

Add following entry into the file
`/etc/sysconfig/network-scripts/route-DEVICE_NAME`

``` bash
10.10.10.0/24 via 192.168.1.11 dev DEVICE_NAME
```
