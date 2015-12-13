---
layout: post
title: Assign IP address via command-line
tags: ifconfig, command line, terminal
category: blog
permalink: /blog/ipaddress-commandline/
comments: true
---

Sometimes, assigning IP address using command line is much more easier
than using Network manager applet, this post covers examples with
syntax

_Note_: You must be `root` or `sudo` to run following commands

## Assign IP address

Syntax

    ifconfig <INTERFACE> <IP-ADDRESS> netmask <NETMASK>

Example

    ifconfig eth0 192.168.1.11 netmask 255.255.255.0

## Add gateway/route

Syntax

    route add default gw <GATEWAY-IP> <INTERFACE>

Example

    route add default gw 192.168.1.1 eth0

## Set DNS address

Optionally DNS can be entered in the file `/etc/resolv.conf` in
following format

    # /etc/resolv.conf
    nameserver 8.8.8.8
    nameserver 8.8.4.4

All the about changes will be temporary(unless you reboot the system)
