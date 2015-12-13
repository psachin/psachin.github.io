---
layout: post
title: Qemu - System emulator
tags: qemu, ssh
category: blog
permalink: /blog/qemu/
comments: true
---

In this post I will create an Qemu image and work with it remotely
using SSH.

## Steps

1. Download and install qemu from this
   [link](http://wiki.qemu.org/Main_Page).
2. Create a raw image, install
   [ubuntu 12.04](http://releases.ubuntu.com/12.04/) from an ISO
   image.
3. Boot from an installed image and redirect port 22 to port 2200 of
`localhost`.
4. Create snapshot of an image.
5. Booting snapshot image.

## Download and install qemu

On Debian based distros(Ubuntu, Mint etc.) install qemu using the
command

    sudo apt-get install qemu-system

This will install all qemu-system binaries for all major CPU
architectures. If you are having RPM based distro(like Redhat, Fedora
etc.), type

    sudo yum install qemu

Optionally you can also compile qemu from the latest stable
[source](http://wiki.qemu.org/download/qemu-1.2.0-rc0.tar.bz2). Please
refer the README for compilation instructions.

## Create qemu image

We need to first create a raw qemu image using the command

    qemu-img create -f raw IMAGE_NAME.img SIZE

For example, if I want to create an image of 32 Gigs with the name
_ics-testing.img_, the command would be

    qemu-img create -f raw ics-testing.img 32G

Once the image is created, we can use it as a raw disk image and
install an OS(Distro of your choice). In this case I will install
[ubuntu 12.04](http://releases.ubuntu.com/12.04/ubuntu-12.04-desktop-amd64.iso)
(AMD64) from an ISO image.

The syntax would be

    qemu-system-ARCH -vnc none,ipv4 -hda IMAGE_NAME -cdrom /PATH/TO/ISO/FILE -m MEMORY -enable-kvm

For example, if my system arch is `x86-64` and my ISO path is
`/home/devils/iso/ubuntu-12.04-desktop-amd64.iso` with memory as 4
Gigs. Also I want to enable kernel based virtualization.

    qemu-system-x86_64 -vnc none,ipv4 -hda ics-testing.img \
    -cdrom /home/devils/iso/ubuntu-12.04-desktop-amd64.iso \
    -m 4096 -enable-kvm

this will pop up a qemu window. Proceed with the installation and
reboot the system.

## Boot using qemu image

Once the installation is complete, boot the image by typing,

    qemu-system-x86_64 -vnc none,ipv4 -hda ics-testing.img \
    -m 4096 -enable-kvm

Now configure the system, its package manager and user account.
Install Openssh-server and enable SSH login. If everything is
configured, restart using,

    qemu-system-x86_64 -vnc none,ipv4 -hda ics-testing.img \
    -m 4096 -enable-kvm \
    -redir tcp:2200::22

The `-redir tcp:2200::22` redirects TCP traffic on the host port 2200
to the guest machine (QEMU) port 22. This allows us to SSH to the port
2200 on localhost.

`-vnc none` will disable VNC server.

-  SSH to qemu

    You can ssh into the running qemu system using a command

        ssh -p PORT USER@IP-address or HOSTNAME

    for example, if I want to connect to port 2200 of `localhost` with
    username as `qemu-user`, then

        ssh -p 2200 qemu-user@localhost

    as port 2200 on `localhost` is open and is binded with port 22 of
    qemu system, thus we used `-p 2200` flag.

## Creating snapshots of an image(Optional)

Now as the image is configured and working, we can also create a
snapshots of that image and work on it keeping an original image
intact.

syntax:

    qemu-img create -f qcow2 -b ORIGINAL_IMAGE_NAME SNAPSHOT_IMAGE_NAME

As my original image name was _ics-testing.img_, Let my snapshot image
name be _snapshot.img_. Type

    qemu-img create -f qcow2 -b ics-testing.img snapshot.img

`-f` flag will specify image format. In this case it is `qcow2` which
is most versatile qemu-image format. Please refer man-pages for more
detail.

## Booting snapshot image

You can use the snapshot image using

    qemu-system-x86_64 -vnc none -hda snapshot.img \
    -m 4096 -enable-kvm \
    -redir tcp:2200::22

### Tips

a. You can also specify number of CPU cores using `-smp` flag. For
example, if you want to assign 4 cores of your physical system to
qemu, specify it as `-smp 4`. `smp` stands for
[Symmetric-multiprocessing](http://en.wikipedia.org/wiki/Symmetric_multiprocessing).

b. Don't you run qemu over the snapshot image, it will corrupt the
snapshot image.

### Refs

1.  [Qemu](http://wiki.qemu.org/Main_Page)
2.  [Ubuntu 12.04](http://releases.ubuntu.com/12.04/)
3.  [Creating snapshots](http://wiki.qemu.org/Documentation/CreateSnapshot)
