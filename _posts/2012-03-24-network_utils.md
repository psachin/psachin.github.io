---
layout: post
title: Network utilities
tags: ifconfig, ip, command line, terminal
category: blog
permalink: /blog/network-utils/
author: sachin
comments: true
---


Few network configuration which can be performed using CLI, this post
covers examples with syntax.

(Updated on Aug 09, 2018)


_Note_: You must be `root` or `sudo` user to run following commands.
_Note_: `ifconfig` has been deprecated in favor of `ip`

## Assign IP address

Syntax

    ifconfig <INTERFACE> <IP-ADDRESS> netmask <NETMASK>

	# or

	ip addr add <IP-ADDRESS/CIDR> dev <INTERFACE>

Example

    ifconfig eth0 192.168.1.11 netmask 255.255.255.0

	# or

	ip addr add 192.168.1.11/24 dev eth0

## Add gateway/route

Syntax

    route add default gw <GATEWAY-IP> <INTERFACE>

	# or

	ip route add default via <GATEWAY-IP> dev <INTERFACE>

Example

    route add default gw 192.168.1.1 eth0

    # or

	ip route add default via 192.168.1.1 dev eth0

## Temporary spoof MAC address

Syntax

	ip link set down dev DEVICE_NAME
	ip link set dev DEVICE_NAME address AA:BB:CC:DD:EE:FF
	ip link set up dev DEVICE_NAME

Example

	ip link set down dev enp0s21
	ip link set dev enp0s21 address AA:BB:CC:DD:EE:FF
	ip link set up dev enp0s21

## Set DNS address

Optionally DNS can be entered in the file `/etc/resolv.conf` in
following format

    # /etc/resolv.conf
    nameserver 8.8.8.8
    nameserver 8.8.4.4

All the above changes will be temporary(unless you reboot the system)

## Additional scenario

- You want 10.10.10.x address space to bypass default gateway of the
  network. You can reach network range of 10.10.10.0/24 via
  192.168.1.11 on device `eth0`

      ip route add 10.10.10.0/24 via 192.168.1.11 dev eth0


### Make routes persistent(on Fedora/RHEL)

Add following entry into the file
`/etc/sysconfig/network-scripts/route-DEVICE_NAME`

	10.10.10.0/24 via 192.168.1.11 dev DEVICE_NAME

### CLI to control NetworkManager

- Check overall status

      nmcli general status

- Show all connections

      nmcli connection

- Show details for specific connection

      # Syntax
      nmcli connection show <GENERAL.NAME>

      # Example
      nmcli connection show my-dsl-conn

- Connect using connection name

      # Syntax
      nmcli connection up <GENERAL.NAME>

      # Example
      nmcli connection up my-dsl-conn
